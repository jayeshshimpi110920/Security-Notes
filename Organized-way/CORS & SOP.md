## SOP (same-Origin Policy) 

Its a rule that is enforced by browsers to control access to data between web application.

* This does not prevent writing between web application, it prevents reading between web application.
* Access is determined based on the origin.

Examples to Illustrate <br>
**Example 1: Writing is Allowed** <br>
A webpage on https://site-a.com includes a <form>: <br>
```
<form action="https://site-b.com/submit-data" method="POST">
    <input type="text" name="data" value="example">
    <input type="submit" value="Send">
</form>
```
When the user submits the form, the data is sent to https://site-b.com. SOP allows this because it’s a write operation. <br>
**Example 2: Reading is Prevented** <br>
The same page on https://site-a.com tries to fetch data from https://site-b.com: <br>
```
fetch("https://site-b.com/api")
    .then(response => response.json())
    .then(data => console.log(data));
```
If https://site-b.com does not include the necessary CORS headers, the browser blocks access to the response data, even though the request is sent successfully.
<br>

POC : it prevent reading between web application unless it explicitaly allow by CORS.

what is origin?
-Its defined by schema(protocol), hostname(domain) and port of URL used to access it. <br>
<img width="290" alt="{45DEAA7E-02C1-419A-8DE8-CA9F04CBDA87}" src="https://github.com/user-attachments/assets/02680c5d-bf4c-4956-b9b8-9e1ad534e1b0">
<br>
Origin must  need to same in SOP 


---

## CORS (Cross-Origin resource sharing)
its a mechanism that uses **HTTP headers** to define origins that the browser permit loading resources.
<br> <img width="282" alt="{1AC342A2-BC95-4CB8-903F-DBB11775D2FF}" src="https://github.com/user-attachments/assets/4172380c-3db6-4ddd-acbd-e85f97c960df">
<br>

CORS makes use of 2 HTTP headers:
1) Access-Control-Allow-Origin
2) Access-Control-Allow-Credentials


## Access-Control-Allow-Origin (response header)
<br>
## SOP (same-Origin Policy) 

Its a rule that is enforced by browsers to control access to data between web application.

* This does not prevent writing between web application, it prevents reading between web application.
* Access is determined based on the origin.

Examples to Illustrate <br>
**Example 1: Writing is Allowed** <br>
A webpage on https://site-a.com includes a <form>: <br>
```
<form action="https://site-b.com/submit-data" method="POST">
    <input type="text" name="data" value="example">
    <input type="submit" value="Send">
</form>
```
When the user submits the form, the data is sent to https://site-b.com. SOP allows this because it’s a write operation. <br>
**Example 2: Reading is Prevented** <br>
The same page on https://site-a.com tries to fetch data from https://site-b.com: <br>
```
fetch("https://site-b.com/api")
    .then(response => response.json())
    .then(data => console.log(data));
```
If https://site-b.com does not include the necessary CORS headers, the browser blocks access to the response data, even though the request is sent successfully.
<br>

POC : it prevent reading between web application unless it explicitaly allow by CORS.

what is origin?
-Its defined by schema(protocol), hostname(domain) and port of URL used to access it. <br>
<img width="290" alt="{45DEAA7E-02C1-419A-8DE8-CA9F04CBDA87}" src="https://github.com/user-attachments/assets/02680c5d-bf4c-4956-b9b8-9e1ad534e1b0">
<br>
Origin must  need to same in SOP 


---

## CORS (Cross-Origin resource sharing)
its a mechanism that uses **HTTP headers** to define origins that the browser permit loading resources.
<br> <img width="282" alt="{1AC342A2-BC95-4CB8-903F-DBB11775D2FF}" src="https://github.com/user-attachments/assets/4172380c-3db6-4ddd-acbd-e85f97c960df">
<br>

CORS makes use of 2 HTTP headers:
1) Access-Control-Allow-Origin
2) Access-Control-Allow-Credentials


## Access-Control-Allow-Origin (response header)
<br>
<img width="386" alt="{D724524A-3B4C-4CF2-A543-8807E14588C4}" src="https://github.com/user-attachments/assets/673e63af-29db-45e8-b4be-325eaffc6aa4">
<br>











