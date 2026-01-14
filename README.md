# user-service
Production-grade user service handling authentication, authorization, and user lifecycle management using Firebase Authentication and FastAPI.

### Why this service exists

This service acts as the identity and user management layer for the application.
It delegates authentication to Firebase (as the Identity Provider) while enforcing
authorization, user state, and business rules at the backend.

### Architecture Overview

- Firebase Authentication is used as the Identity Provider (IdP)
- Client applications authenticate directly with Firebase
- Backend verifies Firebase ID tokens
- Backend manages user state, roles, and domain-specific data

### Features

- Email/password authentication via Firebase
- OAuth login (Google, Apple, Facebook)
- Email verification enforcement
- Secure user synchronization on first login
- User profile management
- Soft delete & account suspension
- Audit logging for authentication events
- GDPR-compliant user deletion

### Authentication Model

- Authentication is handled entirely by Firebase
- Backend never processes or stores passwords
- All requests require a valid Firebase ID token
- Email verification is enforced server-side

### API Endpoints

POST   /v1/auth/login        # Sync user after Firebase login
GET    /v1/users/me          # Get current user
PATCH  /v1/users/me          # Update profile
DELETE /v1/users/me          # Soft delete account

### Environment Variables

FIREBASE_PROJECT_ID=
FIREBASE_PRIVATE_KEY=
FIREBASE_CLIENT_EMAIL=

DATABASE_URL=
JWT_AUDIENCE=
LOG_LEVEL=

### Local Development

1. Clone the repository
2. Create `.env` from `.env.example`
3. Add Firebase service account credentials
4. Run:

docker-compose up --build


### Security Practices

- Firebase Admin SDK for token verification
- Least-privilege database roles
- Rate limiting on auth endpoints
- PII masking in logs
- No sensitive data in responses
