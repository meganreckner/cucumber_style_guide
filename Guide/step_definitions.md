# Step Definitions
These guidelines cover best practices for structuring Cucumber step definitions.

## Format
Step definitions are defined using a regular expression matching the step description.

Step:

    When I view my profile page
    
Step definition:

    When /^I view my profile page$/ do
      # some code
    end


#### Use regular expressions to pass arguments into a step
Each regular expression in a step is treated as an argument that can be used within the step definition.

If you have the step:

    Given I am an "admin" user for the "test" account


The corresponding step definition might look like this:

    Given /^I am an "admin" user for the "test" account$/ do
      set_role("admin")
      set_account("test")
    end


But could also be defined as:

    Given /^I am an "([^"]*)" user for the "([^"]*)" account$/ do |role, account|
      set_role(role)
      set_account(account)
    end


The first definition doesn't receive any arguments because no regular expressions are defined; the second definition receives two arguments based on the two regular expressions defined.

## General Guidelines
#### Allow for different subjects, adjectives, and other grammar variations
Account for steps that could be written in slightly different ways, depending on the subject or action in the test.

* Prevents creating multiple definitions for the same step functionality
* Allows steps to maintain proper english without breaking tests

For example:

    Given I am an "admin" user
    Given I am a "support" user


can both be captured in one step definition:

    Given /^I am (a|an) "([^"]*)" user$/ do |role|
      # some code
    end


#### Do not call step definitions from within other step definitions
Nested step definitions can be confusing to navigate and hard to debug. Rather than calling steps within other steps, create helpers to contain actions that need to be available across step definitions.

* Makes finding code around specific actions easier to find
* Allows code affecting many tests to only have to be updated in one place