# EX01 Developing a Simple Webserver
## Date:

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
import subprocess


def get_specs():
    info = {
        "OS": platform.system(),
        "Release": platform.release(),
        "Version": platform.version(),
        "Architecture": platform.machine(),
        "Processor": platform.processor(),
    }
    try:
        out = subprocess.check_output(
            "wmic computersystem get Model,TotalPhysicalMemory",
            shell=True,
            text=True,
        )
        lines = [x.strip() for x in out.splitlines() if x.strip()]
        if len(lines) > 1:
            parts = lines[1].rsplit(None, 1)
            info["Model"] = parts[0]
            ram_gb = round(int(parts[1]) / (1024**3), 2)
            info["RAM"] = f"{ram_gb} GB"
    except Exception:
        pass
    return info


class Handler(BaseHTTPRequestHandler):
    def do_GET(self):
        specs = get_specs()
        items = "".join(f"<li><b>{k}:</b> {v}</li>" for k, v in specs.items())

        page = f"""
        <html>
        <head><title>Laptop Specs</title></head>
        <body>
            <h2>Windows Laptop Specifications</h2>
            <ul>{items}</ul>
        </body>
        </html>
        """

        self.send_response(200)
        self.send_header("Content-type", "text/html")
        self.end_headers()
        self.wfile.write(page.encode())


server = HTTPServer(("127.0.0.1", 8000), Handler)
print("Serving at [http://127.0.0.1:8000](http://127.0.0.1:8000)")
server.serve_forever()
~~~

## OUTPUT:


## RESULT:
The program for implementing simple webserver is executed successfully.
