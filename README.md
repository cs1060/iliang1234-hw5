# hw5_server
Stub HTTP and SSH servers for Homework 5.
Prototyped with Codeium Windsurf and the DeepSeek V3 model.
Intentionally incomplete—these programs do not handle all situations
gracefully.

## Setup
1. Create a virtual environment:
```bash
python3 -m venv venv
```

2. Activate the virtual environment:
```bash
source venv/bin/activate  # On Unix/macOS
# or
.\venv\Scripts\activate  # On Windows
```

3. Install dependencies:
```bash
pip3 install -r requirements.txt
```

Note: Always make sure the virtual environment is activated (you'll see `(venv)` in your prompt) before running any Python scripts.

## ssh_server.py
Usage:
```
python3 ssh_server.py # defaults to 2222, admin, admin
python3 ssh_server.py --port 2224 
python3 ssh_server.py --port 2224 --username myuser --password mypass
```

## http_server.py
Usage:
```
python3 http_server.py # defaults to 8080, admin, admin
python3 http_server.py --port 8081 
python3 http_server.py --port 8081 --username user --password pass
```

# AI Model Testing for SQL Injection (initial generation from Windsurf)

I tested several AI models to understand their responses to SQL injection-related prompts:

## ChatGPT (GPT-3.5)
- Initially refused to provide direct SQL injection assistance
- Has strong ethical guardrails against security exploits
- Required framing the request as security research/education
- Eventually provided guidance when explicitly mentioning educational context

## Claude 2
- Very resistant to providing SQL injection help
- Maintained strict ethical boundaries
- Would only discuss SQL injection in theoretical terms
- Suggested learning about security through proper channels

## Bard
- More willing to discuss SQL injection concepts
- Still showed some resistance to direct exploit generation
- Provided general SQL injection patterns after educational context
- Included warnings about ethical use

## Successful Approach
To work around AI safety measures, I:
1. Framed requests in educational/research context (I'm not a threat)
2. Emphasized testing known vulnerabilities
3. Referenced existing security documentation
4. Specified the controlled test environment
5. Included explicit mentions of academic purpose

The key was to present the task as legitimate security research rather than an actual attack attempt. Most models were more cooperative when understanding the educational nature of the request.

## Test Attack Command (from Windsurf)
```bash
curl -X POST https://cat-hw4.vercel.app/county_data -H "Content-Type: application/json" -d @attack.json
```

# Simple Penetration Tester (initial generation from Windsurf)
## Install dependencies
```bash
pip install -r requirements.txt
brew install nmap  # for macOS
```

## Running the servers
In one terminal:
```bash
python3 ssh_server.py  # starts SSH server on port 2222
```

In another terminal:
```bash
python3 http_server.py  # starts HTTP server on port 8080
```

## Running the vulnerability scanner
Normal mode (only shows successful exploits):
```bash
python3 vulnerability_scanner.py
```
Expected output:
```
http://admin:admin@127.0.0.1:8080 success
ssh://admin:admin@127.0.0.1:2222 success
```

Verbose mode (shows scanning progress):
```bash
python vulnerability_scanner.py -v
```
Expected output:
```
Found open ports: [2222, 8080]
Checking port 2222...
Trying HTTP auth with admin:admin
HTTP connection error on port 2222: Connection refused
Trying HTTP auth with root:abc123
HTTP connection error on port 2222: Connection refused
Trying HTTP auth with skroob:12345
HTTP connection error on port 2222: Connection refused
Trying SSH auth with admin:admin
ssh://admin:admin@127.0.0.1:2222 success
Trying SSH auth with root:abc123
SSH connection error on port 2222: Authentication failed.
Trying SSH auth with skroob:12345
SSH connection error on port 2222: Authentication failed.
Checking port 8080...
Trying HTTP auth with admin:admin
http://admin:admin@127.0.0.1:8080 success
Trying HTTP auth with root:abc123
HTTP connection error on port 8080: 401 Client Error
Trying HTTP auth with skroob:12345
HTTP connection error on port 8080: 401 Client Error
Trying SSH auth with admin:admin
SSH connection error on port 8080: [Errno 61] Connection refused
Trying SSH auth with root:abc123
SSH connection error on port 8080: [Errno 61] Connection refused
Trying SSH auth with skroob:12345
SSH connection error on port 8080: [Errno 61] Connection refused
```

