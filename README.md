My Notes App (Svelte)

A simple notes application built with Svelte that supports adding, editing, deleting, and searching notes. It also supports dark mode.

How to Run the App:
1. Clone the repository                                                                                                                                                                                              
 	bash                                                                                                                                                                                                         
	git clone https://github.com/yaswanth0091/Notes-App-Svelte.git                                                                                                                                               
	cd Notes-App-Svelte
2. Install dependencies
	bash                                                                                                                                                                                                         
	npm install
3. Start the development server
	bash                                                                                                                                                                                                         
	npm run dev
---------------------------------------------------------------------------------------------------------------------------------------
Features:
1. Add, edit, and delete notes
2. Search notes by title
3. Dark/light mode toggle
4. Confirm before deleting
5. Backend powered by MockAPI
--------------------------------------------------------------------------------------------------------------------------------------
Trade-offs & Assumptions
1. Used MockAPI for simulating a backend. In a real-world app, this would be replaced with an actual database and backend.
2. Notes do not persist offline or across browsers (since it uses an online API).
3. Minimal input validation for simplicity.
--------------------------------------------------------------------------------------------------------------------------------------
With More Time...
1. Add user authentication
2. Store notes offline using IndexedDB
3. Add tags or categories for notes
4. Support markdown content in notes
5. Implement unit and integration tests
-------------------------------------------------------------------------------------------------------------------------------------
Screenshots:
[Light Mode:](https://github.com/yaswanth0091/Notes-App-Svelte/blob/main/screenshots/light-mode.png?raw=true)                                                                                                        
[Dark Mode:](https://github.com/yaswanth0091/Notes-App-Svelte/blob/main/screenshots/dark-mode.png?raw=true)                                                                                                          
[Search-Bar-Functionality](https://github.com/yaswanth0091/Notes-App-Svelte/blob/main/screenshots/search-bar-functionality.png?raw=true)                                                                             
[Edit-Functionality](https://github.com/yaswanth0091/Notes-App-Svelte/blob/main/screenshots/edit-functionality.png?raw=true)                                                                                         
[Delete-Confirmation](https://github.com/yaswanth0091/Notes-App-Svelte/blob/main/screenshots/delete-confirmation.png?raw=true)                                                                                       
