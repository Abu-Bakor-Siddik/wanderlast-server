# Wanderlast Server

The backend REST API for **Wanderlast**, a travel destination booking platform. Built with Express.js and MongoDB, it handles destination listings and bookings, and verifies authentication tokens issued by the Wanderlast client (via Better Auth JWKS).

## Tech Stack

- **Runtime:** Node.js
- **Framework:** Express 5
- **Database:** MongoDB (MongoDB Atlas)
- **Auth:** JWT verification via `jose-cjs`, validated against the client app's Better Auth JWKS endpoint
- **Deployment:** Vercel

## Features

- CRUD operations for travel destinations
- Booking creation, lookup by user, and deletion
- Protected routes secured with bearer token verification
- CORS enabled for cross-origin requests from the client app

## API Endpoints

| Method | Endpoint | Auth Required | Description |
|--------|----------|:--------------:|-------------|
| GET | `/` | No | Health check |
| GET | `/featured` | No | Get 4 featured destinations |
| GET | `/destination` | No | Get all destinations |
| POST | `/destination` | No | Create a new destination |
| GET | `/destination/:id` | Yes | Get a single destination by ID |
| PATCH | `/destination/:id` | Yes | Update a destination by ID |
| DELETE | `/destination/:id` | Yes | Delete a destination by ID |
| GET | `/booking/:userId` | No | Get all bookings for a user |
| POST | `/booking` | Yes | Create a new booking |
| DELETE | `/booking/:bookingId` | Yes | Delete a booking by ID |

> Protected routes expect an `Authorization: Bearer <token>` header, where `<token>` is a JWT issued by the client app's Better Auth instance.

## Environment Variables

Create a `.env` file in the project root with the following variables:

```env
PORT=5000
MONGODB_URI=your_mongodb_connection_string
CLIENT_URL=https://your-client-app-url.com
```

- `PORT` — Port the server listens on
- `MONGODB_URI` — MongoDB Atlas connection string
- `CLIENT_URL` — Base URL of the client app; used to fetch the JWKS at `${CLIENT_URL}/api/auth/jwks` for token verification

## Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/Abu-Bakor-Siddik/wanderlast-server.git
   cd wanderlast-server
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**

   Create a `.env` file as described above.

4. **Run the server**
   ```bash
   node index.js
   ```

   The server will start on the port specified in your `.env` file.

## Deployment

This project is configured for deployment on **Vercel** via `vercel.json`, which routes all incoming requests to `index.js`. Make sure to add the environment variables (`MONGODB_URI`, `CLIENT_URL`, `PORT`) in your Vercel project settings before deploying.

## Related Repositories

- Client app: *(add link to the Wanderlast frontend repository here)*

## License

This project is currently unlicensed. Add a license of your choice if you plan to open source it.
