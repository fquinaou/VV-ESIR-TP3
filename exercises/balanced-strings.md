# Balanced strings

A string containing grouping symbols `{}[]()` is said to be balanced if every open symbol `{[(` has a matching closed symbol `)]}` and the substrings before, after and between each pair of symbols is also balanced. The empty string is considered as balanced.

For example: `{[][]}({})` is balanced, while `][`, `([)]`, `{`, `{(}{}` are not.

Implement the following method:

```java
public static boolean isBalanced(String str) {
    ...
}
```

`isBalanced` returns `true` if `str` is balanced according to the rules explained above. Otherwise, it returns `false`.

Use the coverage criteria studied in classes as follows:

1. Use input space partitioning to design an initial set of inputs. Explain below the characteristics and partition blocks you identified.
2. Evaluate the statement coverage of the test cases designed in the previous step. If needed, add new test cases to increase the coverage. Describe below what you did in this step.
3. If you have in your code any predicate that uses more than two boolean operators, check if the test cases written so far satisfy *Base Choice Coverage*. If needed, add new test cases. Describe below how you evaluated the logic coverage and the new test cases you added.
4. Use PIT to evaluate the test suite you have so far. Describe below the mutation score and the live mutants. Add new test cases or refactor the existing ones to achieve a high mutation score.

Write below the actions you took on each step and the results you obtained.
Use the project in [tp3-balanced-strings](../code/tp3-balanced-strings) to complete this exercise.

## Answer

1. We can partition the input space based on several characteristics of the input strings:

 - Empty string: The string contains no characters.
    Example: ""
 - Single type of grouping symbols: The string contains only one type of symbol ( only () or {} or []).
    Balanced example: "()", "{}", "[]".
    Unbalanced example: "(", "{", "]".
 - Mixed types of symbols but in the correct order: The string contains multiple types of symbols, but they are balanced.
     Balanced example: "{[]}", "({})", "([])", "({[]})".
 - Mixed types of symbols but in the wrong order: The string contains symbols that are not properly matched or ordered.
   Unbalanced example: "([)]", "([}", "{".
 - Extra or unmatched opening symbols: The string has more opening symbols than closing ones.
    Unbalanced example: "({[]", "(((".
 - Extra or unmatched closing symbols: The string has more closing symbols than opening ones.
    Unbalanced example: "()))", "[]]".

2. We execute the tests with coverage and we got 100% coverage, we can conclude that the tests are working.

3. No need to implement other test because with have 100% test coverage

4. We can use pit by copying this in the pom.xml file.
<plugin>
    <groupId>org.pitest</groupId>
    <artifactId>pitest-maven</artifactId>
    <version>LATEST</version>
    <configuration>
        <targetClasses>
            <param>com.your.package.root.want.to.mutate*</param>
        </targetClasses>
        <targetTests>
            <param>com.your.package.root*</param>
        </targetTests>
    </configuration>
</plugin>

after that we execute this command line : mvn test-compile org.pitest:pitest-maven:mutationCoverage