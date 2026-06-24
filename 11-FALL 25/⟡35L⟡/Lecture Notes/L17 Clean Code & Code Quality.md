## Information Hiding, Separation of Concerns, SOLID
### Information Hiding vs. SoC
- Use of **modular decomposition** to reduce complexity
- IH - more concrete, tells you which concerns should be separated, and tells you to *hide the implementation of concerns* from *other modules
- SoC - more abstract, only tells you to separate concerns
### Information Hiding vs. SOLID
- Use of **hiding details** to reduce complexity
- SOLID is a set of *concrete steps/rules*, applies to object-oriented programming languages
- IH is more abstract and applies to all programming languages

## Code Comprehension Approaches
### Bottom-up (novices)
- Read line by line, grouping statements into logical chunks
- Takes more time because each statement needs to be analyzed
### Top-down (experts)
- Driven by a hypothesis of what the code does
- Look for *key lines of code* that reveal the core purpose
- Get the big picture then look for details

# Clean Code
### Four pillars:
1. Meaningful naming
2. Simplified structure
3. Purposeful documentation
4. Defensive programming

## 1. Meaningful naming
- Meaningless names are better than misleading names
- Choose commonly used names to follow conventions
- Shorter, abbreviated names are better (unless it compromises meaning)
### Common conventions
- Class names should be **nouns**
- Method names should be **verbs**
- Each programming language has different style conventions

## 2. Simplified structure
Focus on minimizing **cognitive load**
- Reduce **nesting level**
- Use **guard clauses**
	- Exit the function early after checking and handling an **edge case**
- Use **chunks** to support meaningful abstractions
	- Limit function size
	- Extract methods, even if a block of code is only used once
	- Abstractions should not require developers to look inside the function to understand what it does

## 3. Purposeful documentation
- Comments focus on **intent** and **non-obvious details** instead of repeating what the code does
	- Document the purpose of the code, why it was written this way
- Refactor code to express intent

## 4. Defensive programming
### Design by contract
Each function defines:
- **Pre-conditions**: assumptions on inputs
- **Post-conditions**: guarantees on output
These make up the visible contract of the module, and the implementation is then hidden.
- **Assertions** make assumptions explicit

Before refactoring, make sure you have good tests