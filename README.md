# BunkerWeb Web Application Firewall (WAF) Lab

## Hands-on Web Security Project

A hands-on cybersecurity project focused on deploying and configuring **BunkerWeb as a Web Application Firewall (WAF)** to protect a **Flask web application** in a virtualized Linux environment.

The project demonstrates how a web application can be placed behind a WAF and reverse proxy to inspect, filter, and control incoming HTTP/HTTPS traffic before it reaches the application.

---

## Project Overview

In this lab, I deployed **BunkerWeb WAF** on a **CentOS Stream 10** virtual machine and configured it to work as a security layer in front of a Flask web application.

The Flask application runs as the backend application, while BunkerWeb handles incoming web traffic and provides security controls through its Nginx-based architecture.

The main objective was to gain practical experience with:

- Web Application Firewall deployment
- Reverse proxy configuration
- HTTP/HTTPS traffic handling
- SSL/TLS configuration
- Web application protection
- WAF management and configuration
- API-based management
- HTTP response analysis
- Web security troubleshooting
- Virtualized security infrastructure

---

## Architecture

```
                    Internet / Client
                           |
                           | HTTP / HTTPS
                           v
                  +-------------------+
                  |    BunkerWeb WAF  |
                  |   Security Layer  |
                  +-------------------+
                           |
                           | Reverse Proxy
                           v
                  +-------------------+
                  |       Nginx       |
                  | Traffic Handling  |
                  +-------------------+
                           |
                           v
                  +-------------------+
                  |   Flask Web App   |
                  | Backend Service   |
                  +-------------------+
                           |
                           v
                    Application Response
```

### Traffic Flow

```
Client
  |
  | HTTP/HTTPS Request
  v
BunkerWeb WAF
  |
  | Security Inspection
  | Request Filtering
  | Policy Enforcement
  v
Nginx Reverse Proxy
  |
  | Proxy Request
  v
Flask Application
  |
  | HTTP Response
  v
Nginx
  |
  v
BunkerWeb
  |
  v
Client
```

---

## Objectives

The main objectives of this project were:

- Deploy BunkerWeb as a Web Application Firewall.
- Configure a Flask application as the protected backend service.
- Configure Nginx reverse proxy functionality.
- Understand how requests flow through a WAF.
- Configure HTTP and HTTPS access policies.
- Implement SSL/TLS for secure communication.
- Explore BunkerWeb's management interface.
- Work with the BunkerWeb API.
- Analyze HTTP requests and responses.
- Troubleshoot reverse-proxy and routing issues.
- Understand practical WAF deployment in a Linux environment.
- Build a reproducible web-security laboratory environment.

---

## Technologies Used

| Technology | Purpose |
|---|---|
| BunkerWeb WAF | Web Application Firewall and security layer |
| Nginx | Web server and reverse proxy |
| Flask | Backend web application |
| CentOS Stream 10 | Linux server operating system |
| Linux | Server administration and configuration |
| HTTP | Web traffic communication |
| HTTPS | Secure web communication |
| SSL/TLS | Encryption and secure transport |
| VMware Fusion | Virtualized laboratory environment |
| BunkerWeb Management UI | WAF configuration and management |
| BunkerWeb API | Programmatic management and control |

---

## Environment

### Operating System

- **CentOS Stream 10**
- Architecture: ARM64 / AArch64

### Backend Application — Flask

The Flask application was deployed as the backend service and tested locally before placing it behind BunkerWeb.

Example backend endpoint:

```
127.0.0.1:5000
```

The Flask application was verified independently before configuring the WAF and reverse proxy.

---

## BunkerWeb Deployment

BunkerWeb was installed and configured on the CentOS Stream virtual machine.

The deployment included the following components:

```
BunkerWeb Scheduler
        |
        +---- BunkerWeb API
        |
        +---- Nginx / BunkerWeb
        |
        +---- Protected Web Application
```

The BunkerWeb environment was configured with:

- Web UI
- Setup Wizard
- BunkerWeb API
- Reverse proxy functionality
- HTTP/HTTPS configuration
- SSL/TLS configuration
- Protected web service
- Security policies

---

## Flask Application

The Flask application acts as the backend web service.

The application was first tested directly to confirm that the backend was working correctly.

```bash
curl http://127.0.0.1:5000
```

If the Flask application is running correctly, the backend returns an HTTP response.

This step is important because it separates application problems from WAF or reverse-proxy problems.

### Backend Flow

