## Quiz Page Functionality

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

---
---

## Quiz Page Functionality

The quiz page presents a placeholder for a question fetched from the backend. Initially, only the front text of the card is visible, while the main text remains hidden until the user pushes the 'Show Card' button.

### User Interactions and Outcomes

| **User Action**                | **Expected Output**                                      | **Description**                                                                                          |
|--------------------------------|----------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| Select existing deck           | Quiz page launches with selected deck title in app bar    | Upon selecting an existing deck from the main page, the quiz page launches, displaying the deck title. |
| Select new difficulty rating  | Difficulty of the card updates                           | User can adjust card difficulty level with a button press, updating its rating in the database.         |
| Show card                      | Hidden text appears, revealing card's back                | User can reveal the back of the card by pressing the 'Show Card' button.                                 |
| Press 'Again' button           | Hidden text disappears, card reloads                     | Pressing the 'Again' button reloads the card, hiding the back text while retaining changes made.        |

### Dynamic Button Functionality

The functionality of the difficulty buttons adapts dynamically based on the user's journey to the quiz page:

- If the user lands on the page to view a single card, pressing 'Again' will re-display the card's front text.
- If the user arrived through a different path, such as selecting a deck or filtering cards by difficulty, pressing any difficulty button updates the card's difficulty field in the database, and the user is redirected back to the main deck viewer page.
- If a user navigates to the quiz page by selecting 'new' cards, pressing the difficulty buttons will cycle through all 'new' cards in the deck until reaching the end, then redirecting the user to the deck viewer.

This dynamic behavior ensures a seamless experience tailored to the user's interaction with the app.
