# EX01 Developing a Simple Webserver
## Date:15-10-2026
## Reg:26008389

## AIM:
To develop a simple webserver to serve html pages and display the list of protocols in TCP/IP Protocol Suite.

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

## PROGRAM:~~~
from http.server import HTTPServer, BaseHTTPRequestHandler
content = """
<!DOCTYPE html>
<html>
<head>
<title>My webserver</title>
</head>
<style>
        :root {
            --primary: #2563eb;
            --primary-dark: #1d4ed8;
            --bg-color: #f8fafc;
            --card-bg: #ffffff;
            --text-main: #1e293b;
            --text-muted: #64748b;
            --border-color: #e2e8f0;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-main);
            margin: 0;
            padding: 40px 20px;
            display: flex;
            justify-content: center;
        }

        .container {
            width: 100%;
            max-width: 900px;
        }

        header {
            text-align: center;
            margin-bottom: 40px;
        }

        h1 {
            color: var(--primary);
            margin-bottom: 10px;
            font-size: 2.2rem;
        }

        p.subtitle {
            color: var(--text-muted);
            font-size: 1.1rem;
        }

        .protocol-group {
            background: var(--card-bg);
            border-radius: 12px;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
            margin-bottom: 30px;
            overflow: hidden;
            border: 1px solid var(--border-color);
        }

        .group-header {
            background-color: var(--primary);
            color: white;
            padding: 15px 25px;
            font-size: 1.25rem;
            font-weight: 600;
        }

        .protocol-list {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        .protocol-item {
            padding: 20px 25px;
            border-bottom: 1px solid var(--border-color);
            display: flex;
            flex-direction: column;
            gap: 6px;
            transition: background-color 0.2s ease;
        }

        .protocol-item:last-child {
            border-bottom: none;
        }

        .protocol-item:hover {
            background-color: #f1f5f9;
        }

        .protocol-name {
            font-size: 1.1rem;
            font-weight: 700;
            color: var(--primary-dark);
        }

        .protocol-desc {
            color: var(--text-muted);
            font-size: 0.95rem;
            line-height: 1.5;
        }

        .badge {
            display: inline-block;
            background: #e0f2fe;
            color: #0369a1;
            padding: 2px 8px;
            border-radius: 4px;
            font-size: 0.75rem;
            font-weight: 600;
            margin-left: 8px;
            vertical-align: middle;
        }
    </style>
<body>
<div class="container">
        <header>
            <h1>Common Network Protocols</h1>
            <p class="subtitle">A structured list of essential communication standards categorized by function.</p>
        </header>

        <!-- Application Layer -->
        <div class="protocol-group">
            <div class="group-header">Application Layer Protocols</div>
            <ul class="protocol-list">
                <li class="protocol-item">
                    <div>
                        <span class="protocol-name">HTTP / HTTPS</span>
                        <span class="badge">Port 80 / 443</span>
                    </div>
                    <div class="protocol-desc">Hypertext Transfer Protocol (Secure) is used for transferring web pages and data over the internet.</div>
                </li>
                <li class="protocol-item">
                    <div>
                        <span class="protocol-name">FTP / SFTP</span>
                        <span class="badge">Port 20, 21 / 22</span>
                    </div>
                    <div class="protocol-desc">File Transfer Protocol (Secure) is used for uploading and downloading files between a client and a server.</div>
                </li>
                <li class="protocol-item">
                    <div>
                        <span class="protocol-name">SMTP</span>
                        <span class="badge">Port 25 / 587</span>
                    </div>
                    <div class="protocol-desc">Simple Mail Transfer Protocol is used for transmitting and sending outgoing emails.</div>
                </li>
                <li class="protocol-item">
                    <div>
                        <span class="protocol-name">DNS</span>
                        <span class="badge">Port 53</span>
                    </div>
                    <div class="protocol-desc">Domain Name System translates human-readable domain names (like example.com) into machine-readable IP addresses.</div>
                </li>
            </ul>
        </div>

        <!-- Transport Layer -->
        <div class="protocol-group">
            <div class="group-header">Transport Layer Protocols</div>
            <ul class="protocol-list">
                <li class="protocol-item">
                    <div>
                        <span class="protocol-name">TCP</span>
                        <span class="badge">Connection-Oriented</span>
                    </div>
                    <div class="protocol-desc">Transmission Control Protocol provides reliable, ordered, and error-checked delivery of data streams.</div>
                </li>
                <li class="protocol-item">
                    <div>
                        <span class="protocol-name">UDP</span>
                        <span class="badge">Connectionless</span>
                    </div>
                    <div class="protocol-desc">User Datagram Protocol enables fast, low-latency transmission ideal for live streaming, gaming, and VoIP where speed beats reliability.</div>
                </li>
            </ul>
        </div>

        <!-- Internet Layer -->
        <div class="protocol-group">
            <div class="group-header">Internet & Network Layer Protocols</div>
            <ul class="protocol-list">
                <li class="protocol-item">
                    <div>
                        <span class="protocol-name">IP (IPv4 / IPv6)</span>
                        <span class="badge">Addressing</span>
                    </div>
                    <div class="protocol-desc">Internet Protocol is responsible for routing packets across network boundaries and identifying hosts via IP addresses.</div>
                </li>
                <li class="protocol-item">
                    <div>
                        <span class="protocol-name">ICMP</span>
                        <span class="badge">Diagnostics</span>
                    </div>
                    <div class="protocol-desc">Internet Control Message Protocol is used for network diagnostics, error reporting, and testing connectivity (e.g., the <code>ping</code> command).</div>
                </li>
                <li class="protocol-item">
                    <div>
                        <span class="protocol-name">ARP</span>
                        <span class="badge">Mapping</span>
                    </div>
                    <div class="protocol-desc">Address Resolution Protocol maps an IP address to a physical hardware MAC address on a local area network.</div>
                </li>
            </ul>
        </div>

    </div></body>
</html>
"""
class myhandler(BaseHTTPRequestHandler):
    def do_GET(self):
        print("request received")
        self.send_response(200)
        self.send_header('content-type', 'text/html; charset=utf-8')
        self.end_headers()
        self.wfile.write(content.encode())
server_address = ('',8080)
httpd = HTTPServer(server_address,myhandler)
print("my webserver is running...")
httpd.serve_forever()
~~~

## OUTPUT:

![alt text](<Screenshot 2026-10-24 140513.png>)

## RESULT:
The program for implementing simple webserver is executed successfully.

