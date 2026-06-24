## Benefits of Reuse
* **Speeds up** software development
* Reused software is **tried and tested** and should be more **dependable**

### Vision vs. Reality
- Create new software by composing existing building blocks: Well-organized libraries of modules that are **highly compatible** with each other
- However in reality, modules are **partially incompatible** but often still glued together

## Internal vs. External Reuse
- **Internal Reuse**
	- Code written by the same developer/team
- **External Reuse**
	- Code written by a third party

## Designing with External Reuse
### Design Principle: Keep Versions of Dependencies Fixed
- Package managers allow you to **specify** and install **specific versions** of packages in a virtual environment
	- `pipenv`

### Design Principle: Update dependencies to receive bug fixes and security patches
- Reuse **well-maintained** and **popular** modules
	- Often fixed quickly
- Regularly check for security patches and bug fixes, but also be aware of the side effects of updates

### Design Principle: Strive for fewer package dependencies
- Avoid reusing **trivial code** (e.g. `left-pad` story)
- Package dependencies can become a **security vulnerability**

### Cost-Benefit Analysis for External Reuse
Balance **effort to *adapt* the reusable module**
- Integration effort
- Finding module
- Limited changeability

...with **effort saved by *reusing* the module**
- Implementation and testing effort

## Designing with Internal Reuse
### Design Principle: Identify violated assumptions
- Software that worked in one context might not work in another context (ex. NASA Ariane 5 failure)
- Identify **assumptions** made by a reuse candidate and check that the reusable software will operate reliably under these **new conditions**
	- Test it!

### Cost-Benefit Analysis for Internal Reuse
Balance **effort to adapt the reusuable module**
- Identification of implicit assumptions
...with **effort saved by reusing the module**
- Implementation and testing effort

## Library vs. Framework
### Library
- Your code makes calls to the library API to use their functions
### Framework
- Your code defines **callbacks** to be called later by the framework
- **"Hollywood Principle" of Inversion of Control**: "Don't call us, we'll call you"
- Makes more decisions for you and provides **less flexibility**, but also *hides a lot of complexity* and you can write less code
- Decisions to use a framework are often harder to *reverse*

## Design Decisions
#### Think of many design alternatives
- 5 design options > 3 design options > 1 detailed design option
- **Idea generation**: think broadly about a **diverse range of solutions**
- **Evaluation**: Narrow down on ideas

#### Delaying decisions
- Identify design decisions that need more information or may change later
- Track a list of **delayed decisions**

#### Solve simpler problems first
- Solution to a simpler problem may be incomplete but can be extended later

### Rational Decision Making Process
1. **Identify** your requirements. What is important?
2. Think of many design **alternatives**.
3. **Evaluate** how well your alternatives implement the requirements from Step 1.
4. Consider the trade-offs and make a decision.

### "Design Docs"
Unstructured text
Consists of:
- **Context and scope** relevant for understanding the design doc
- **Goals and non-goals** define scope: requirements vs. what can be ignored
- **Design**: models and design descriptions to describe a solution
- **Alternatives** and trade-offs that motivate the decision