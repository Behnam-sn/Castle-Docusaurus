---
sidebar_position: 11
---

# Data Tables

Data Tables are handy for passing a list of values to a step definition.  
A useful tool in complex Gherkin examples.

## Example

```gherkin
Feature: Calculator

Calculator for adding two numbers

@mytag
Feature: Calculator

Calculator for adding two numbers

@mytag
Scenario: Add two numbers
Add two numbers with the calculator
Given I have entered <First> into the calculator
And I have entered <Second> into the calculator

When I press add
Then the result should be <Result> on the screen
Examples:
| First | Second | Result |
| 50    | 70     | 120    |
| 30    | 40     | 70     |
| 60    | 30     | 90     |
```

## References

- https://specflow.org/learn/gherkin
