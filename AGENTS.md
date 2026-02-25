# Code Cleanup Guide

## Goal

Improve code quality and consistency across robot codebases without changing core functionality or tuned values. The heart of each subsystem — its control logic,
hardware configuration, and tuning constants — stays intact. We're only cleaning up how the code is written, not what it does.

Reference standard: [FRC-Coding-Documentation](https://github.com/team6749/FRC-Coding-Documentation)

---

## Ground Rules

- **Do not change tuning values** (PID gains, feedforward constants, current limits, velocity/acceleration limits, gear ratios, CAN IDs, thresholds). These belong to the
hardware team and require physical testing to verify. You CAN identify obvious bugs like type conversion issues or private vs public, etc..
- **Do not refactor subsystem architecture** — no moving logic between classes, no new abstractions, no design changes.
- **Always build and confirm successful compilation before committing.** Use the WPILib JDK:
./gradlew build -Dorg.gradle.java.home="C:/Users/Public/wpilib/2026/jdk"
- **Present the list of proposed changes grouped by type and get approval before making any edits.**
- When resolving merge conflicts, flag any tuning value differences rather than silently adopting one side — let the team decide.

---

## Workflow

1. Identify cleanup opportunities and group them by type (see categories below).
2. **Present the grouped list to the team for approval/feedback before editing anything.**
3. Apply one group at a time, build to confirm it compiles, then commit that group.
4. Repeat for each approved group.

This keeps the git history readable — each commit has a clear, single purpose.

---

## Change Categories

### 1. Access Modifiers — `private` on fields

Fields that are only used within their own class should be declared `private`. This enforces encapsulation and prevents accidental access from outside the class.

**What to look for:**
- Fields with no access modifier (package-private by default)
- Fields declared `public` that are never accessed outside their class

**What NOT to change:**
- Fields that are intentionally public API (accessed from other classes)
- Static utility fields like `SparkUtil.sparkStickyFault` that are designed for shared access

**Example:**
```java
// Before
SendableChooser<Boolean> disableOutput = new SendableChooser<>();
PIDController motorPID = new PIDController(0, 0, 0);

// After
private SendableChooser<Boolean> disableOutput = new SendableChooser<>();
private PIDController motorPID = new PIDController(0, 0, 0);
```
---
2. Immutability — final on constants

Fields and variables that are assigned once and never reassigned should be declared final. This is especially important for constants in *Constants.java files and robot-wide
values in Constants.java.

What to look for:
- public static fields in constants files missing final
- Fields initialized in the constructor or at declaration that are never reassigned
- Local variables that are assigned once

What NOT to change:
- Fields that are intentionally mutable (target states, PID setpoints, mode flags)
- Tuning constants — adding final is fine, but do not change the values

Example:
```java
// Before
public static double gearReduction = 3.0;
public static AngularVelocity maxVelocity = DegreesPerSecond.of(90);

// After
public static final double gearReduction = 3.0;
public static final AngularVelocity maxVelocity = DegreesPerSecond.of(90);
```
---
3. Naming Conventions

All names should follow standard Java camelCase conventions and be descriptive.

What to look for:
- Hungarian notation prefixes: m_fieldName → fieldName
- Non-descriptive variable names: myInputs → lastInputs
- Method names starting with uppercase: LinearToAngularVelocity() → linearToAngularVelocity(), Pivot() → pivot()
- Confusing boolean names: isHomedAsterisk → isDeploymentComplete
- Local variable config objects with wrong casing: TurretMotorConfig → turretMotorConfig
- Constants named too generically for their context: motorCanId in TurretConstants → turretMotorCanId

What NOT to change:
- Names that are part of a public interface or override a parent method
- Names already in use across many files (defer to a dedicated rename PR)

---
4. Dead and Stale Comments

Comments that restate what the code does, contain leftover debug notes, or are no longer accurate should be removed. Per the coding standard, comments should only explain why
something is done, not what — the code should speak for itself.

What to look for:
- Comments that just restate the line of code below them
- Frustration/joke comments left in production code
- Wrong Javadoc (e.g., /** Creates a new Intake. */ on a Feeder class)
- TODO comments that have already been resolved
- Commented-out code with no obvious purpose — but read the context first (see below)

Use judgment on commented-out code. Not all of it is dead. Some areas of the codebase — especially configureBindings(), deployment sequences, and active math/control logic —
deliberately keep multiple implementation options commented out while the team experiments. A single commented-out line next to an active one is often a "we tried this, might go
back" marker, not garbage. Ask yourself:
- Is this in an area where multiple approaches are clearly being explored?
- Would removing it lose useful context for the next person?

If yes, leave it. Only remove commented-out code that is clearly obsolete and provides no navigational or historical value.

What NOT to remove:
- TODOs that flag real open issues needing team discussion
- Comments explaining non-obvious logic or edge cases
- Comments calling out known hardware quirks or bugs
- Commented-out alternatives in actively evolving sections of code
- System.err.println calls used for hardware bounds or safety diagnostics — these signal when a subsystem is being commanded outside its physical limits and are not debug noise

---
5. Hardcoded Values → Constants

Magic numbers embedded directly in code should be extracted to the appropriate *Constants.java file. This makes it easier to update values in one place and understand what they
represent.

What to look for:
- CAN IDs, port numbers, or device addresses hardcoded inline
- Physical measurements (wheel diameters, circumferences, gear ratios) defined as field-level variables instead of constants
- String literals for camera/device names used directly instead of through a constants class

Subsystem ownership of hardware IDs. A subsystem's CAN ID belongs in that subsystem's constants file and should be referenced directly by its IO class — not passed in as a
constructor argument from RobotContainer. For example, TurretIOReal should reference TurretConstants.turretMotorCanId internally rather than accepting an int turretPort
parameter. This keeps hardware configuration localized to where it belongs.

What NOT to change:
- Values that are already in constants files
- Simulation placeholder values (0.0, etc.) that are intentionally not real hardware values

---
6. Gear Ratio Notation

This is a conventions rule, not a correctness fix.

Gear ratios should always be written as explicit fractions, even when they reduce to a whole number. The fraction communicates mechanical intent — a reader can see which stage
is which and verify the math against the physical gearbox.

// Wrong — loses mechanical meaning
public static final double gearReduction = 3.0;

// Right — readable as a physical ratio
public static final double gearReduction = 3.0 / 1.0;

// Also right — multi-stage ratio, each stage visible
public static final double gearReduction = (120.0 / 31.0) * (3.0 / 1.0);

What NOT to do:
- Do not simplify 3.0 / 1.0 to 3.0 — this erases the ratio notation
- Do not treat 3d / 1d as accidental — the d suffix is intentional double notation, not sloppy code
- Do not convert ratio expressions under "minor correctness" without confirming they aren't intentional ratio notation

---
7. Minor Correctness Issues

Small bugs or inconsistencies that are clearly unintentional.

What to look for:
- Integer division where floating-point is intended: (4/1)*(32/14) → (4.0/1.0)*(32.0/14.0)
- Typos in string literals, variable names, or method names: votlage, Chasssis
- Duplicate imports
- Unused imports left behind after refactoring
- Deprecated API calls with non-breaking replacements available in the current library

What NOT to change:
- Any value that could be intentional hardware tuning, even if it looks wrong — flag it and ask first
- Division expressions in constants files that look like ratios — see Section 6 before touching these

---
What This Cleanup Does NOT Include

- Changing control logic, PID behavior, or subsystem state machines
- Restructuring class hierarchies or moving code between files
- Adding new features or commands
- Changing tuned values (gains, limits, thresholds, CAN IDs, gear ratios) — always ask before touching these
- Silently resolving merge conflicts on tuning values — flag them for team review