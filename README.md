![image](https://github.com/user-attachments/assets/965e24d8-f794-4698-b113-0480d94c75a3)

# Order Processing Saga - Microservices Architecture

This project implements a **Saga Orchestration Pattern** using **Spring Boot 3**, **Apache Kafka**, and **Docker**.  
It simulates an order processing system where multiple microservices handle different parts of the workflow, ensuring consistency through event-driven communication.  

---

## 🧪 Technologies  
- **Java 17**  
- **Spring Boot 3**  
- **Apache Kafka**  
- **PostgreSQL**  
- **MongoDB**  
- **Docker & Docker Compose**  
- **Redpanda Console**  

---

## ⚙️ Microservices Architecture  
The system consists of five microservices:  

1. **Order-Service**: Handles order creation and event retrieval (**MongoDB**).  
2. **Orchestrator-Service**: Manages the entire Saga execution flow (stateless).  
3. **Product-Validation-Service**: Validates product availability (**PostgreSQL**).  
4. **Payment-Service**: Processes payments based on order details (**PostgreSQL**).  
5. **Inventory-Service**: Updates product stock after an order (**PostgreSQL**).  

All services are containerized and can be started via **Docker Compose**.  

---

## 🚀 Running the Project  

You can run the project using different methods:  

### 1⃣ **Full Execution via Docker Compose**  
```bash
docker-compose up --build -d
```

### 2⃣ **Automated Execution via Python Script**  
```bash
python build.py
```

### 3⃣ **Running Only Databases & Message Broker**  
```bash
docker-compose up --build -d order-db kafka product-db payment-db inventory-db
```

### 4⃣ **Manual Execution (CLI)**  
```bash
gradle build -x test
gradle bootRun
# or
java -jar build/libs/<service-name>.jar
```

---

## 🔗 API Access  
- **Swagger UI**: [http://localhost:3000/swagger-ui.html](http://localhost:3000/swagger-ui.html)  
- **Redpanda Console**: [http://localhost:8081](http://localhost:8081)  

---

## 📌 Sample API Calls  

### ✅ **Create an Order**  
```http
POST http://localhost:3000/api/order
```
#### **Payload:**  
```json
{
  "products": [
    {
      "product": { "code": "COMIC_BOOKS", "unitValue": 15.50 },
      "quantity": 3
    },
    {
      "product": { "code": "BOOKS", "unitValue": 9.90 },
      "quantity": 1
    }
  ]
}
```

---

### 🔍 **Retrieve Saga Status**  
```http
GET http://localhost:3000/api/event?orderId=64429e987a8b646915b3735f
GET http://localhost:3000/api/event?transactionId=1682087576536_99d2ca6c-f074-41a6-92e0-21700148b519
```

