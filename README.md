# Kong API Gateway Project

## Overview

This project demonstrates how to set up **Kong API Gateway** to manage and secure microservices.  
It includes a **Node.js backend API** with **JWT authentication** and **Rate Limiting** managed by Kong.

**API Gateway**: Kong  
**Backend**: Node.js + Express  
**Authentication**: JWT  
**Rate Limiting**: Kong Plugin  
**Deployment**: Docker + Docker Compose  

---

Authentication (JWT) Setup
Kong requires consumers to authenticate using JWT.

1. Create a Consumer
sh
Copy
Edit
curl -X POST http://localhost:8001/consumers --data "username=testuser"
2. Generate JWT Credentials
sh
Copy
Edit
curl -X POST http://localhost:8001/consumers/testuser/jwt
 Response:

json
Copy
Edit
{
  "key": "your-key",
  "secret": "your-secret"
}
 API Usage
 Login to Get JWT Token
sh
Copy
Edit
curl -X POST http://localhost:8000/login \
     -H "Content-Type: application/json" \
     -d '{"username":"admin"}'
 Response: { "token": "your_jwt_token_here" }

 Access Protected Route
sh
Copy
Edit
curl -X GET http://localhost:8000/secure-data \
     -H "Authorization: Bearer your_jwt_token_here"
 Response: { "message": "This is secured data!" }

 Test Rate Limiting
After 5 requests per minute, Kong will block further requests.

sh
Copy
Edit
curl -X GET http://localhost:8000/secure-data \
     -H "Authorization: Bearer your_jwt_token_here"
 Response: { "message": "API rate limit exceeded" }

 
 Next Steps
 Deploy to Kubernetes with Kong Ingress
 Add OAuth2 Authentication
 Enable Logging & Monitoring (Prometheus/Grafana)

Feel free to contribute or raise issues! 

*License
This project is open-source under the MIT License.
