
#SSRF

Basic SSRF against the local server: [link](https://portswigger.net/web-security/ssrf/lab-basic-ssrf-against-localhost)

in this challenge we have a vulnerability in check stock functionality that when you click on check stock the server send a request into a `stockApi=http://stock.weliketoshop.net:8080/product/stock/check?productId=1&storeId=1` 

so the solution is make the server send a request into resource in the same network like `stockApi=http://localhost/admin`

