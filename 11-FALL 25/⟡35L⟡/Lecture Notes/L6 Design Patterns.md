# Design patterns
## Principle of separation of concerns
- Systems should be divided into distinct sections, each addressing a separate, specific purpose
	- Makes the system easier to develop and evolve
	- Parts can be changed independently (good for teamwork)
- **Presentation layer** displays information to the user and collects input
	- Ex. UI
	- Makes calls into the application layer
	- Should always check the validity of user input to ensure it doesn't corrupt the state
- **Application layer** implements domain logic and behavior
	- Should not know there is a UI

## Design patterns
- A common, acceptable solution to a recurring problem in a specific context

### Observer design pattern
- How does the frontend know the state of the backend has changed?
	- Application layer allows presentation layer to register a *callback* e.g. `onBalanceChanged`
	- Presentation layer knows there is a change, so it knows to use a getter from the application layer e.g. `getCurrentBalance()`
	- The presentation layer forwards user events to the application layer
- **Backend (subject/observable)**: keeps track of the **internal state** and keeps a list of **registered observers**
	- *Notifies* all observers (calls `update(event)` for each observer) when the state changes
- **Frontend (observer/presentation layer)**:
	- Abstract class `AbstractObserver` with an `update(Event)` method
		- With concrete implementations that implements `update(Event)`

### Model view controller (MVC)
Note: MVC is a specific version of the observer design pattern. The model is the subject and the view is the observer, and the controller helps implement the update
- **Model:**
    - provides core functionality
    - registers views and controllers
    - notifies components about data changes
- **View**:
    - displays information to user
    - creates controller
    - retrieves data from model
    - implements update
- **Controller**:
    - accepts user input
    - acts as bridge between model and view
