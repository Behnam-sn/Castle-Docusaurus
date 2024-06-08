---
sidebar_position: 3
---

# Testing Strategy

The knowledge of both the business logic implementation pattern and the architectural pattern,  
Can be used as a heuristic for choosing a testing strategy for the codebase.

The difference between the testing strategies is their emphasis on the different types of tests:  
unit, integration, and end-to-end.

Let’s analyze each strategy and the context in which each pattern should be used.

## Testing Pyramid

The classic testing pyramid emphasizes unit tests, fewer integration tests, and even fewer end-to-end tests.

Both variants of the domain model patterns are best addressed with the testing pyramid.

Aggregates and value objects make perfect units for effectively testing the business logic.

## Testing Diamond

The testing diamond focuses the most on integration tests.

When the active record pattern is used, the system’s business logic is, by definition, spread across both the
service and business logic layers.
