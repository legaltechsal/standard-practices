# Introduction
This document or guidelines are the standard practise of LTS' Java development in which to promote the consistency of convention across all system within LTS' software/service implementations in Java stack.

# 1. Clean code and conventions

- What is clean code and why have conventions?
    - A code that any develope rcan read and change easily.
    - Software code spents majority of time in maintenance.
    - Source code as a product.

# 2. Souce file

- Filename
    - Case sensitive name of the top level calss it contins
    - .java extension

- File encoding
    - UTF-8

# 3. Source file structure

Consists of the following in order:
- License or copyright information (optional).
- Package statement.
- Import statements
    - No widecard imports.
    - All static imports in a single block.
    - All non-static imports in a single block.
    - Within each block, imported names appear in ASCII sort order.
- Exactly on top-level class.

# 4. Source file formatting

- 4.1 Braces
    - Are used with if, else, for, do and while statements even when the bod is empty or contains only a single statement.

- 4.2 Block indentation
    - Keep to a consistent number of spaces.

- 4.3 Column limit
    - Keep within a consistent number of characters.
    - Exception:
        - Package and import statements.

- 4.4 Line wrapping
    - Break after a comma.
    - Break before an operator
    - Prefer high-level breaks to lower-level breaks.
    - Align the new line with the beginning of the expression at the same level on the previous line.
    - If the above rules lead to confusing code or to code that's squished up against the right margin, just indent 8 spaces instead.

``` java
longName1 = longName2 * (longName3 + longName4 - longName5)
            + 4 * longName6; // Preferred

longName1 = longName2 * (longName3 + longName4
                         - longName5) + 4 * longName6; // Avoid

// Don't use this indentation
if ((condition1 && ocndition2)
    || (condition3 && condition4)
    ||!(condition5 && condition6)) {   // Bad Wraps
    doSomethingAboutIt();              // Make this line easy to miss
}

// Use this indentation instead
if ((condition1 & condition2)
        || (condition3 && condition4)
        ||!(condition5 && condition6)) {
    doSomethingAboutIt();
}

// Or use this
if ((condition1 & condition2) || (condition3 && condition4)
        ||!(condition5 && condition6)) {
    doSomethingAboutIt();
}
```

# 5. Naming
- Class names in UpperCamelCase
    - Typically nouns or noun phrases e.g. `Person`.
    - Test class ends with 'Test' e.g. `PersonTest`.
- Method names in `lowerCamelCase`.
- Constant names use `UPPER_SNAKE_CASE`.
- Non constant field names in `lowerCamelCase`.
- Local variable names in `lowerCamelCase`.

# 6. Programming Practises
- `@Override` annotation must be always used.
- Do not ignore caught exceptions
    - If no action, add a comment to explain why.
- Use class name to access class (static) variables / methods
    - e.g. `Aclass.classMethod();` // OK
    - e.g. `anObject.classMethod();` // AVOID

# 7. Javadoc
General basic form:
``` java
/**
 * Multiple lines
 */
public String method(String p1) { ... }
```
For public class and public or protected member of such class
- Exceptions
    - Self explanatory member e.g. getFoo().
    - Method that overrides a supertype method.

# 8. References
- [Oracle Code Convention](https://www.oracle.com/technetwork/java/codeconventions-150003.pdf)
- [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)