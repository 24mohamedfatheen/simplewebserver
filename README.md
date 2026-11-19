# EX01 Developing a Simple Webserver
**Name:** Mohamed Fatheen  
**Register No:** `26006890`  
**Date:** `19/11/2026`

## AIM:
To develop a simple webserver to serve html pages and display the Windows Specifications of your Laptop.

## DESIGN STEPS:
### Step 1: 
HTML content creation.

### Step 2:
Design of webserver workflow.

### Step 3:
Implementation using Python code.

### Step 4:
Import the necessary modules.

### Step 5:
Define a custom request handler.

### Step 6:
Start an HTTP server on a specific port.

### Step 7:
Run the Python script to serve web pages.

### Step 8:
Serve the HTML pages.

### Step 9:
Start the server script and check for errors.

### Step 10:
Open a browser and navigate to http://127.0.0.1:8000 (or the assigned port).

## PROGRAM:
~~~
from http.server import BaseHTTPRequestHandler, HTTPServer
import platform

class Server(BaseHTTPRequestHandler):
    def do_GET(self):
        html = f"""
        <h2>Windows Specs</h2>
        <p>OS: {platform.system()} {platform.release()}</p>
        <p>Version: {platform.version()}</p>
        <p>Arch: {platform.machine()}</p>
        <p>CPU: {platform.processor()}</p>
        """
        self.send_response(200)
        self.end_headers()
        self.wfile.write(html.encode())

HTTPServer(("127.0.0.1", 8000), Server).serve_forever()
~~~

## OUTPUT:
<img width="1917" height="985" alt="image" src="https://github.com/user-attachments/assets/4733b444-74dc-49c1-bddc-1203593567cf" />
<img width="1475" height="366" alt="image" src="https://github.com/user-attachments/assets/abc3a2d7-bca9-47dd-be42-3c9a802c595b" />


## RESULT:
The program for implementing simple webserver is executed successfully.
