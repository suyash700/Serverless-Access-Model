<img width="1910" height="911" alt="Screenshot 2026-04-26 200827" src="https://github.com/user-attachments/assets/8353248a-c93d-40d8-91b8-8da4ee6bbf6b" /># 🎓 College API – Student Management (AWS Serverless)

This module was implemented as part of the practical to manage student records using a serverless architecture.

---

## 🧠 Architecture

Client → API Gateway → Lambda → DynamoDB

---

## 🗄️ DynamoDB Table: Students

* Table Name: **Students**
* Partition Key: `studentId` (String)

---

## 📊 Table Attributes

| Attribute | Type   | Description               |
| --------- | ------ | ------------------------- |
| studentId | String | Unique ID of student      |
| name      | String | Student name              |
| branch    | String | Department (e.g., IT, CS) |
| year      | Number | Academic year             |

---

## 🔧 Steps Performed

### 1️⃣ Created Students Table

* Open DynamoDB → Create Table
* Table name: `Students`
* Partition key: `studentId`

  <img width="1919" height="905" alt="Screenshot 2026-04-26 194723" src="https://github.com/user-attachments/assets/3d58c2e2-09f7-4a80-9f12-4bf67a7ff91c" />

  <img width="1916" height="902" alt="Screenshot 2026-04-26 194814" src="https://github.com/user-attachments/assets/55672321-cb66-4b3c-ae3f-35421e004fe2" />


<img width="1912" height="864" alt="Screenshot 2026-04-26 194856" src="https://github.com/user-attachments/assets/fe117d5c-d05d-4eea-a99e-27e5d676ad1e" />

---

### 2️⃣ Created Lambda Functions

* `createStudent`
* `getStudents`
* `updateStudent`
* `deleteStudent`

<img width="1913" height="884" alt="Screenshot 2026-04-26 195514" src="https://github.com/user-attachments/assets/9b0e827f-83ed-4cc4-bb97-a41d66f6db22" />

<img width="1919" height="898" alt="Screenshot 2026-04-26 195559" src="https://github.com/user-attachments/assets/6dfaeba6-93b9-4320-af04-e6cdfb5f153a" />


---

### 3️⃣ Implemented Lambda Logic

#### ✔ createStudent

* Accepts student details
* Generates unique `studentId`
* Stores record in DynamoDB

---

#### ✔ getStudents

* Retrieves all students using `scan()`

---

#### ✔ updateStudent

* Updates student details using `update_item()`

---

#### ✔ deleteStudent

* Deletes student using `studentId`

---

### 4️⃣ Created API Gateway (College API)

* Created REST API
* Created resource:

```id="l2t3bp"
/students
```

<img width="1919" height="829" alt="Screenshot 2026-04-26 200024" src="https://github.com/user-attachments/assets/27d0be66-ca14-4942-85c6-20669947396b" />

---

### 5️⃣ Added Methods

| Method | Endpoint  | Lambda        |
| ------ | --------- | ------------- |
| GET    | /students | getStudents   |
| POST   | /students | createStudent |
| PUT    | /students | updateStudent |
| DELETE | /students | deleteStudent |


<img width="1918" height="894" alt="Screenshot 2026-04-26 200252" src="https://github.com/user-attachments/assets/7b03bf94-ddeb-4c25-a68a-6170885fdbae" />

<img width="1912" height="889" alt="Screenshot 2026-04-26 200321" src="https://github.com/user-attachments/assets/e41a69b8-d58a-447a-9c77-fe7957645959" />


<img width="1917" height="883" alt="Screenshot 2026-04-26 200748" src="https://github.com/user-attachments/assets/6fe8463a-45f8-43fb-b968-762fbdca443f" />



<img width="1919" height="881" alt="Screenshot 2026-04-26 200850" src="https://github.com/user-attachments/assets/651d4874-f938-43d0-a0bc-052f5db3ef83" />

✔ Enabled Lambda Proxy Integration

---

### 6️⃣ Enabled CORS

* Enabled for all methods

<img width="1917" height="911" alt="Screenshot 2026-04-26 200927" src="https://github.com/user-attachments/assets/726c4e74-0e12-41bd-a4b9-27352d9927b4" />

---

### 7️⃣ Deployed API

* Stage: `dev`

---

## 🧪 Testing (Postman)

### 🔵 GET Students

```id="t4cmr6"
GET /students
```

---

### 🟢 Create Student

```json id="th1pc9"
{
  "name": "Suyash",
  "branch": "IT",
  "year": 3
}
```

---

### 🟡 Update Student

```json id="k4svul"
{
  "studentId": "your-id",
  "name": "Updated Name",
  "branch": "CS",
  "year": 4
}
```

---

### 🔴 Delete Student

```json id="sh3gxf"
{
  "studentId": "your-id"
}
```

---

## 💡 Key Learnings

* Designed a student management system using serverless architecture
* Implemented CRUD operations using Lambda and DynamoDB
* Integrated API Gateway with Lambda using proxy integration
* Understood real-world API design

---
