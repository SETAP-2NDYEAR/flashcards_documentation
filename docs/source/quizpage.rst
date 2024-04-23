

The quiz page emerges with a placeholder for a question fetched from the backend. Positioned at the top of the page, this placeholder
text sets the stage for interaction. Below, at the page's bottom, rests the 'Show Card' button and an 'Edit' button.
Upon clicking the 'Show Card' button, the answer to the question is revealed, centered on the page. Following this reveal, four 
buttons appear horizontally, occupying the same space. These buttons are labeled 'Again', 'Hard', 'Good', and 'Easy'.
Understanding the functionality of these buttons hinges on the user's journey to the quiz page. For instance, if a user lands 
on the page to view a single card, pressing 'Again' will re-display the card's front text. Alternatively, if the user arrived through 
a different path, such as selecting a deck or filtering cards by difficulty, pressing any difficulty button updates the card's difficulty 
field in the database. Subsequently, the user is redirected back to the main deck viewer page.
Consider a scenario where a user navigates to the quiz page by selecting 'new' cards. In this case, pressing the difficulty buttons will 
cycle through all 'new' cards in the deck until reaching the end. Then, the user is redirected to the deck viewer.
Thus, the functionality of the difficulty buttons adapts dynamically, providing a seamless experience tailored to the user's interaction with the app.
