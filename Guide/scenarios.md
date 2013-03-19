# Scenarios
These guidelines cover best practices for structuring Cucumber scenarios.

## Format
Scenarios describe the acceptance criteria for a given feature. They are defined using a series of Given/When/Then statements.

The first line of a scenario starts with the `Scenario` keyword, followed by a brief description of the scenario to be tested. It is followed by a series of Given/When/Then/And statements that describe what should happen in the scenario for it to be considered "passing."

See the example below; the feature definition is included to provide context.

    Feature: Select subscription level
      As a customer
      I want to be able to select a subscription level
      so that I can purchase it
      
    Scenario: I am not subscribed
    	Given I do not have a subscription
    	When I select a subscription
    	And provide payment
    	Then I should be subscribed


#### Use Background to set up scenarios
The background scenario is run before each individual scenario in the feature file. It is a special type of scenario used to prepare the environment for the scenarios to be run. Rather than copying setup steps on a per-scenario basis, pull common steps applicable to all scenarios into the background.

#### Use Scenario Outline to define functionality with multiple data points
Scenario Outlines allow one feature to be defined, but tested using multiple data points. The functionality behind the feature doesn't change, but expected outcomes vary depending on the given inputs.

* Keep scenarios DRY
* Allow new data points to be added as needed

The following scenario would be run once for each row in the example table. 

    Scenario Outline: A user sees the dashboard upon login
    	Given I am a <role>
    	And I log into the site
    	Then I should see the <view> page
    	
    	Examples:
    	| role				| view				|
    	| user				| dashboard			|
    	| support_person	| support dashboard	|
    	| administrator		| admin dashboard	|


## General Guidelines
#### Describe *what* a user should be able to do, not *how* they should do it
Keep a higher level of abstraction when writing scenarios.

* Decouples functionality from user interface elements
* Prevents scenarios from having to be rewritten when user experience changes, but functionality does not

Compare this scenario:

    Scenario: I am not subscribed
    	Given I do not have a subscription
    	When I select a subscription
    	And provide payment
    	Then I should be subscribed


to this one:

    Scenario: I am not subscribed
    	Given I do not have a subscription
    	When I view the subscription page
    	And I select a "basic" subscription
    	And I select "pay with credit card"
    	And I enter my credit card number
    	And I enter my credit card expiration
    	And I submit my payment information
    	Then I should see a confirmation of my purchase

They both test the same outcome (a user subscribes), but the first scenario can be implemented in multiple ways without needing to change the description. The second scenario is more tightly coupled to the user interface, and would need to be rewritten if any of the expected elements were changed or removed.

#### Keep scenarios independent of one another
Scenarios should run the same way, and have the same outcomes, regardless of the order in which the test suite is run. One scenario should not be used to set up another.

## Tags
#### Tag scenarios that require the browser with @javascript
Scenarios must be tagged with `@javascript` to invoke the browser.

#### Tag 'work in progress' scenarios with @wip
Tagging with `@wip` prevents a given scenario from being run with the test suite.

* Prevent unexpected failures due to incomplete scenarios or test definitions
* Don't waste time running a test that will not work