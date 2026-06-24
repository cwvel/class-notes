### Information Hiding Principle
- Each module is designed to hide its internal **design decisions** from external users
- Increases flexibility and supports changeability
#### Modules should have **fixed interfaces** to allow for variations in implementation
- Module's **interface** is what is visible
	- Stable contract that describes what the module does
- Module's **implementation** is hidden
	- How the module fulfills the contract
	- Can be changed freely without affecting the rest of the system as long as the interface remains the same
	- *ex.* Data structures and formats, algorithms and logic, dependencies on libraries/frameworks
#### Deep vs. Shallow modules
![Pasted image 20251203000803](Pasted%20image%2020251203000803.png)

#### Coupling and cohesion
- **Coupling**: Dependencies **between** modules
	- High coupling: changes in one module ripple through the entire system
	- Low coupling: Changes are localized and modules are independent
- **Cohesion**: Dependencies **within** modules
![Pasted image 20251203000934](Pasted%20image%2020251203000934.png)

#### Dependencies
- **Syntactic dependencies:** A cannot be compiled/interpreted without B
-  **Semantic dependencies:** A does not function properly without B, or a change in B also requires a change in A
	- Harder to identify

### Modularity
- A **modular design** method produces systems of **loosely coupled, coherent, understandable** components
#### Single choice principle
- Don't repeat yourself
- When a system must support a set of alternatives, **one and only one** module should know the exhaustive list
	- e.g. Which payment methods are supported
	- When adding a new alternative, only one module needs to change

### Change Impact Analysis
Evaluates whether a design follows the IHP
- List all changes that could reasonably happen in the future
	- Prioritize the likelihood of these changes
- Evaluate the effort to make each change
- Redesign the system until you do not have any changes that are **highly likely AND have a high effort of change**
