# API Authentication using Axios

This project demonstrates **API authentication** using four different methods with Axios:

1. **No Authentication**
2. **Basic Authentication**
3. **API Key Authentication**
4. **Bearer Token Authentication**

---

## 🏃 Usage

1. Clone the repository.

2. Install dependencies:

``` bash
npm install
```

3. Run the server:

```bash
nodemon solution.js
```

4. Visit the following routes in your browser:

  **http://localhost:3000/**

   1. **/noAuth**

   2. **/basicAuth**

   3. **/apiKey**

   4. **/bearerToken**

---

## 🚀 Prerequisites

Before running the project, you need to register and generate your authentication credentials.

### 1. Register User
Register your **username** and **password** with the API:

**POST** `https://secrets-api.appbrewery.com/register`

**Body:**
```json
{
  "username": "your-username",
  "password": "your-password"
}
```

### 2. Generate API Key

To get your API Key, call:

GET https://secrets-api.appbrewery.com/generate-api-key

### 3. Get Bearer Token

To obtain your Bearer Token, call:

POST https://secrets-api.appbrewery.com/get-auth-token

**Body:**
```json
{
  "username": "your-username",
  "password": "your-password"
}
```

---

## 🔑 Authentication Methods with Code Examples

Below are examples using Express.js + Axios for different authentication methods.

### 1. No Authentication

**A request to a public endpoint without any credentials.**

```js
app.get("/noAuth", async (req, res) => {
  try {
    const result = await axios.get(API_URL + "/random");
    res.render("index.ejs", { content: JSON.stringify(result.data) });
  } catch (error) {
    res.status(404).send(error.message);
  }
});
```

### 2. Basic Authentication

**Uses username:password encoded in Base64 automatically by Axios.**
```js
app.get("/basicAuth", async (req, res) => {
  try {
    const result = await axios.get(API_URL + "/all?page=2", {
      auth: {
        username: yourUsername,
        password: yourPassword,
      },
    });
    res.render("index.ejs", { content: JSON.stringify(result.data) });
  } catch (error) {
    res.status(404).send(error.message);
  }
});
```

### 3. API Key Authentication

**Sends the API key as a query parameter.**

```js
app.get("/apiKey", async (req, res) => {
  try {
    const result = await axios.get(API_URL + "/filter", {
      params: {
        score: 5,
        apiKey: yourAPIKey,
      },
    });
    res.render("index.ejs", { content: JSON.stringify(result.data) });
  } catch (error) {
    res.status(404).send(error.message);
  }
});
```

### 4. Bearer Token Authentication

**Sends the Bearer Token in the request headers.**

```js
const config = {
  headers: { Authorization: `Bearer ${yourBearerToken}` },
};

app.get("/bearerToken", async (req, res) => {
  try {
    const result = await axios.get(API_URL + "/secrets/2", config);
    res.render("index.ejs", { content: JSON.stringify(result.data) });
  } catch (error) {
    res.status(404).send(error.message);
  }
});
```
---

## 📦 Tech Stack

**Axios – for HTTP requests**

**Express.js – backend framework**

**EJS – template engine**

---
## 📌 Notes

**Replace yourUsername, yourPassword, yourAPIKey, and yourBearerToken with the values you obtained during registration.**

**Keep your credentials private and never commit them to version control.**
