# Features
These guidelines cover best practices for structuring Cucumber features.

## General Guidelines
#### Each feature file should contain only one feature
A feature should be clearly defined and focused. If you are attempting to accomplish more than one task in a feature, it should be broken out into multiple features.

* Prevents feature files from getting overblown with scenarios
* Increases ease of maintaining feature sets

## Format
Features are defined using three components.

1. Feature
2. Benefit
3. Stakeholder

The first line starts with the `Feature` keyword, followed by the name of the feature. See the example below.

    Feature: Add item to cart
      As a customer
      I want to be able to add an item to my cart
      so that I can purchase it


This is known as the Connextra format for user stories.