```
Flask Application
        |
        | HTTP :5000
        v
BunkerWeb / Nginx
        |
        | HTTP / HTTPS
        v
Client
```

---

## Reverse Proxy Configuration

BunkerWeb was configured to act as the front-end security layer while forwarding legitimate requests to the Flask application.

The reverse-proxy workflow is:

```
Client Request
      |
      v
BunkerWeb
      |
      | Inspect Request
      v
Security Policies
      |
      | Allowed Request
      v
Nginx Reverse Proxy
      |
      v
Flask Backend
```

This architecture prevents clients from directly accessing the backend application when the application is properly bound and routed through the WAF.

---

## HTTP and HTTPS

The project included testing and configuration of both HTTP and HTTPS traffic.

### HTTP

HTTP was used during initial application and routing tests.

```
http://flask.local.demo
```

### HTTPS

HTTPS was configured to provide encrypted communication between the client and the protected service.

```
https://flask.local.demo
```

The HTTPS configuration was used to understand how SSL/TLS termination and secure web traffic work in a WAF/reverse-proxy environment.

---

## SSL/TLS

SSL/TLS configuration was included as part of the secure web deployment.

The purpose of TLS in this project was to:

- Encrypt communication
- Protect HTTP traffic from being transmitted in plaintext
- Provide secure client-to-server communication
- Understand certificate-based HTTPS configuration
- Learn how HTTPS works with a reverse proxy and WAF

Conceptually:

**HTTP:**
```
Client -------- Plain HTTP --------> Server
```

**HTTPS:**
```
Client ===== Encrypted TLS ========> BunkerWeb
                                      |
                                      v
                                  Backend App
```

---

## BunkerWeb Management Interface

The BunkerWeb management interface was used to manage and configure protected services.

The management interface provides a centralized way to work with:

- Services
- Security settings
- Reverse proxy configuration
- HTTP/HTTPS settings
- SSL/TLS settings
- WAF policies
- Application configuration
- Service status

This provided practical experience with managing a WAF through a web-based interface rather than relying entirely on manual configuration files.

---

## BunkerWeb API

The BunkerWeb API was also enabled as part of the project.

The API provides a programmatic interface for managing and interacting with BunkerWeb.

The API was configured to listen locally:

```
127.0.0.1:8888
```

This helped demonstrate how WAF infrastructure can be managed through APIs in addition to a graphical management interface.

---

## Security Layer

The main security concept demonstrated by the project is placing a WAF between the client and the application.

Instead of:

```
Client
  |
  v
Flask Application
```

the architecture becomes:

```
Client
  |
  v
BunkerWeb WAF
  |
  v
Nginx Reverse Proxy
  |
  v
Flask Application
```

This allows the WAF to act as a security boundary for the application.

---

## Request Inspection

One of the important learning outcomes was understanding how incoming web requests are handled before reaching the backend application.

A simplified request-processing flow is:

```
1. Client sends HTTP/HTTPS request
              |
              v
2. BunkerWeb receives request
              |
              v
3. WAF/security policies process request
              |
              v
4. Request is allowed or blocked
              |
              v
5. Allowed request is forwarded
              |
              v
6. Flask application processes request
              |
              v
7. Response travels back through proxy
              |
              v
8. Client receives response
```

This demonstrates the basic role of a WAF in a web application security architecture.

---

## Troubleshooting and Debugging

A major part of this project involved troubleshooting web traffic, routing, reverse-proxy behavior, and service configuration.

The troubleshooting process included checking:

```
BunkerWeb
    |
    +-- Service Status
    |
    +-- Nginx Status
    |
    +-- API Status
    |
    +-- Flask Status
    |
    +-- Listening Ports
    |
    +-- HTTP Responses
    |
    +-- Reverse Proxy Configuration
    |
    +-- Domain / Host Configuration
```

Useful Linux commands included:

```bash
systemctl status bunkerweb
systemctl status bunkerweb-scheduler
systemctl status bunkerweb-api
```

Checking listening ports:

```bash
ss -tulpn
```

Testing the Flask backend:

```bash
curl http://127.0.0.1:5000
```

Testing HTTP/HTTPS:

```bash
curl -I http://flask.local.demo
curl -k -I https://flask.local.demo
```

Checking Nginx/BunkerWeb logs:

```bash
journalctl -u bunkerweb
```

These tests helped identify whether an issue was related to the application, proxy, WAF, DNS/host configuration, or service availability.

---

## Example Service Ports

The laboratory environment used separate ports for different components.

