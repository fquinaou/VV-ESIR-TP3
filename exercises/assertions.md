# On assertions

Answer the following questions:

1. The following assertion fails `assertTrue(3 * .4 == 1.2)`. Explain why and describe how this type of check should be done.

2. What is the difference between `assertEquals` and `assertSame`? Show scenarios where they produce the same result and scenarios where they do not produce the same result.

3. In classes we saw that `fail` is useful to mark code that should not be executed because an exception was expected before. Find other uses for `fail`. Explain the use case and add an example.

4. In JUnit 4, an exception was expected using the `@Test` annotation, while in JUnit 5 there is a special assertion method `assertThrows`. In your opinion, what are the advantages of this new way of checking expected exceptions?

## Answer

1. The assertion fails because of the inaccuracies related to the floating-point numbers (double and float). It fails because of how these numbers are represented in memory. The calculated value of 3 * 0.4 is not exactly 1.2 in memory.

Correct code:

double result = 3 * 0.4;
double expected = 1.2;
double epsilon = 0.000001;
assertTrue(Math.abs(result - expected) < epsilon);

2. AssertEquals uses the equals method of the objects to see if their are equals where AssertSame verifies that two objects are the same instance (same address in memory).

Same results : 
String str1 = "Hello";
String str2 = str1; 
assertEquals(str1, str2);  // Values are equal
assertSame(str1, str2);    // Same memory reference

Differents results : 

String s1 = new String("Hello");
String s2 = new String("Hello");  // Different instances with the same value
assertEquals(str1, str2);  // Values are equal
assertSame(str1, str2);    // Fails because different instances


3. fail can be used to explicitly mark a failure in the case where an unexpected condition occurs or to indicate that a test did not complete correctly. It can also be used to indicate that certain code branches should never be reached.

public void testValueRange() {
    int value = getValue();
    if (value > 10) {
        // Test logic for value > 10
    } else if (value < 0) {
        // Test logic for value < 0
    } else {
        fail("The value is out of the expected range!");
    }
}


4. Advantages of assertThrows:

More precise control: With assertThrows, you can test not only the type of the exception but also check additional conditions after the exception is thrown. For example, you can analyze the exception's error message.
More limited test scope: In JUnit 4, the exception could be thrown at any point in the test method, which could lead to less precise tests. With assertThrows, the exception must be thrown specifically in a block of code, ensuring that only the part of the code you want to test is involved.
Improved readability: assertThrows is more explicit and makes the test more readable. It clearly shows which part of the code is expected to throw the exception.

@Test
void testDivisionByZero() {
    ArithmeticException exception = assertThrows(ArithmeticException.class, () -> {
        int result = 10 / 0;
    });
    assertEquals("/ by zero", exception.getMessage());
}
