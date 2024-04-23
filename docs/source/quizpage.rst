### Quiz Page Functionality ###

1. **Initial Page Layout**:
   - The quiz page displays a placeholder for a question fetched from the backend, positioned at the top of the page.
   - This placeholder text serves as the focal point for user interaction.

2. **Buttons Placement**:
   - Positioned at the bottom of the page are the 'Show Card' button and an 'Edit' button, allowing for further actions.

3. **Revealing Answer**:
   - Upon clicking the 'Show Card' button, the answer to the question is revealed, presented at the center of the page.
   
4. **Difficulty Buttons**:
   - After revealing the answer, four buttons labeled 'Again', 'Hard', 'Good', and 'Easy' appear horizontally, occupying the same space.

5. **Button Functionality**:
   - The functionality of these buttons varies based on the user's journey to the quiz page.
   - If a user arrives to view a single card, pressing 'Again' will re-display the card's front text.
   - For users arriving through different paths, such as selecting a deck or filtering cards by difficulty, pressing any difficulty button updates the card's difficulty field in the database.
   - Subsequently, the user is redirected back to the main deck viewer page.

6. **Dynamic Adaptation**:
   - Consider a scenario where a user navigates to the quiz page by selecting 'new' cards.
   - In this case, pressing the difficulty buttons will cycle through all 'new' cards in the deck until reaching the end.
   - After completion, the user is seamlessly redirected to the deck viewer.
   
By dynamically adapting to the user's interaction with the app, the functionality of the difficulty buttons ensures a tailored and intuitive experience.
