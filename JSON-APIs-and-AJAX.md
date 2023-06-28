## 1. Handle Click Events with JavaScript using the onclick property

You want your code to execute only once your page has finished loading.  
For that purpose, you can attach a JavaScript event to the document called `DOMContentLoaded`. Here's the code that does this:

```
document.addEventListener('DOMContentLoaded', function() {

});
```

```
<script>
  document.addEventListener('DOMContentLoaded', function(){
    // Add your code below this line
    document.getElementById('getMessage').onclick = function(){};
    // Add your code above this line
  });
</script>

<style>
  body {
    text-align: center;
    font-family: "Helvetica", sans-serif;
  }
  h1 {
    font-size: 2em;
    font-weight: bold;
  }
  .box {
    border-radius: 5px;
    background-color: #eee;
    padding: 20px 5px;
  }
  button {
    color: white;
    background-color: #4791d0;
    border-radius: 5px;
    border: 1px solid #4791d0;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    background-color: #0F5897;
    border: 1px solid #0F5897;
  }
</style>
<h1>Cat Photo Finder</h1>
<p class="message box">
  The message will go here
</p>
<p>
  <button id="getMessage">
    Get Message
  </button>
</p>
```

## 2. Change Text with click Events

```
<script>
  console.log(document.getElementsByClassName('message'));
  document.addEventListener('DOMContentLoaded', function(){
    document.getElementById('getMessage').onclick = function(){
      // Add your code below this line
      document.getElementsByClassName('message')[0].textContent="Here is the message";
      // Add your code above this line
    }
  });
</script>

<style>
  body {
    text-align: center;
    font-family: "Helvetica", sans-serif;
  }
  h1 {
    font-size: 2em;
    font-weight: bold;
  }
  .box {
    border-radius: 5px;
    background-color: #eee;
    padding: 20px 5px;
  }
  button {
    color: white;
    background-color: #4791d0;
    border-radius: 5px;
    border: 1px solid #4791d0;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    background-color: #0F5897;
    border: 1px solid #0F5897;
  }
</style>

<h1>Cat Photo Finder</h1>
<p class="message box">
  The message will go here
</p>
<p>
  <button id="getMessage">
    Get Message
  </button>
</p>
```

## 3. Get JSON with the JavaScript XMLHttpRequest Method

```
const req = new XMLHttpRequest();
req.open("GET",'/json/cats.json',true);
req.send();
req.onload = function(){
  const json = JSON.parse(req.responseText);
  document.getElementsByClassName('message')[0].innerHTML = JSON.stringify(json);
};
```

Here's a review of what each piece is doing.  
The JavaScript XMLHttpRequest object has a number of properties and methods that are used to transfer data.  
First, an instance of the XMLHttpRequest object is created and saved in the req variable.  
Next, the open method initializes a request - this example is requesting data from an API, therefore is a GET request.  
The second argument for open is the URL of the API you are requesting data from.  
The third argument is a Boolean value where true makes it an asynchronous request.  
The send method sends the request.  
Finally, the onload event handler parses the returned data and applies the JSON.stringify method to convert the JavaScript object into a string.  
This string is then inserted as the message text.

```
<script>
  document.addEventListener('DOMContentLoaded', function(){
    document.getElementById('getMessage').onclick = function(){
      // Add your code below this line
      const req = new XMLHttpRequest();
      req.open("GET",'/json/cats.json',true);
      req.send();
      req.onload = function(){
        const json = JSON.parse(req.responseText);
        document.getElementsByClassName('message')[0].innerHTML = JSON.stringify(json);
      };
      // Add your code above this line
    };
  });
</script>

<style>
  body {
    text-align: center;
    font-family: "Helvetica", sans-serif;
  }
  h1 {
    font-size: 2em;
    font-weight: bold;
  }
  .box {
    border-radius: 5px;
    background-color: #eee;
    padding: 20px 5px;
  }
  button {
    color: white;
    background-color: #4791d0;
    border-radius: 5px;
    border: 1px solid #4791d0;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    background-color: #0F5897;
    border: 1px solid #0F5897;
  }
</style>

<h1>Cat Photo Finder</h1>
<p class="message box">
  The message will go here
</p>
<p>
  <button id="getMessage">
    Get Message
  </button>
</p>
```

