# Amplify and Cognito

## Getting started

- The Amplify Auth category provides an interface for authenticating a user.

## Goal

To setup and configure your application with Amplify Auth and go through a simple api to check the current auth session

## Prerequisites

An Android application targeting at least Android SDK API level 16 with Amplify libraries integrated

## Configure Auth Category

1. run in the terminal : amplify add auth
2. Enter the following when prompted:
   ? Do you want to use the default authentication and security configuration?
   `Default configuration`
   ? How do you want users to be able to sign in?
   `Username`
   ? Do you want to configure advanced settings?
   `No, I am done.`

3. To push your changes to the cloud : amplify push
4. add this dependecies: implementation 'com.amplifyframework:aws-auth-cognito:1.24.0'to build.gradle

## Initialize Amplify Auth

6. added

```// Add this line, to include the Auth plugin.
Amplify.addPlugin(new AWSCognitoAuthPlugin());
Amplify.configure(getApplicationContext());
```

## Check the current auth session

7. For testing purposes, you can run this from your MainActivity's onCreate method.

```Amplify.Auth.fetchAuthSession(
    result -> Log.i("AmplifyQuickstart", result.toString()),
    error -> Log.e("AmplifyQuickstart", error.toString())
);
```

## Sign in

- The Auth category can be used to register a user, confirm attributes like email/phone, and sign in with optional multi-factor authentication.

## Register a user

- Invoke the following api to initiate a sign up flow.

```AuthSignUpOptions options = AuthSignUpOptions.builder()
    .userAttribute(AuthUserAttributeKey.email(), "my@email.com")
    .build();
Amplify.Auth.signUp("username", "Password123", options,
    result -> Log.i("AuthQuickStart", "Result: " + result.toString()),
    error -> Log.e("AuthQuickStart", "Sign up failed", error)
);
```

- The next step in the sign up flow is to confirm the user. A confirmation code will be sent to the email id provided during sign up.

```Amplify.Auth.confirmSignUp(
    "username",
    "the code you received via email",
    result -> Log.i("AuthQuickstart", result.isSignUpComplete() ? "Confirm signUp succeeded" : "Confirm sign up not complete"),
    error -> Log.e("AuthQuickstart", error.toString())
);
```

## Sign in a user

- Implement a UI to get the username and password from the user.by calling this method:

```Amplify.Auth.signIn(
    "username",
    "password",
    result -> Log.i("AuthQuickstart", result.isSignInComplete() ? "Sign in succeeded" : "Sign in not complete"),
    error -> Log.e("AuthQuickstart", error.toString())
);
```
