## JWT
JWT token has 3 parts: <header>.<payload>.<signature>

- Header: A JSON(Base64 encoded) that has info about algorithm used(like HS256, RSA) and so on.

- Payload: A JSON(Base64 encoded) that has info about the user. Payload is just a JSON should contain anything that your app needs to identify user.
Typically this is:
    - User Id, Username, Email, Image URL
    - Any ACL like: isAdmin, isManager etc.

- Signature: A String that was generated using #1 + #2 + “a secret” (that only the server knows), using the algorithm mentioned in #1.


https://jwt.io can show the content of JWT token 


## Implementing JWT Token In The Server
- Generate JWT token and return it to the client
    - User Signs Up (using email or Social network)
    - User Signs In (after Sign up)
    - Tries to Re-Authenticate using existing token (Browser Refresh)

- Verify JWT token for protected routes in future requests

## Storing And Using JWT In Client 
- Sign In page
- Sign Up page
- Logout
- Browser Refresh