# API Introduction

This is the backend API for the Food Ordering project.

- Authentication: Login, Register, Logout
- Account: Get and update personal information
- Dish: Read, Add, Update, Delete dishes
- Media: Upload images
- Test API

> Important note: Please pull the latest code from the GitHub repo regularly, as the API logic may be updated during the video recording process.

> In the `server/.env` file, there is a `COOKIE_MODE` property. Set it to `true` if you want to use cookies for authentication on the server.

## Technologies Used

Node.js + Fastify + Sqlite

## Installation

Just clone this repository, cd into the folder, install the packages, and run `npm run dev`:

```bash
cd server
npm i
npm run dev
```

To run the production build:

```bash
npm run build
npm run start
```

To view the database, open Prisma Studio with the command:

```bash
npx prisma studio
```

It will run at [http://localhost:5555](http://localhost:5555)

The source code contains a `.env` file for configuration. In this file, you can change the backend API port (default is `4000`).

When uploading, images will be stored in the `/uploads` directory inside the `server` folder.

## Response Format

The response format is JSON and always contains a `message` field. It may also include `data` or `errors` fields.

Example of a successful response:

```json
{
  "data": {
    "id": 2,
    "name": "Iphone 11",
    "price": 20000000,
    "description": "Description for iPhone 11",
    "image": "http://localhost:4000/static/bec024f9ea534b7fbf078cb5462b30aa.jpg",
    "createdAt": "2024-03-11T03:51:14.028Z",
    "updatedAt": "2024-03-11T03:51:14.028Z"
  },
  "message": "Product created successfully!"
}
```

If there is an error and the request body is not in the correct format, the server will return a `422` error with details as follows:

Example: The body is missing the `price` field

```json
{
  "message": "A validation error occurred when validating the body...",
  "errors": [
    {
      "code": "invalid_type",
      "expected": "number",
      "received": "undefined",
      "path": ["price"],
      "message": "Required",
      "field": "price"
    }
  ],
  "code": "FST_ERR_VALIDATION",
  "statusCode": 422
}
```

For other errors, the server will return the error in the `message` field, for example:

```json
{
  "message": "Data not found!",
  "statusCode": 404
}
```

## API Details

By default, the API runs at [http://localhost:4000](http://localhost:4000). If you want to change the port, edit the `.env` file.

For standard POST and PUT APIs, the request body must be JSON and must include the header `Content-Type: application/json`.

For image upload APIs, you must send the request as `form-data`.

User authentication is handled via a session token, which is a JWT. The JWT secret key is stored in the `.env` file and is used to create and verify tokens.

For APIs that require user authentication (such as the `Account` group), you need to send the accessToken to the server via the header `Authorization: "Bearer <accessToken>"`

### Test API: Check if the API is working

- `GET /test`: Returns a message if the API is working

### APIs requiring realtime

- `POST /guest/orders`: Create a new order

## Quick Postman Setup

A file named `NextJs Free API.postman_collection.json` is saved in the `server` directory. Just import this file into Postman to get the collection. Then, create a new environment, set the `host` variable to `http://localhost:4000`, and select this environment when calling the API.

## Default Accounts

Admin account: admin@order.com | 123456
User accounts:

- phuminhdat@gmail.com | 123123
- buianhson@gmail.com | 123123
- ngocbichhuynh@gmail.com | 123123
- binhnguyen@gmail.com | 123123
