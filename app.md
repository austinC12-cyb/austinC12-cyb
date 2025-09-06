```python
from flask import Flask, request, render_template_string
import requests

app = Flask(**name**)
HTML_TEMPLATE = '''

<!DOCTYPE html>
<html>
<head>
  <title>X-Ray Vision Terminal</title>
  <style>
    body {
      background-color: #000;
      color: #00FF00;
      font-family: monospace;
      padding: 40px;
    }
    h2 {
      color: #00FF00;
      text-shadow: 0 0 5px #0f0;
    }
    input, button {
      background-color: #111;
      border: 1px solid #0f0;
      color: #0f0;
      font-family: monospace;
      padding: 8px;
      margin-right: 10px;
    }
    input {
      width: 300px;
    }
    button:hover {
      background-color: #0f0;
      color: #000;
      cursor: pointer;
    }
    pre {
      background-color: #111;
      border: 1px solid #0f0;
      padding: 20px;
      margin-top: 30px;
      overflow-x: auto;
    }
    a {
      color: #00ffff;
      display: block;
      margin-top: 10px;
      text-decoration: none;
    }
    a:hover {
      text-decoration: underline;
      color: #ff00ff;
    }
    hr {
      border-color: #0f0;
      margin-top: 40px;
    }
  </style>
</head>
<body>
  <h2>I CAN SEE YOU WITH MY L33T HACKS!!!</h2>
  <form method="POST">
    <input name="url" placeholder="Enter a URL">
    <button>SCAN</button>
  </form>
  <a href="/status">Run internal diagnostics</a>
  <hr>
  <pre>{{ result }}</pre>
</body>
</html>
'''

@app.route("/", methods=["GET", "POST"])
def index():
result = ""
if request.method == "POST":
url = request.form.get("url", "")
try:
r = requests.get(url, timeout=3)
result = r.text[:2000]
except Exception as e:
result = f"Error: {e}"
return render_template_string(HTML_TEMPLATE, result=result)

@app.route("/status")
def trigger():
return (
"Error: Unable to reach internal diagnostics module at 127.0.0.1:1337/status.",
503,
{"Content-Type": "text/plain"},
)

if **name** == "**main**":
app.run(host="0.0.0.0", port=5000)
```