| Service | Example Address |
|---|---|
| Flask Application | 127.0.0.1:5000 |
| BunkerWeb API | 127.0.0.1:8888 |
| HTTP | 0.0.0.0:80 |
| HTTPS | 0.0.0.0:443 |
| BunkerWeb Management UI | Management interface |

The exact port exposure should be adapted according to the deployment environment.

---

## Domain Configuration

A local hostname was used for testing the protected application.

```
flask.local.demo
```

The hostname was mapped to the WAF server so that requests could be routed through BunkerWeb instead of directly accessing the Flask service.

The intended flow was:

```
flask.local.demo
        |
        v
BunkerWeb
        |
        v
Flask Application
```

---

## Project Learning

Through this project, I gained practical experience in:

1. **Web Application Firewalls** — Understanding the purpose of a WAF and how it can protect web applications by inspecting incoming requests.
2. **Reverse Proxies** — Understanding how Nginx/BunkerWeb can receive client requests and forward them to backend applications.
3. **HTTP/HTTPS** — Learning how web requests are handled over HTTP and secure HTTPS connections.
4. **SSL/TLS** — Understanding the role of certificates and encrypted communication in secure web deployments.
5. **Linux Server Administration** — Working with services, ports, logs, networking, processes, and application deployment on CentOS Stream.
6. **Application Security** — Understanding how a security layer can be positioned in front of an application.
7. **Troubleshooting** — Analyzing service status, HTTP response codes, logs, routing configuration, and connectivity problems.
8. **Virtualized Security Infrastructure** — Building and testing the entire environment inside a virtual machine.

---

## Problems Encountered

During the implementation, several configuration and routing challenges were encountered.

These included issues related to:

- Reverse proxy routing
- Service configuration
- Nginx port binding
- Hostname configuration
- WAF service configuration
- HTTP/HTTPS behavior
- Management UI access
- Backend application routing

Instead of treating these issues as failures, they were used as part of the learning process to understand how each component communicates.

---

## Troubleshooting Methodology

The troubleshooting approach followed a layered model:

```
Layer 1 — Operating System
        |
        v
Layer 2 — Service Status
        |
        v
Layer 3 — Network / Ports
        |
        v
Layer 4 — Nginx / Reverse Proxy
        |
        v
Layer 5 — BunkerWeb WAF
        |
        v
Layer 6 — Flask Application
        |
        v
Layer 7 — HTTP / HTTPS Response
```

This approach makes it easier to isolate problems instead of changing multiple configurations at the same time.

---

## Security Architecture

The final conceptual architecture of the project is:

```
                         CLIENT
                           |
                           |
                     HTTP / HTTPS
                           |
                           v
                 +-------------------+
                 |    BunkerWeb WAF  |
                 |                   |
                 | Request Filtering |
                 | Security Policies |
                 | TLS / HTTPS       |
                 +-------------------+
                           |
                           |
                    Reverse Proxy
                           |
                           v
                 +-------------------+
                 |       Nginx       |
                 +-------------------+
                           |
                           |
                     Backend Proxy
                           |
                           v
                 +-------------------+
                 |    Flask Web App  |
                 |    127.0.0.1:5000 |
                 +-------------------+
```

---

## Why This Project Matters

Modern web applications are exposed to a wide range of security risks. Simply running an application server is not enough to create a strong security architecture.

A WAF can provide an additional security layer between users and the application.

This project demonstrates the practical concept of:

```
User
 ↓
Web Security Layer
 ↓
Reverse Proxy
 ↓
Application
```

The project therefore combines web security, network security, Linux administration, application deployment, and infrastructure security into one practical laboratory.

---

## Key Takeaways

The major concepts demonstrated in this project are:

- BunkerWeb WAF deployment
- WAF architecture
- Reverse proxy architecture
- Nginx configuration
- Flask application deployment
- HTTP/HTTPS configuration
- SSL/TLS implementation
- WAF management
- API-based configuration
- Linux service management
- Port and network troubleshooting
- HTTP response analysis
- Secure application deployment
- Virtualized cybersecurity infrastructure

---

## Future Improvements

The lab can be extended with additional security testing and monitoring capabilities.

Potential future improvements include:

- OWASP Top 10 testing
- Automated WAF rule validation
- Security logging and centralized monitoring
- Wazuh integration
- CrowdSec integration
- Web attack detection
- Rate limiting
- Bot protection
- Advanced TLS hardening
- Security header testing
- Automated deployment
- Docker/containerized deployment
- CI/CD security integration
- Vulnerability scanning
- Attack simulation in an isolated lab

