# Multi-Cloud Architecture Demo

## Overview
This project demonstrates a *multi-cloud architecture* where services are distributed across two cloud providers:

1. *Backblaze B2* – Cloud Storage (Task 1)
2. *Python Flask App* – Compute layer (local or free hosting)

The services communicate via *HTTP requests*, demonstrating interoperability between platforms.

---

## Architecture Diagram

+----------------+       HTTPS / REST API       +------------------+
|  Backblaze B2  |  ------------------------>  |  Python Flask App|
|  Cloud Storage |                               |  (Compute Layer)|
+----------------+                               +-----------------+

*Description:*
- Backblaze B2 stores example files.
- The Flask application fetches files via HTTP request from Backblaze.
- This simulates multi-cloud service interaction even if the bucket is private.

---
Interoperability

Service	Cloud Provider	Interaction Mechanism

Storage	Backblaze B2	HTTP request / REST API
Compute	Python Flask App	Fetch files from storage URL


This shows services on different platforms working together, fulfilling the multi-cloud requirement.

## Demo Application

*Python Flask App:*

```python
import requests
from flask import Flask

app = Flask(_name_)

@app.route("/fetch-file")
def fetch_file():
    url = "https://f004.backblazeb2.com/file/my-private-bucket/example.txt"
    try:
        response = requests.get(url)
        response.raise_for_status()
        content = response.text
    except Exception as e:
        content = f"Could not fetch file. Error: {str(e)}"
    return f"File content: {content}"

if _name_ == "_main_":
    app.run(port=5000)
