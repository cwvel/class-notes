## Software Testing
#### Goals
**Reveal bugs** so they can be fixed
*testing can prove the existence of bugs, not their absence*
**Document** what the code should do
*if you're not sure what the code should do, you can look at its tests*

#### Pytest
- A common testing framework in python
- Calls all functions starting with `test` in the `/tests` folder of the project

#### Continuous Integration Workflow
- A development practice where you frequently merge changes into the main branch
- Only push changes that should pass the tests

#### Verification and Validation
- **Verification:** Did we build the system right?
	- Can often be automated, e.g. *automated program repair*
- **Validation:** Did we build the right system?
	- Must be done manually by someone who *represents real users*

## Test-Driven Development (TDD)
Puts **testing** before **development**

#### TDD Workflow
1. **Red**: For your new requirement write a *small test* that fails, and perhaps doesn’t even compile at first
2. **Green**: Make the test pass with *minimal coding effort*, potentially using simplifying shortcuts in the process
3. **Refactor**: Make the design more elegant, cleaner, and potentially faster while *not changing the functionality of the program*

#### Refactoring
- Reduces accidental complexity and makes code easier to read/understand
- Common themes:
	- Avoid code duplication by creating **abstractions**
	- Remove dead code & improve **documentation**
	- Replace conditional logic with **polymorphism**
	- Improve **naming** of classes, functions, & variables

#### Rules of TDD
- Do not write a line of production code until you have a failing unit test
- Do not write more of a unit test than is sufficient for the test to fail
- Do not write more production code than is sufficient to pass the tests

#### Limitations of TDD
TDD doesn't work well for:
- complex behavior where the solution is not an **incremental improvement to simpler problems** *e.g. we can't keep building taller towers to reach the moon*
- systems with **non-binary success outcomes** *e.g. image processing*
- testing **non-functional properties** *e.g. response time*

### Integration Testing
Unit tests aren't always enough: components that work well in isolation might break once composed together
#### Levels of software tests:
1. **UNIT TESTING**: Tests individually testable units of an application (e.g., functions, classes, components) in isolation
2. **INTEGRATION TESTING**: Tests whether different components, modules, or services work together correctly
3. **SYSTEM TESTING (END-TO-END TESTING)**: Tests whether the complete application from user input to output works correctly

## Indirect Inputs and Outputs
![Pasted image 20251124010137](../../Pasted%20images/Pasted%20image%2020251124010137.png)

### Test Doubles
#### Mock object
Replaces the DOC and only verifies the indirect outputs from the system
#### Test spy
Replaces the DOC, collects the indirect outputs and forwards them directly to the test, instead of outputting to the system
#### Test stub
Replaces the DOC and simulates its behavior, taking in output from the system and sending the desired inputs to the system
