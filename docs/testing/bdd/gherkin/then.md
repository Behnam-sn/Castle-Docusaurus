---
sidebar_position: 8
---

# Then

Then keyword defines the outcome of previous steps.

## Example

```gherkin
Feature: Calculator

Calculator for adding two numbers

Scenario: Add two numbers
Add two numbers with the calculator
Given I have entered 50 into the calculator
And I have entered 70 into the calculator

When I press add
Then the result should be 120 on the screen
```

## References

- https://specflow.org/learn/gherkin