## 4. Get JSON with the JavaScript fetch method

Another way to request external data is to use the JavaScript fetch() method.  
It is equivalent to XMLHttpRequest, but the syntax is considered easier to understand.

```
fetch('/json/cats.json')
  .then(response => response.json())
  .then(data => {
    document.getElementById('message').innerHTML = JSON.stringify(data);
  })
```

The first line is the one that makes the request.  
So, fetch(URL) makes a GET request to the URL specified. The method returns a Promise.  
After a Promise is returned, if the request was successful, the then method is executed, which takes the response and converts it to JSON format.  
The then method also returns a Promise, which is handled by the next then method. The argument in the second then is the JSON object you are looking for!  
Now, it selects the element that will receive the data by using `document.getElementById()`.  
Then it modifies the HTML code of the element by inserting a string created from the JSON object returned from the request.

```
<script>
  document.addEventListener('DOMContentLoaded',function(){
    document.getElementById('getMessage').onclick= () => {
      // Add your code below this line
      fetch('/json/cats.json')
        .then(response => response.json())
        .then(data => {
          document.getElementById('message').innerHTML = JSON.stringify(data);
        });
      // Add your code above this line
    };
  });
</script>
<style>
  body {
    text-align: center;
    font-family: "Helvetica", sans-serif;
  }
  h1 {
    font-size: 2em;
    font-weight: bold;
  }
  .box {
    border-radius: 5px;
    background-color: #eee;
    padding: 20px 5px;
  }
  button {
    color: white;
    background-color: #4791d0;
    border-radius: 5px;
    border: 1px solid #4791d0;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    background-color: #0F5897;
    border: 1px solid #0F5897;
  }
</style>
<h1>Cat Photo Finder</h1>
<p id="message" class="box">
  The message will go here
</p>
<p>
  <button id="getMessage">
    Get Message
  </button>
</p>
```

## 5. Access the JSON Data from an API

Now you'll take a closer look at the returned data to better understand the JSON format.  
Recall some notation in JavaScript:

>[ ] -> Square brackets represent an array.


>{ } -> Curly brackets represent an object.


>" " -> Double quotes represent a string. They are also used for key names in JSON.

