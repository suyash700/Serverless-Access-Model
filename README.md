# 🚀 Serverless Orders API (AWS)

A serverless REST API that performs CRUD operations on orders using AWS services.

---

## 🧠 Architecture

Client → API Gateway → Lambda → DynamoDB

Built using:

* Amazon API Gateway
* AWS Lambda
* Amazon DynamoDB

---

## 📂 API Endpoints

| Method | Endpoint | Description        |
| ------ | -------- | ------------------ |
| GET    | /orders  | Fetch all orders   |
| POST   | /orders  | Create a new order |
| PUT    | /orders  | Update an order    |
| DELETE | /orders  | Delete an order    |

---

## 🗄️ DynamoDB Table Design

* Table Name: **Orders**
* Partition Key: `orderId`
* Sort Key: `timestamp`

---

# 🔧 Steps Performed

## 1️⃣ Created DynamoDB Table

* Open AWS Console → DynamoDB
* Created table:

  * Name: `Orders`
  * Partition key: `orderId`
  * Sort key: `timestamp`

---

## 2️⃣ Created IAM Role

* Open IAM → Roles → Create Role
* Selected **Lambda service**
* Attached policies:

  * AmazonDynamoDBFullAccess
  * AWSLambdaBasicExecutionRole

---

## 3️⃣ Created Lambda Functions

Created 4 functions:

* `createOrder`
* `getOrders`
* `updateOrder`
* `deleteOrder`

Runtime: Python 3.x
Attached IAM role to all functions

---

## 4️⃣ Implemented Lambda Logic

### ✔ createOrder

* Accepts JSON input
* Generates `orderId` (UUID) and `timestamp`
* Stores data in DynamoDB

---

### ✔ getOrders

* Uses `scan()` to fetch all records

---

### ✔ updateOrder

* Uses `update_item()`
* Fixed DynamoDB reserved keyword issue using:

  * `ExpressionAttributeNames`

---

### ✔ deleteOrder

* Uses `delete_item()`
* Requires `orderId` + `timestamp`

---

## 5️⃣ Created API Gateway

* Selected **REST API**
* Endpoint type: **Regional**

---

## 6️⃣ Created Resource

Created resource:

```
/orders
```

---

## 7️⃣ Added Methods

Mapped each method to a separate Lambda:

| Method | Lambda      |
| ------ | ----------- |
| GET    | getOrders   |
| POST   | createOrder |
| PUT    | updateOrder |
| DELETE | deleteOrder |

✔ Enabled **Lambda Proxy Integration** for all methods

---

## 8️⃣ Fixed Common Issues

* ❌ Methods created on `/` instead of `/orders` → Fixed routing
* ❌ Missing Authentication Token → Fixed endpoint path
* ❌ 502 Internal Server Error → Fixed Lambda logic
* ❌ DynamoDB reserved keyword (`item`) → Used alias (`#it`)
* ❌ Old Lambda response ("Hello from Lambda") → Deployed updated code

---

## 9️⃣ Enabled CORS

* Enabled CORS on `/orders`
* Allowed all methods

---

## 🔟 Deployed API

* Created stage: `dev`
* Deployed API

Example endpoint:

```
https://your-api-id.execute-api.region.amazonaws.com/dev/orders
```

---

## 🧪 Testing (Postman)

### 🔵 GET Orders

```
GET /orders
```

---

### 🟢 Create Order

```json
{
  "item": "Laptop"
}
```

---

### 🟡 Update Order

```json
{
  "orderId": "your-id",
  "timestamp": "your-timestamp",
  "item": "Mobile"
}
```

---

### 🔴 Delete Order

```json
{
  "orderId": "your-id",
  "timestamp": "your-timestamp"
}
```

---

## 🧠 Key Learnings

* Serverless architecture using AWS
* API Gateway ↔ Lambda integration
* DynamoDB composite key design
* Handling reserved keywords in DynamoDB
* Debugging using logs

---

## 🔥 Future Improvements

* Add authentication (JWT / Cognito)
* Add frontend (React)
* Use `/orders/{orderId}`
* Implement pagination instead of scan

---

## 📌 Conclusion

Built a scalable serverless backend using AWS with proper REST API design and full CRUD functionality.

---
