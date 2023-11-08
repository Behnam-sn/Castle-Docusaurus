---
sidebar_position: 9
---

# Tags

Then keyword defines the outcome of previous steps.You can place tags above Feature to group related features, independent of your file and directory structure.  
Furthermore you can filter tags within your CI/CD-pipeline.

## Example

```gherkin
Feature: Calculator

Calculator for adding two numbers

@mytag
Scenario: Add two numbers
Add two numbers with the calculator
Given I have entered 50 into the calculator
And I have entered 70 into the calculator

When I press add
Then the result should be 120 on the screen
```

## References

- https://specflow.org/learn/gherkin