```
[
   {
      "id":0,
      "imageLink":"https://s3.amazonaws.com/freecodecamp/funny-cat.jpg",
      "altText":"A white cat wearing a green, helmet shaped melon on its head. ",
      "codeNames":[
         "Juggernaut",
         "Mrs. Wallace",
         "Buttercup"
      ]
   },
   {
      "id":1,
      "imageLink":"https://s3.amazonaws.com/freecodecamp/grumpy-cat.jpg",
      "altText":"A white cat with blue eyes, looking very grumpy. ",
      "codeNames":[
         "Oscar",
         "Scrooge",
         "Tyrion"
      ]
   },
   {
      "id":2,
      "imageLink":"https://s3.amazonaws.com/freecodecamp/mischievous-cat.jpg",
      "altText":"A ginger cat with one eye closed and mouth in a grin-like expression. Looking very mischievous. ",
      "codeNames":[
         "The Doctor",
         "Loki",
         "Joker"
      ]
   }
]
```
The first and last character you see in the JSON data are square brackets [ ].  
This means that the returned data is an array.  
The second character in the JSON data is a curly { bracket, which starts an object.  
Looking closely, you can see that there are three separate objects.  
The JSON data is an array of three objects, where each object contains information about a cat photo.

You learned earlier that objects contain "key-value pairs" that are separated by commas.  
In the Cat Photo example, the first object has `"id":0` where `id` is a key and `0` is its corresponding value.  
Similarly, there are keys for imageLink, altText, and codeNames.  
Each cat photo object has these same keys, but with different values.

Another interesting "key-value pair" in the first object is `"codeNames":["Juggernaut","Mrs. Wallace","ButterCup"]`.  
Here codeNames is the key and its value is an array of three strings.  
It's possible to have arrays of objects as well as a key with an array as a value.

## 6. Convert JSON Data to HTML

You can use a `forEach` method to loop through the data since the cat photo objects are held in an array.  
As you get to each item, you can modify the HTML elements.

```
<script>
  document.addEventListener('DOMContentLoaded', function(){
    document.getElementById('getMessage').onclick = function(){
      const req = new XMLHttpRequest();
      req.open("GET",'/json/cats.json',true);
      req.send();
      req.onload = function(){
        const json = JSON.parse(req.responseText);
        let html = "";
        // Add your code below this line
        json.forEach(function(val) {
        const keys = Object.keys(val);
        html += "<div class = 'cat'>";
        keys.forEach(function(key) {
        html += "<strong>" + key + "</strong>: " + val[key] + "<br>";
        });
        html += "</div><br>";
      });
        // Add your code above this line
        document.getElementsByClassName('message')[0].innerHTML = html;
      };
    };
  });
</script>

<style>
  body {
    text-align: center;
    font-family: "Helvetica", sans-serif;
  }
  h1 {
    font-size: 2em;
    font-weight: bold;
  }
  .box {
    border-radius: 5px;
    background-color: #eee;
    padding: 20px 5px;
  }
  button {
    color: white;
    background-color: #4791d0;
    border-radius: 5px;
    border: 1px solid #4791d0;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    background-color: #0F5897;
    border: 1px solid #0F5897;
  }
</style>

<h1>Cat Photo Finder</h1>
<p class="message box">
  The message will go here
</p>
<p>
  <button id="getMessage">
    Get Message
  </button>
</p>
```

## 7. Render Images from Data Sources

```
<script>
  document.addEventListener('DOMContentLoaded', function(){
    document.getElementById('getMessage').onclick = function(){
      const req=new XMLHttpRequest();
      req.open("GET",'/json/cats.json',true);
      req.send();
      req.onload = function(){
        const json = JSON.parse(req.responseText);
        let html = "";
        json.forEach(function(val) {
          html += "<div class = 'cat'>";
          // Add your code below this line
          html += "<img src = '" + val.imageLink + "' " + "alt='" + val.altText + "'>";
          // Add your code above this line
          html += "</div><br>";
        });
        document.getElementsByClassName('message')[0].innerHTML=html;
      };
     };
  });
</script>

<style>
  body {
    text-align: center;
    font-family: "Helvetica", sans-serif;
  }
  h1 {
    font-size: 2em;
    font-weight: bold;
  }
  .box {
    border-radius: 5px;
    background-color: #eee;
    padding: 20px 5px;
  }
  button {
    color: white;
    background-color: #4791d0;
    border-radius: 5px;
    border: 1px solid #4791d0;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    background-color: #0F5897;
    border: 1px solid #0F5897;
  }
</style>
<h1>Cat Photo Finder</h1>
<p class="message box">
  The message will go here
</p>
<p>
  <button id="getMessage">
    Get Message
  </button>
</p>
```

## 8. Pre-filter JSON to Get the Data You Need

```
<script>
  document.addEventListener('DOMContentLoaded', function(){
    document.getElementById('getMessage').onclick = function(){
      const req = new XMLHttpRequest();
      req.open("GET",'/json/cats.json', true);
      req.send();
      req.onload=function(){
        let json = JSON.parse(req.responseText);
        let html = "";
        // Add your code below this line
        json = json.filter(function(val) {
          return (val.id !== 1);
        });
        // Add your code above this line
         json.forEach(function(val) {
           html += "<div class = 'cat'>"
           html += "<img src = '" + val.imageLink + "' " + "alt='" + val.altText + "'>"
           html += "</div>"
         });
         document.getElementsByClassName('message')[0].innerHTML = html;
       };
     };
  });
</script>

<style>
  body {
    text-align: center;
    font-family: "Helvetica", sans-serif;
  }
  h1 {
    font-size: 2em;
    font-weight: bold;
  }
  .box {
    border-radius: 5px;
    background-color: #eee;
    padding: 20px 5px;
  }
  button {
    color: white;
    background-color: #4791d0;
    border-radius: 5px;
    border: 1px solid #4791d0;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    background-color: #0F5897;
    border: 1px solid #0F5897;
  }
</style>

<h1>Cat Photo Finder</h1>
<p class="message box">
  The message will go here
</p>
<p>
  <button id="getMessage">
    Get Message
  </button>
</p>
```

## 9. Get Geolocation Data to Find A User's GPS Coordinates

Another cool thing you can do is access your user's current location.  
Every browser has a built in navigator that can give you this information.

```
if (navigator.geolocation){
  navigator.geolocation.getCurrentPosition(function(position) {
    document.getElementById('data').innerHTML="latitude: " + position.coords.latitude + "<br>longitude: " + position.coords.longitude;
  });
}
```

First, it checks if the `navigator.geolocation` object exists. 
If it does, the `getCurrentPosition` method on that object is called, which initiates an asynchronous request for the user's position. 
If the request is successful, the callback function in the method runs. 
This function accesses the `position` object's values for latitude and longitude using dot notation and updates the HTML.

## 10. Post Data with the JavaScript XMLHttpRequest Method

```
const xhr = new XMLHttpRequest();
xhr.open('POST', url, true);
xhr.setRequestHeader('Content-Type', 'application/json; charset=UTF-8');
xhr.onreadystatechange = function () {
  if (xhr.readyState === 4 && xhr.status === 201){
    const serverResponse = JSON.parse(xhr.response);
    document.getElementsByClassName('message')[0].textContent = serverResponse.userName + serverResponse.suffix;
  }
};
const body = JSON.stringify({ userName: userName, suffix: ' loves cats!' });
xhr.send(body);
```

You've seen several of these methods before.  
Here the `open` method initializes the request as a `POST` to the given URL of the external resource, and passes `true` as the third parameter - indicating to perform the operation asynchronously.  
  
  
The `setRequestHeader` method sets the value of an HTTP request header, which contains information about the sender and the request.  
It must be called after the `open` method, but before the `send` method.  
The two parameters are the name of the header and the value to set as the body of that header.  
  
Next, the `onreadystatechange` event listener handles a change in the state of the request.  
A `readyState` of 4 means the operation is complete, and a `status` of `201` means it was a successful request.  
Therefore, the document's HTML can be updated.  
  
Finally, the send method sends the request with the body value. The body consists of a userName and a suffix key.

```
<script>
  document.addEventListener('DOMContentLoaded', function(){
    document.getElementById('sendMessage').onclick = function(){

      const userName = document.getElementById('name').value;
      const url = 'https://jsonplaceholder.typicode.com/posts';
      // Add your code below this line
      const xhr = new XMLHttpRequest();
      xhr.open('POST', url, true);
      xhr.setRequestHeader('Content-Type', 'application/json; charset=UTF-8');
      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 201){
          const serverResponse = JSON.parse(xhr.response);
          document.getElementsByClassName('message')[0].textContent = serverResponse.userName + serverResponse.suffix;
          }
        };
      const body = JSON.stringify({ userName: userName, suffix: ' loves cats!' });
      xhr.send(body);
      // Add your code above this line
    };
  });
</script>

<style>
  body {
    text-align: center;
    font-family: "Helvetica", sans-serif;
  }
  h1 {
    font-size: 2em;
    font-weight: bold;
  }
  .box {
    border-radius: 5px;
    background-color: #eee;
    padding: 20px 5px;
  }
  button {
    color: white;
    background-color: #4791d0;
    border-radius: 5px;
    border: 1px solid #4791d0;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    background-color: #0F5897;
    border: 1px solid #0F5897;
  }
</style>

<h1>Cat Friends</h1>
<p class="message box">
  Reply from Server will be here
</p>
<p>
  <label for="name">Your name:
    <input type="text" id="name"/>
  </label>
  <button id="sendMessage">
    Send Message
  </button>
</p>
```


