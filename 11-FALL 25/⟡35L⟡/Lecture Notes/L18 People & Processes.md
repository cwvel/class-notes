## Waterfall model
- Big upfront design
- Each step completed entirely before the next:
	1. Requirements
	2. Design
	3. Development
	4. Testing
	5. Deployment
- Challenges:
	- Requirements might change during development
	- Feedback considered very late

## Agile manifesto
- Key idea: **iterative, incremental development**
- Get continuous feedback from customers to identify issues with the requirements
- **Sprints/iterations:** short time periods where a specific set of work (**feature backlog**) is completed and ready for review
	- After each sprint, collect feedback from customer, and write new user stories
- Values:
	- Working software over comprehensive documentation
	- Customer collaboration
	- Responding to change over following a strict plan

### Scrum Process
![Pasted image 20251207143843](Pasted%20image%2020251207143843.png)

### Planning poker
- Consensus-based technique for estimating effort/size of user stories by voting simultaneously and discussing differences
- Numbers represent "effort"

### Challenges of Agile
- Software is hard to change
- Improving quality attributes is hard
- Small **bus factor**

## Risk-Driven Design
- Identify biggest risks of the software and focus design on these risks
- Amount of risk involved determines **amount of upfront design**

### Risks
- Risks are decisions that are hard to change
- Examples:
	- Programming languages
	- Target platforms
	- Component architectures/connectors
	- Interfaces
	- Quality attributes
- Examples:
	- Online shops
		- Security, privacy, changeability
	- Games
		- Platforms, usability, performance
	- Medical software
		- Reliability, robustness, testability

### Risk storming
Collaborative risk identification technique
1. Model your software as diagrams
2. Identify risks on post-its, with colors representing priorities
3. Discuss risks and summarize

### Identify and mitigate highest-priority risks
- Make big design decisions early, defer small-scale decisions until later
- High cost of change $\Rightarrow$ **upfront** design
- Low cost of change $\Rightarrow$ **lean** design

## Agile projects
### Changeability
- Good architecture allows you to **defer decisions**, maximizing number of decisions not made

### Technical debt
- **Technical debt backlog**: issues that improve software design by refactoring and building abstractions
	- Technical debt results from short-term-oriented decisions that make future changes more costly or impractical
	- Examples:
		- Fixing code smells
		- Improving documentation
		- Architectural changes to support performance, scalability, etc.
- Integrating technical debt into Agile Processes
	- Have a special *architect* role who maintains the technical debt backlog
	- Include some technical debt issues in every sprint, or dedicating one sprint to reducing technical debt

# Human aspect
## Ivory tower
- Don't design in an "isolated ivory tower"
- "Ivory tower" architects are not involved in activities of software construction and ignore input from other developers
- Ivory tower designs only work in theory
- Software construction is a **collaborative activity**

## Rational vs. intuitive decision making
- Rational decision making uses **explicit knowledge**, uses logical reasoning to rank design options
- Intuitive decision making relies on a "gut feeling" (can use "implicit" knowledge and experience)
	- Faster, helps experts
	- Hard to communicate or justify
	- Prone to cognitive biases
- Should combine both processes:
	- Rational when justification is needed, well structured problems, or optimal decision is needed
	- Intuitive under time pressure, have experience, hard-to-define problem, "good-enough" is sufficient
- Designers often retroactively rationalize decisions

# Domain-specific needs
## Doghouse vs. Skyscraper
- Doghouses
	- Fewer people involved
	- Lower risk of failure
	- Short process of construction
	- Less upfront design and models
	- More **intuitive** decision making
- Skyscrapers
	- Many people involvoed
	- Long process
	- Higher risk of failure
	- More **rational** decision making
## Adapt the design process to the level of risk
- Social media apps vs. spacecraft software vs. startups
- Identify risks, amount of upfront design needed, type of decision making to rely on