# Immutable Passport Integration Guide

In this guide, we will walk you through the process of integrating Immutable Passport into your application. Immutable Passport is a secure and easy way to manage user authentication and transactions on the Immutable X marketplace. 

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Getting Started](#getting-started)
   1. [Create a Simple Application](#create-a-simple-application)
   2. [Register the Application](#register-the-application)
   3. [Initialize Passport Client](#initialize-passport-client)
3. [User Authentication](#user-authentication)
   1. [Logging In a User](#logging-in-a-user)
   2. [Displaying User Information](#displaying-user-information)
   3. [Logging Out a User](#logging-out-a-user)
4. [Initiating a Transaction](#initiating-a-transaction)

## Prerequisites

Before you begin, make sure you have the following:

- Node.js installed on your machine.
- A basic understanding of JavaScript and web development.

## Getting Started

### Create a Simple Application

For this guide, we will use a simple Node.js application as an example. You can create a new project or clone a repository that includes a basic structure.

```bash
# Clone a sample app repository
git clone https://github.com/your-username/immutable-passport-sample
cd immutable-passport-sample
```

### Register the Application
To integrate Immutable Passport, you need to register your application on the Immutable Developer Hub. This step involves creating an application and obtaining API keys. Follow the official documentation to complete this process: Immutable Developer Hub.

### Initialize Passport Client
In your application, install the immutable-passport package using npm or yarn.

```bash
npm install immutable-passport
```

In your app's JavaScript file, initialize the Passport client using your API keys.

```javascript
const { Passport } = require('immutable-passport');

const passport = new Passport({
  apiKey: 'YOUR_API_KEY',
  apiSecret: 'YOUR_API_SECRET',
});
```

## User Authentication
### Logging In a User
You can use Passport to initiate the login process for your users. Here's a simple example using Express.js:

```javascript
app.get('/login', (req, res) => {
  // Redirect the user to the Immutable Passport login page
  const loginURL = passport.getLoginURL();
  res.redirect(loginURL);
});
```

### Displaying User Information
After successful login, you can obtain the ID token, access token, and user's nickname from the Passport client.

```javascript
app.get('/callback', async (req, res) => {
  const { code } = req.query;

  // Exchange the code for tokens
  const tokens = await passport.exchangeCode(code);

  // Access user information
  const { idToken, accessToken, nickname } = tokens;

  res.json({ idToken, accessToken, nickname });
});
```

### Logging Out a User
To log out a user, simply clear their session or tokens.

```javascript
app.get('/logout', (req, res) => {
  // Clear user session or tokens
  // Redirect to a logged-out page
});
```

## Initiating a Transaction
You can use Passport to initiate transactions on the Immutable X marketplace. Here's an example:

```javascript
const transactionHash = await passport.createTransaction({
  to: 'recipient-address',
  tokenId: 'token-id',
  quantity: 1,
  note: 'This is a test transaction.',
});
```

This initiates a transaction and returns the transaction hash, which can be used to track the transaction's status.

That's it! You've successfully integrated Immutable Passport into your application. You can now manage user authentication and transactions securely.

For a complete example, you can check out the Immutable Passport Sample App.

If you have any questions or need further assistance, refer to the Immutable Passport Documentation.

Happy coding!
