Neeche **clean + proper API docs + Postman step-by-step testing flow** de raha hoon. Isme **har endpoint clickable format + full testing sequence + cookies handling** sab included hai.

---

# 🚀 Base URL

```
http://localhost:8000
```

---

# 🏥 1. Health Check

### 🔗 Endpoint

👉 [http://localhost:8000/health](http://localhost:8000/health)

### Method

```
GET
```

### Test (curl)

```bash
curl http://localhost:8000/health
```

### Expected Response

```json
{
  "status": "ok",
  "uptime": 12345
}
```

---

# 👤 2. User APIs (/api/v1/user)

## 🔗 Endpoints

* POST [http://localhost:8000/api/v1/user/signup](http://localhost:8000/api/v1/user/signup)
* POST [http://localhost:8000/api/v1/user/signin](http://localhost:8000/api/v1/user/signin)
* POST [http://localhost:8000/api/v1/user/signout](http://localhost:8000/api/v1/user/signout)
* GET  [http://localhost:8000/api/v1/user/profile](http://localhost:8000/api/v1/user/profile)
* PATCH [http://localhost:8000/api/v1/user/profile](http://localhost:8000/api/v1/user/profile)
* PATCH [http://localhost:8000/api/v1/user/change-password](http://localhost:8000/api/v1/user/change-password)
* DELETE [http://localhost:8000/api/v1/user/account](http://localhost:8000/api/v1/user/account)

---

## 🧪 Step-by-step Postman Flow (IMPORTANT)

### ✅ STEP 1: Signup

**POST**

```
http://localhost:8000/api/v1/user/signup
```

Body (JSON):

```json
{
  "name": "Test User",
  "email": "test@example.com",
  "password": "Test@1234"
}
```

---

### ✅ STEP 2: Signin (🔥 COOKIE SAVE HOGA)

**POST**

```
http://localhost:8000/api/v1/user/signin
```

Body:

```json
{
  "email": "test@example.com",
  "password": "Test@1234"
}
```

### 👉 Postman setting:

* Go to **Cookies tab**
* Check domain `localhost`
* Cookie automatically save ho jayegi

---

### ✅ STEP 3: Profile (AUTH REQUIRED)

**GET**

```
http://localhost:8000/api/v1/user/profile
```

👉 No headers needed (cookie auto send)

---

### ✅ STEP 4: Update Profile

**PATCH**

```
http://localhost:8000/api/v1/user/profile
```

Body (form-data):

```
name = Updated Name
```

---

### ✅ STEP 5: Change Password

**PATCH**

```
http://localhost:8000/api/v1/user/change-password
```

Body:

```json
{
  "currentPassword": "Test@1234",
  "newPassword": "NewPass@1234"
}
```

---

### ✅ STEP 6: Signout

**POST**

```
http://localhost:8000/api/v1/user/signout
```

---

### ❌ STEP 7: Delete Account

**DELETE**

```
http://localhost:8000/api/v1/user/account
```

---

# 📚 3. Course APIs (/api/v1/course)

## 🔗 Endpoints

* GET [http://localhost:8000/api/v1/course/published](http://localhost:8000/api/v1/course/published)
* GET [http://localhost:8000/api/v1/course/search?query=js](http://localhost:8000/api/v1/course/search?query=js)
* POST [http://localhost:8000/api/v1/course](http://localhost:8000/api/v1/course)
* GET [http://localhost:8000/api/v1/course](http://localhost:8000/api/v1/course)
* GET [http://localhost:8000/api/v1/course/c/:courseId](http://localhost:8000/api/v1/course/c/:courseId)
* PATCH [http://localhost:8000/api/v1/course/c/:courseId](http://localhost:8000/api/v1/course/c/:courseId)
* GET [http://localhost:8000/api/v1/course/c/:courseId/lectures](http://localhost:8000/api/v1/course/c/:courseId/lectures)
* POST [http://localhost:8000/api/v1/course/c/:courseId/lectures](http://localhost:8000/api/v1/course/c/:courseId/lectures)

---

## 🧪 Testing Flow

### 1. Public courses

```
GET http://localhost:8000/api/v1/course/published
```

---

### 2. Search

```
GET http://localhost:8000/api/v1/course/search?query=javascript
```

---

### 3. Create Course (INSTRUCTOR ONLY)

```
POST http://localhost:8000/api/v1/course
```

Body (form-data):

```
title = My Course
description = Course description
thumbnail = file.jpg
```

---

### 4. My Courses

```
GET http://localhost:8000/api/v1/course
```

---

### 5. Course Detail

```
GET http://localhost:8000/api/v1/course/c/<courseId>
```

---

### 6. Update Course

```
PATCH http://localhost:8000/api/v1/course/c/<courseId>
```

Body:

```
title = Updated Title
```

---

### 7. Lectures

```
GET http://localhost:8000/api/v1/course/c/<courseId>/lectures
```

---

### 8. Add Lecture

```
POST http://localhost:8000/api/v1/course/c/<courseId>/lectures
```

Body (form-data):

```
title = Lecture 1
video = file.mp4
```

---

# 📊 4. Progress APIs (/api/v1/progress)

## 🔗 Endpoints

* GET [http://localhost:8000/api/v1/progress/:courseId](http://localhost:8000/api/v1/progress/:courseId)
* PATCH [http://localhost:8000/api/v1/progress/:courseId/lectures/:lectureId](http://localhost:8000/api/v1/progress/:courseId/lectures/:lectureId)
* PATCH [http://localhost:8000/api/v1/progress/:courseId/complete](http://localhost:8000/api/v1/progress/:courseId/complete)
* PATCH [http://localhost:8000/api/v1/progress/:courseId/reset](http://localhost:8000/api/v1/progress/:courseId/reset)

---

## 🧪 Tests

### Get Progress

```
GET /api/v1/progress/<courseId>
```

---

### Mark Lecture Complete

```json
PATCH /lectures/<lectureId>
{
  "completed": true
}
```

---

### Complete Course

```
PATCH /complete
```

---

### Reset Progress

```
PATCH /reset
```

---

# 💳 5. Purchase APIs (/api/v1/purchase)

## 🔗 Endpoints

* POST [http://localhost:8000/api/v1/purchase/checkout/create-checkout-session](http://localhost:8000/api/v1/purchase/checkout/create-checkout-session)
* POST [http://localhost:8000/api/v1/purchase/webhook](http://localhost:8000/api/v1/purchase/webhook)
* GET [http://localhost:8000/api/v1/purchase/course/:courseId/detail-with-status](http://localhost:8000/api/v1/purchase/course/:courseId/detail-with-status)
* GET [http://localhost:8000/api/v1/purchase](http://localhost:8000/api/v1/purchase)

---

## 🧪 Flow

### Create Checkout Session

```json
POST /checkout/create-checkout-session
{
  "courseId": "<courseId>"
}
```

---

### Purchase Status

```
GET /course/<courseId>/detail-with-status
```

---

### All Purchases

```
GET /api/v1/purchase
```

---

# 💰 6. Razorpay APIs (/api/v1/razorpay)

## 🔗 Endpoints

* POST [http://localhost:8000/api/v1/razorpay/create-order](http://localhost:8000/api/v1/razorpay/create-order)
* POST [http://localhost:8000/api/v1/razorpay/verify-payment](http://localhost:8000/api/v1/razorpay/verify-payment)

---

### Create Order

```json
{
  "courseId": "<courseId>",
  "amount": 999
}
```

---

### Verify Payment

```json
{
  "razorpay_order_id": "order_xxx",
  "razorpay_payment_id": "pay_xxx",
  "razorpay_signature": "signature"
}
```

---

# 🎬 7. Media Upload (/api/v1/media)

## 🔗 Endpoint

```
POST http://localhost:8000/api/v1/media/upload-video
```

Body (form-data):

```
file = video.mp4
```

---

# ⚡ FULL TESTING FLOW (IMPORTANT)

👉 Postman sequence:

1. Signup
2. Signin (cookie save)
3. Profile check
4. Create course (instructor)
5. Add lecture
6. Create checkout / razorpay order
7. Track progress
8. Logout

---

# 🔥 PRO TIP (Postman Setup)

### ✔ Enable:

* Cookies ON (auto session handling)
* Environment variable:

```
base_url = http://localhost:8000
```

Then use:

```
{{base_url}}/api/v1/user/signin
```

---

Agar tu chahe toh main next step me:
✅ Postman Collection JSON file
✅ Swagger/OpenAPI docs
✅ ya frontend integration flow (React/Next.js)

bhi bana dunga.
