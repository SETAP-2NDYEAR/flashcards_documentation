.. _login:

**********************
The Login/Sign Up Page
**********************

.. meta::
    :description: Detailed description of the login page of our software.
    :keywords: Login, Page

The Login page is the first interaction a user has with the software.
It is the access portal to the site.


New Users
=========

A new user has to sign up , providing a valid email and password.
If the provided email is not in the right format[xxxxx@xxxxx.xxx] , the system will display an error : “Error”.
if the provided email has already been used , the system will display an error : “Error”.
There are no restrictions to the password format.

Once registration and authentication is completed for a new user.
The user details are added to the Firebase database and a new set of default flashcards are created.

.. _registerUser:

.. code-block:: dart

    Future<void> _registerUser() async {
    AuthenticationBackend authBackend = AuthenticationBackend();
    await authBackend.registerUser(
      emailController.text,
      passwordController.text,
      displayNameController.text,
    );
  }

.. _registerUserAuth:

.. code-block:: dart

    Future<void> registerUser(String email, String password, String displayName) async {
    try {
      // Create user in Firebase Authentication
      await _auth.createUserWithEmailAndPassword(email: email, password: password);

      // Get the current user
      User? user = _auth.currentUser;

      // Update user profile with display name
      await user?.updateProfile(displayName: displayName);

      // Add user to Firestore
      await _addUserToFirestore(user?.uid, displayName);

      // Automatically creates a deck in a new users account called misc
      await _createUserDeck( user?.uid, 'misc');

      // Used to test adding a card to a deck
      String? tempDeckId = await _findDeckIdByTitle(user?.uid, 'misc');


      if (tempDeckId != null) {
        await _createUserCard(user?.uid, tempDeckId, 'cardTitle', 'frontText', 'backText', 'NEW');
        await _createUserCard(user?.uid, tempDeckId, 'cardTitle', 'frontText', 'backText', 'NEW');
      } else {
        print('Deck not found with the specified title.');
      }

      await getCardCountByDifficulty(user?.uid, tempDeckId, 'HARD');

      print('Registration successful');
    } catch (e) {
      print('Error: $e');
    }

  }

Existing Users
==============

Login
-----

An existing user can sign in , providing their valid email and password .
If the provided email is not in the right format [xxxxx@xxxxx.xxx] , the system will display an error : “Error”.
If the provided password is incorrect , the system will display an error: “Error”.
If the user cannot provide their existing password ,they can opt for the “Forgot Password?” Button ,where they will be asked to provide their email and then they will finally be able to retrieve their password.
However, that is a requirement the software has yet to meet.


.. _loginUser:

.. code-block:: dart

     Future<void> _loginUser() async {
    AuthenticationBackend authBackend = AuthenticationBackend();
    await authBackend.loginUser(
      emailController.text,
      passwordController.text,
    );
  }
}

.. _loginUserAuth:

.. code-block:: dart

    Future<void> loginUser(String email, String password) async {
    try {
      // Sign in the user using provided email and password
      await _auth.signInWithEmailAndPassword(email: email, password: password);
      print('Login successful'); // add navigation to correct page here
    } catch (e) {
      print('Error: $e');
    }
  }

Logout
------

An existing user can log out of the system.
The system will then print out a message : "User logged out successfully".
For any exceptions , the system will print out an error message.

.. _logoutUser:

.. code-block:: dart

    Future<void> _loginUser() async {
    AuthenticationBackend authBackend = AuthenticationBackend();
    await authBackend.loginUser(
      emailController.text,
      passwordController.text,
    );
  }

.. _logoutUser:

.. code-block:: dart

    Future<void> _logoutUser() async {
    try {
      await _auth.signOut();
      print('User logged out successfully');
    } catch (e) {
      print('Error logging out user: $e');
    }
  }


Code Breakdown
==============

Registration and Login Functions
--------------------------------
The `AuthenticationPage` allows users to register or login using their email and password.

- The "Register" button triggers the `_registerUser` function, which registers a new user by creating an account in Firebase Authentication and adding their information to Firestore.
- The "Login" button triggers the `_loginUser` function, which logs in an existing user using their email and password.
- The "Logout" button triggers the `_logoutUser` function, which logs out an existing user using their email and password.

:ref:`registerUser <registerUser>`
:ref:`loginUser <loginUser>`
:ref:`logoutUser <logoutUser>`

.. code-block:: dart

    Future<void> _registerUser() async {
      // Function to register a new user
    }

    Future<void> _logoutUser() async {
      // Function to log out of a user
    }

    Future<void> _loginUser() async {
      // Function to log in a user
    }

AuthenticationBackend Class
----------------------------

:ref:`registerUserAuth <registerUserAuth>`
:ref:`loginUserAuth <loginUserAuth>`
:ref:`logoutUserAuth <logouUserAuth>`

.. code-block:: dart

    class AuthenticationBackend {
      final FirebaseAuth _auth = FirebaseAuth.instance;
      final CollectionReference _usersCollection = FirebaseFirestore.instance.collection('users');

      // Register and login functions

      // Function to log out user
      Future<void> _logoutUser() async {
      }

      // Function to add user information to Firestore
      Future<void> _addUserToFirestore(String? userId, String displayName) async {
        // Function to add user information to Firestore
      }
    }
