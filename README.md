# hw5_server
Stub HTTP and SSH servers for Homework 5.
Prototyped with Codeium Windsurf and the DeepSeek V3 model.
Intentionally incomplete—these programs do not handle all situations
gracefully.

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

# AI Model Testing for SQL Injection

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
1. Framed requests in educational/research context
2. Emphasized testing known vulnerabilities
3. Referenced existing security documentation
4. Specified the controlled test environment
5. Included explicit mentions of academic purpose

The key was to present the task as legitimate security research rather than an actual attack attempt. Most models were more cooperative when understanding the educational nature of the request.

## Test Attack Command
```bash
curl -X POST https://cat-hw4.vercel.app/county_data -H "Content-Type: application/json" -d @attack.json
```