---

## Project Outcome

The project provided practical experience in deploying a Web Application Firewall and reverse-proxy architecture rather than only studying WAF concepts theoretically.

By building the environment from the application layer through the WAF and proxy layer, I gained a better understanding of how web applications can be securely exposed while maintaining control over incoming traffic.

---

## Skills Demonstrated

- Cybersecurity
- Web Application Security
- WAF Deployment
- Network Security
- Linux Administration
- Nginx
- Reverse Proxy
- HTTP/HTTPS
- SSL/TLS
- Flask
- API Management
- System Troubleshooting
- Virtualization
- Security Infrastructure

---

## Project Screenshots

> Add screenshots of the actual lab environment here.

Recommended screenshots:

- BunkerWeb dashboard
- Protected service configuration
- Flask application running
- HTTP response testing
- HTTPS response testing
- SSL/TLS configuration
- BunkerWeb service status
- Nginx service status
- BunkerWeb API status
- Final protected application

Example:

```markdown
## Screenshots Uploaded


## Repository Structure

```
bunkerweb-waf-lab/
│
├── README.md
│
├── flask-app/
│   ├── app.py
│   ├── requirements.txt
│   └── templates/
│
├── bunkerweb/
│   ├── configuration/
│   └── policies/
│
├── nginx/
│   └── configuration/
│
├── screenshots/
│   ├── bunkerweb-dashboard.png
│   ├── flask-application.png
│   ├── https-configuration.png
│   └── service-status.png
│
└── docs/
    └── architecture.md
```

---

## Installation Overview

### Step 1 — Update the System

```bash
sudo dnf update -y
```

### Step 2 — Install Required Packages

Install the packages required for the Flask application and supporting environment.

```bash
sudo dnf install -y python3 python3-pip nginx curl
```

### Step 3 — Create Flask Environment

```bash
python3 -m venv venv
source venv/bin/activate
```

### Step 4 — Install Flask

```bash
pip install flask
```

### Step 5 — Start Flask

Example:

```bash
python app.py
```

Verify:

```bash
curl http://127.0.0.1:5000
```

### Step 6 — Install and Configure BunkerWeb

Install BunkerWeb according to the official installation method for the target Linux distribution and architecture.

After installation, verify the services:

```bash
systemctl status bunkerweb
systemctl status bunkerweb-scheduler
systemctl status bunkerweb-api
```

### Step 7 — Configure the Protected Service

Configure the BunkerWeb service with the required:

- Server Name
- Reverse Proxy
- Backend URL
- HTTP/HTTPS
- SSL/TLS
- Security Policies

### Step 8 — Test the Application

```bash
curl -I http://flask.local.demo
```

For HTTPS:

```bash
curl -k -I https://flask.local.demo
```

---

## Verification Checklist

Use the following checklist when reproducing the lab:

- [x] CentOS Stream server configured
- [x] Flask application deployed
- [x] Flask backend tested
- [x] BunkerWeb installed
- [x] BunkerWeb services verified
- [x] Nginx configured
- [x] Reverse proxy configured
- [x] Protected service created
- [x] HTTP tested
- [x] HTTPS tested
- [x] SSL/TLS configured
- [x] Management interface configured
- [x] API configured
- [x] HTTP responses analyzed
- [x] Routing issues troubleshot
- [x] Final WAF-to-Flask architecture verified

---

## Ethical Use

This project is intended for educational and authorized security testing only.

Do not use the WAF testing techniques, attack simulations, or security testing methods demonstrated in this repository against systems or applications without proper authorization.

---

## Author

**Shlok Chavan**

Cybersecurity | Network Security | SOC | VAPT

Interested in:

- Cybersecurity
- Network Security
- SOC Operations
- Vulnerability Assessment
- Penetration Testing
- Web Application Security
- Security Infrastructure
- AI Security

### Connect

- **LinkedIn:** linkedin.com/in/shlok-chavan-17926a356
- **Portfolio:** https://shlok-chavan.vercel.app

---

## Tags

`#Cybersecurity` `#WebSecurity` `#WAF` `#BunkerWeb` `#NetworkSecurity` `#ApplicationSecurity` `#Linux` `#Nginx` `#Flask` `#HTTPS` `#SSLTLS` `#ReverseProxy` `#SecurityEngineering` `#Virtualization` `#HandsOnLearning`

---

## Disclaimer

This repository represents a personal cybersecurity laboratory project created for learning, experimentation, and skill development. All testing should be performed only in environments where explicit authorization has been provided.
