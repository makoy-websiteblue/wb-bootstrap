# Ecme Database Structure

This document provides a comprehensive reference of the database schema for Ecme, detailing all tables, relationships, and constraints that form the data architecture of the system.

## next_auth Schema

The `next_auth` schema is designed to manage authentication and user sessions. It consists of the following tables:

## Tables

### 1. accounts

- **Description**: Stores information about user accounts linked to various providers.
- **Columns**:
    - `id` (uuid): Primary key, unique identifier for the account.
    - `type` (text): Type of account (e.g., OAuth).
    - `provider` (text): Name of the authentication provider (e.g., Google, Facebook).
    - `providerAccountId` (text): Unique identifier for the account from the provider.
    - `refresh_token` (text): Token used to refresh the session.
    - `access_token` (text): Token used to access the provider's API.
    - `expires_at` (bigint): Expiration time of the access token.
    - `token_type` (text): Type of the token.
    - `scope` (text): Scopes granted by the user.
    - `id_token` (text): ID token for the user.
    - `session_state` (text): State of the session.
    - `oauth_token_secret` (text): Secret for OAuth.
    - `oauth_token` (text): Token for OAuth.
    - `userId` (uuid): Foreign key referencing the `users` table.

### 2. sessions

- **Description**: Manages user sessions.
- **Columns**:
    - `id` (uuid): Primary key, unique identifier for the session.
    - `expires` (timestamp with time zone): Expiration time of the session.
    - `sessionToken` (text): Unique token for the session.
    - `userId` (uuid): Foreign key referencing the `users` table.

### 3. users

- **Description**: Stores user information.
- **Columns**:
    - `id` (uuid): Primary key, unique identifier for the user.
    - `name` (text): Name of the user.
    - `email` (text): Email address of the user.
    - `emailVerified` (timestamp with time zone): Time when the email was verified.
    - `image` (text): URL of the user's profile image.

### 4. verification_tokens

- **Description**: Stores tokens for email verification.
- **Columns**:
    - `identifier` (text): Identifier for the user (e.g., email).
    - `token` (text): Unique token for verification.
    - `expires` (timestamp with time zone): Expiration time of the token.

## Relationships

- **accounts**:

    - `userId` references `users(id)`: Each account is linked to a user.

- **sessions**:

    - `userId` references `users(id)`: Each session is linked to a user.

- **verification_tokens**:
    - No direct relationships with other tables.

## Summary

The `next_auth` schema effectively manages user authentication, session management, and email verification, ensuring a secure and organized approach to user data.

<br>
<br>
<br>

---

# public Schema

The `public` schema is designed to manage user information and pending user registrations. It consists of the following tables:

## Tables

### 1. pending_users

- **Description**: Stores information about users who are in the process of registration but have not yet been fully activated.
- **Columns**:
    - `id` (uuid): Primary key, unique identifier for the pending user.
    - `email` (text): Email address of the pending user.
    - `password` (text): Password for the pending user.
    - `salt` (text): Salt used for hashing the password.
    - `name` (text): Name of the pending user.
    - `info` (text): Additional information about the pending user (default is an empty string).
    - `created_at` (timestamp with time zone): Timestamp when the user was created.
    - `updated_at` (timestamp with time zone): Timestamp when the user was last updated.

### 2. users

- **Description**: Stores information about registered users.
- **Columns**:
    - `id` (uuid): Primary key, unique identifier for the user.
    - `name` (text): Name of the user.
    - `email` (text): Email address of the user.
    - `image` (text): URL of the user's profile image.
    - `auth_provider` (text): Authentication provider used by the user (e.g., Google, Facebook, Email).
    - `role` (text): Role assigned to the user (e.g., SUPER-ADMIN, ADMIN, EDITOR, VIEWER).
    - `first_name` (text): First name of the user.
    - `last_name` (text): Last name of the user.
    - `phone` (text): Phone number of the user.
    - `city` (text): City where the user resides.
    - `info` (text): Additional information about the user.
    - `created_at` (timestamp with time zone): Timestamp when the user was created.
    - `updated_at` (timestamp with time zone): Timestamp when the user was last updated.
    - `salt` (text): Salt used for hashing the password.

## Relationships

- **pending_users**:

    - No direct relationships with other tables.

- **users**:
    - No direct relationships with other tables.

## Summary

The `public` schema effectively manages user registrations and user information, providing a structured approach to handle both pending and active users.
