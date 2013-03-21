# Steps
These guidelines cover best practices for structuring Cucumber steps.

## Format
A Step is an individual action taken in a Scenario. Steps are defined using statements beginning with the Given/When/Then keywords.

**Given**  
Describes the initial state of the scenario being tested. It should not be used to perform any actions on the system.

This step captures both the act of being a user, and the act of signing in:
    
    Given I am a user that has signed in
    
    
It can be rewritten as:

    Given I am a user
    And I am signed in


**When**  
Describes an action taken by the user. It should describe what the user does, not what the system does. `When` statements are used in conjunction with `Then` statements to describe a cause and effect relationship between user actions and the system's responses. The `When` statement describes the cause in terms of the user's action.

This step assigns the action being taken to the page:
    
    When my profile page loads

It can be rewritten to capture the user's action instead:

    When I view my profile page


**Then**  
Describes an action taken by the system. It should describe what the system does, not what the user does. `When` statements are used in conjunction with `Then` statements to describe a cause and effect relationship between user actions and the system's responses. The `Then` statement describes the effect in terms of the system.

This step assigns the action being taken to the user:
    
    Then I can view my profile picture

It can be rewritten to capture the system's action instead:

    Then my profile picture is displayed


The `And` and `But` keywords can also be used to add additional conditions to a Given/When/Then statement or make it more clear.

    Given I am a user
    And I am logged in
    When I view my profile page
    And I have a picture uploaded
    But do not have a nickname set
    Then my picture is displayed
    And a nickname is not.


## General Guidelines
#### Describe only one task per step
Avoid using conjunctions, such as "and," to connect and define multiple tasks in one step.

* Conjunctive steps are an anti-pattern
* Introducing multiple failure points in a single step makes debugging more difficult

#### Use consistent domain language across steps
Reference pages, views, and other app components using the same terminology in all places. For example, if "Home page" describes the page a user sees upon logging in, "Home page" should be the term used in all tests that specific page is referenced. Do not call it the "Home page" in one test and the "Landing page" in another.

* Reduces confusion among step descriptions across features
* Keeps technical and non-technical members of the team on the same page

#### Use descriptive steps
Steps should describe how the application progresses, not how it is implemented. `Then I log in` is a good step, `Then I click the login button` is not.

* Decouples functionality from user interface elements
* Prevents steps from having to be rewritten when user experience changes, but functionality does not

#### Do not use any kind of code or data structures in step descriptions
Steps should be written in plain text, without any implementation references.

* Provides readability across a variety of audiences, technical and non-technical alike
* Prevents steps from having to be rewritten when implementation details change
