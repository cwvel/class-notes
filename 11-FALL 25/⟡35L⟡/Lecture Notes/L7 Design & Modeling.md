## Different views visualize different aspects of software
![Pasted image 20251207180507](Pasted%20image%2020251207180507.png)


## Class diagrams visualize the code view
![Pasted image 20251207180607](Pasted%20image%2020251207180607.png)
- **Visibility**: (+) = public, (-) = private

### Associations
![Pasted image 20251207180654](Pasted%20image%2020251207180654.png)
![Pasted image 20251207180702](Pasted%20image%2020251207180702.png)
- **Navigable**
	- Employee - Boss
	- Vote - Politician
- **Aggregation**
	- Car *HAS-A* Wheel
	- Library *HAS-A* Book
- **Composition**
	- Person *HAS-A* (needs) a Head
	- House *HAS-A* (needs) a Room

## Entity-Relation Diagrams (ERDs) visualize data view
![Pasted image 20251207180920](Pasted%20image%2020251207180920.png)

## Component Diagrams visualize runtime view
- **Components** are independently deployable runtime units (e.g. processes)
- Components execute over a prolonged period (not just a function that instantly returns, nor packages of code)
![Pasted image 20251207181020](Pasted%20image%2020251207181020.png)

## Sequence Diagrams visualize behavioral view
- Show examples of interactions between objects and component instances
![Pasted image 20251207181104](Pasted%20image%2020251207181104.png)
- Support **fragments** to show multiple execution paths
	- **Alt** (book found, else)
		- Executes exactly one of the cases based on conditions
	- **Loop** (for each book)
		- Loop gets executed as long as condition is true
	- **Opt** (login successful)
		- Only executed if conditions are true

## State Machine Diagrams visualize behavioral view
![Pasted image 20251207181232](Pasted%20image%2020251207181232.png)

# SOLID design principles
## Single Responsibility Principle
- A class should have only one reason to change: it should have a **single, well-defined responsibility**
	- Changes to one responsibility won't impact unrelated parts of the system

## Open-Closed Principle
- A module should be **open for extension** but **closed for modification**
	- Extensions: subclassing, adding behavior
	- Modifications: large changes of source code

## Liskov Substitution Principle
- Subclasses should be **substitutable** for their superclasses without breaking the application's correctness

## Interface Segregation Principle
- A client module should not be forced to depend on methods it does not use
	- SRP for interfaces
- Split up larger interfaces into smaller coherent interfaces

## Dependency Inversion Principle (DIP)
- High-level (abstract) modules should not depend on low-level (concrete) modules
	- Both should depend on abstractions