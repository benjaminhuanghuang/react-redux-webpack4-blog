Handling Transactional Emails In React Redux Apps
- https://medium.com/@rajaraodv/handling-transactional-emails-in-react-redux-apps-8b1134748f76



Scenario 1 - User has signed up to our app with an email and we need to verify that email.
1. User sign up, app shows "please verify email"
2. Server send email with verification link
3. User got email and click verfication link
4. Open a verification link, pass token to server API
5.1 If token is not valid, server returns an error and Redux App shows user resend or update email
5.2 If Success, Redux App redirect user to index.

Scenario 2 — Resend Email

Scenario 3 — Update Email