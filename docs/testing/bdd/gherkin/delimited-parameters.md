---
sidebar_position: 10
---

# Delimited parameters

Delimited parameters \<\> are used as references which are referred to in the example tables.  
SpecFlow will automatically replace these parameters when executing tests.

## Example

```gherkin
Feature: Calculator

Calculator for adding two numbers

@mytag
Scenario: Add two numbers
Add two numbers with the calculator
Given I have entered <First> into the calculator
And I have entered <Second> into the calculator

When I press add
Then the result should be <Result> on the screen
```

## References

- https://specflow.org/learn/gherkin
