---
sidebar_position: 7
---

# When

When keyword defines the test action which will be executed.  
By test action we mean the user input action.

## Example

```gherkin
Feature: Calculator

Calculator for adding two numbers

Scenario: Add two numbers
Add two numbers with the calculator
Given I have entered 50 into the calculator
And I have entered 70 into the calculator

When I press add
```

## References

- https://specflow.org/learn/gherkin
