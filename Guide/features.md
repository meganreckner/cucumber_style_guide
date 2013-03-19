# Features
These guidelines cover best practices for structuring Cucumber features.

## Format
Features are defined using three components.

1. Feature
2. Benefit
3. Stakeholder

The first line starts with the `Feature` keyword, followed by the name of the feature. See the example below.

    Feature: Select subscription level
      As a customer
      I want to be able to select a subscription level
      so that I can purchase it


This is known as the Connextra format for user stories. In the above example, "customer" is the stakeholder, the ability to select a subscription level is the feature, and the ability to purchase an item is the benefit to the stakeholder.

## General Guidelines
#### Define only one feature per file
A feature should be clearly defined and focused. If you are attempting to accomplish more than one task in a feature, it should be broken out into multiple features.

* Prevents feature files from getting overblown with scenarios
* Increases ease of maintaining feature sets

#### Frame features in terms of their value to users


    Feature: Select subscription level
      As a customer
      I want to be able to select a subscription level
      so that I can purchase it


#### Use Background to set up 
Background is a special type of scenario. Data setup?