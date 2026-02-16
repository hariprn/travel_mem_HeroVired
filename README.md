


# Travel Memory Application Deployment (MERN Stack on AWS)

## Project Overview

This project demonstrates deployment of the Travel Memory application built using the MERN stack (MongoDB, Express, React, Node.js) on AWS infrastructure.

The deployment architecture includes:

* Separate EC2 instances for frontend and backend
* Nginx reverse proxy configuration
* MongoDB Atlas database
* Horizontal scaling using AMIs
* Target Groups and Application Load Balancers
* Custom domain configuration using Cloudflare DNS
* SSL configuration using Certbot (Let's Encrypt)

---

## Architecture Overview

```
User
 ↓
Cloudflare DNS
 ↓
Frontend Load Balancer
 ↓
Frontend EC2 (Nginx + React)
 ↓ Reverse Proxy (/api)
Backend Load Balancer
 ↓
Backend EC2 (Node.js + PM2)
 ↓
MongoDB Atlas
```

Insert architecture diagram here:

```
screenshots/architecture.png
```

---

## 1. MongoDB Atlas Setup

1. Create MongoDB Atlas account
2. Create free M0 cluster
3. Create database user
4. Allow network access:

```
0.0.0.0/0
```

5. Copy connection string:

```
mongodb+srv://<user>:<password>@cluster.mongodb.net/travelmemory
```

Insert screenshot:

```
screenshots/mongodb.png
```

---

## 2. Launch EC2 Instances

Create two instances:

* frontend-1
* backend-1

Configuration:

* Ubuntu 22.04
* t2.micro
* 8GB storage

### Security Groups

Frontend:

* SSH (22) → My IP
* HTTP (80) → Anywhere

Backend:

* SSH (22) → My IP
* Port 3000 allowed

Insert screenshot:

```
screensho
```

# Travel Memory

`.env` file to work with the backend after creating a database in mongodb: 

```
MONGO_URI='ENTER_YOUR_URL'
PORT=3000
```

Data format to be added: 

```json
{
    "tripName": "Incredible India",
    "startDateOfJourney": "19-03-2022",
    "endDateOfJourney": "27-03-2022",
    "nameOfHotels":"Hotel Namaste, Backpackers Club",
    "placesVisited":"Delhi, Kolkata, Chennai, Mumbai",
    "totalCost": 800000,
    "tripType": "leisure",
    "experience": "Lorem Ipsum, Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum, ",
    "image": "https://t3.ftcdn.net/jpg/03/04/85/26/360_F_304852693_nSOn9KvUgafgvZ6wM0CNaULYUa7xXBkA.jpg",
    "shortDescription":"India is a wonderful country with rich culture and good people.",
    "featured": true
}
```


For frontend, you need to create `.env` file and put the following content (remember to change it based on your requirements):
```bash
REACT_APP_BACKEND_URL=http://localhost:3000
```
