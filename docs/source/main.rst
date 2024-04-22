.. _main:
:ref:`index <index>`

*************
The Main page
*************

.. meta::
    :description: Detailed description of the main page of our software.
    :keywords: Scope, Project

Once a user has logged in the system they are directed to the main page.
Here a user can :

    *   Create/Edit/Delete their own Deck
        *   :ref:`createUserDeck <createUserDeck>`
        *   :ref:`deleteUserDeck <deleteUserDeck>`
        *   :ref:`updateUserDeck <updateUserDeck>`

    *   Create/Edit/Delete their own flashcards, located in their decks
        *   :ref:`createUserCard <createUserCard>`
        *   :ref:`deleteUserCard <deleteUserCard>`
        *   :ref:`updateUserCard <updateUserCard>`

    *   Browse threw their own cards and decks
        *   :ref:`findDeckIdByTitle <findDeckIdByTitle>`
        *   :ref:`findCardIdByTitle <findCardIdByTitle>`

    *   Take multiple different quizzes on their cards
         *   :ref:`quiz <quiz>`

    *   Rate their cards based on difficulty(Easy, Medium, Hard)
    
==========
User Decks
==========

Create a Deck
-------------

Function triggered by a 'Create' Button

.. _createUserDeck:

.. code-block:: dart

    Future<void> _createUserDeck(String? userId, String title) async {
      try {
        // Check if the deck title already exists for the user
        bool isDuplicate = await _validateDeck(userId, title);

        if (!isDuplicate) {
          print('Error: Deck with title "$title" already exists for the user.');
        } else {
          // Create a new deck with a unique ID under the user's decks collection
          DocumentReference deckReference = await _usersCollection
              .doc(userId)
              .collection('decks')
              .add({
            'title': title,
            // You can add more fields here if needed
          });

          print('User Deck created with ID: ${deckReference.id}');
        }
      } catch (e) {
        print('Error creating user deck: $e');
      }
    }

Delete User Deck 
----------------

Function triggered by a 'Delete' Button

.. _deleteUserDeck:

.. code-block:: dart

    Future<void> _deleteUserDeck(String? userId, String deckId) async {
      try {
        // Delete the deck from Firestore
        await _usersCollection
            .doc(userId)
            .collection('decks')
            .doc(deckId)
            .delete();

        print('Deck deleted successfully');
      } catch (e) {
        print('Error deleting deck: $e');
      }
    }

Edit User Deck(Title)
---------------------

Function triggered by a 'Edit' Button

.. _updateUserDeck:

.. code-block:: dart

    Future<void> _updateDeck(String? userId, String deckId, String newTitle) async {
      try {
        // Check for duplicate title
        bool isDuplicate = await _validateDeck(userId, newTitle);

        if (!isDuplicate) {
          print('Error: Deck with title "$newTitle" already exists for the user.');
        } else {
          // Update the deck's title in Firestore
          await _usersCollection
              .doc(userId)
              .collection('decks')
              .doc(deckId)
              .update({
            'title': newTitle,
            // You can add more fields to update if needed
          });

          print('Deck title updated successfully');
        }
      } catch (e) {
        print('Error updating deck title: $e');
      }
    }


==========
User Cards
==========

Create User Card Method
------------------------

Function triggered by a 'Create' Button

.. _createUserCard:

.. code-block:: dart

    Future<void> _createUserCard(String? userId, String deckId, String cardTitle, String frontText, String backText, String difficulty) async {
      try {
        // Add a new card with a unique ID to the specified user's deck
        DocumentReference cardReference = await _usersCollection
            .doc(userId)
            .collection('decks')
            .doc(deckId)
            .collection('cards')
            .add({
          'title': cardTitle,
          'frontText': frontText,
          'backText': backText,
          'difficulty': difficulty
          // You can add more fields here if needed
        });

        print('Card added to User Deck with ID: ${cardReference.id}');
      } catch (e) {
        print('Error adding card title: $e');
        return null;
      }
    }

Delete User Card
----------------

Function triggered by a 'Delete' Button

.. _deleteUserCard:

.. code-block:: dart

    Future<void> _deleteUserCard(String? userId, String deckId, String cardId) async {
      try {
        // Delete the card from Firestore
        await _usersCollection
            .doc(userId)
            .collection('decks')
            .doc(deckId)
            .collection('cards')
            .doc(cardId)
            .delete();

        print('Card deleted successfully');
      } catch (e) {
        print('Error deleting card: $e');
      }
    }


Edit User Card
---------------

Function triggered by a 'Edit' Button

.. _updateUserCard:

.. code-block:: dart

    Future<void> _updateUserCard(
        String? userId,
        String deckId,
        String cardId,
        String newCardTitle,
        String newFrontText,
        String newBackText,
        String newDifficulty,
        ) async {
      try {
        // Update the card in Firestore
        await _usersCollection
            .doc(userId)
            .collection('decks')
            .doc(deckId)
            .collection('cards')
            .doc(cardId)
            .update({
          'title': newCardTitle,
          'frontText': newFrontText,
          'backText': newBackText,
          'difficulty': newDifficulty
          // You can add more fields to update if needed
        });

        print('Card updated successfully');
      } catch (e) {
        print('Error updating card: $e');
      }
    }

========
Browsing 
========

User Deck
---------

.. _findDeckIdByTitle:

.. code-block:: dart

    Future<String?> _findDeckIdByTitle(String? userId, String titleToFind) async {
      try {
        // Convert the target title to uppercase
        String uppercaseTitleToFind = titleToFind.toUpperCase();

        // Get all decks for the user from Firestore
        QuerySnapshot<Map<String, dynamic>> querySnapshot = await _usersCollection
            .doc(userId)
            .collection('decks')
            .get();

        // Iterate through each deck and check for a matching title (case-insensitive)
        for (QueryDocumentSnapshot<Map<String, dynamic>> deckSnapshot in querySnapshot.docs) {
          Map<String, dynamic> deckData = deckSnapshot.data();
          String deckTitle = (deckData['title'] ?? '').toUpperCase();

          // Compare the uppercase titles
          if (deckTitle == uppercaseTitleToFind) {
            // Return the deck ID if titles match
            return deckSnapshot.id;
          }
        }

        // Return null if no matching title is found
        return null;
      } catch (e) {
        print('Error finding deck ID by title: $e');
        return null;
      }
    }


User Card
---------

.. _findCardIdByTitle:

.. code-block:: dart

    Future<String?> _findCardIdByTitle(String? userId, String deckId, String cardTitleToFind) async {
      try {
        // Convert the target card title to uppercase
        String uppercaseCardTitleToFind = cardTitleToFind.toUpperCase();

        // Get all cards for the specified deck from Firestore
        QuerySnapshot<Map<String, dynamic>> querySnapshot = await _usersCollection
            .doc(userId)
            .collection('decks')
            .doc(deckId)
            .collection('cards')
            .get();

        // Iterate through each card and check for a matching title (case-insensitive)
        for (QueryDocumentSnapshot<Map<String, dynamic>> cardSnapshot in querySnapshot.docs) {
          Map<String, dynamic> cardData = cardSnapshot.data();
          String cardTitle = (cardData['title'] ?? '').toUpperCase();

          // Compare the uppercase titles
          if (cardTitle == uppercaseCardTitleToFind) {
            // Return the card ID if titles match
            return cardSnapshot.id;
          }
        }

        // Return null if no matching title is found
        return null;
      } catch (e) {
        print('Error finding card ID by title: $e');
        return null;
      }
    }

