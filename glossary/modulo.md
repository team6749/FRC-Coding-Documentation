is the remainder of a division.

eamples:
10 % 3 = 1 ( 3 remainder 1)
2 % 2 = 0 (1 remainder 0)

a useful trick of modulo is to see if a number is even by doing mod 2.
it can also be used to handle cyclic sensor data like ensuring that a value is within the range of 0 and 360.


code example:
```java
value = 365.5;
double range = value % 360;
System.out.println(range); // 5.5
```

