# Secure Whisper

A secure real-time messaging application built with React, TypeScript, Node.js, Express, MongoDB, JWT authentication, WebSockets, and AES-256-GCM encrypted message storage.

> Note: message encryption is performed on the server using an environment-held key. This is encrypted messaging, but it is **not true end-to-end encryption (E2EE)** because the server can decrypt messages.

## Features
- User registration and login
- JWT-based authentication
- Real-time messaging with WebSockets
- Friend requests and friend management
- AES-256-GCM encrypted message content
- Message reactions, replies, read/seen state and file metadata
- React + TypeScript frontend
- MongoDB/Mongoose backend
- Responsive UI with Tailwind CSS and shadcn/ui components
- Render deployment configuration

## Tech Stack
### Frontend
React 18, TypeScript, Vite, React Router, TanStack Query, Tailwind CSS, shadcn/ui, Radix UI.

### Backend
Node.js, Express.js, MongoDB, Mongoose, JWT, bcryptjs, ws, dotenv.

## Architecture
```text
React + TypeScript + Vite
          |
          | HTTP / WebSocket
          v
Express + Node.js WebSocket Server
          |
          +---- JWT authentication
          +---- AES-256-GCM encryption/decryption
          +---- Friend/message APIs
          |
          v
      MongoDB
```

## Project Structure
```text
Secure-Whisper/
├── src/                  # React frontend
│   ├── components/       # Reusable UI components
│   ├── hooks/            # React hooks
│   ├── lib/              # API/client utilities
│   └── pages/            # Application pages
├── server/
│   ├── models/           # MongoDB models
│   ├── index.js          # Express + WebSocket server
│   ├── db.js             # Database utilities
│   └── generate-keys.js  # Key-generation utility
├── public/
├── package.json
├── render.yaml
└── DEPLOYMENT.md
```

## Local Setup
1. Install Node.js and MongoDB.
2. Install frontend dependencies:
   `npm install`
3. Install backend dependencies:
   `cd server && npm install`
4. Create `server/.env` from `server/.env.example` and set strong secrets.
5. Start the backend with `npm start` from `server/`.
6. Start the frontend with `npm run dev` from the project root.

Never commit `.env`, database files, generated secrets, or other private credentials.

## Environment Variables
```env
PORT=4000
JWT_SECRET=your_strong_jwt_secret
ENCRYPTION_KEY=your_32_byte_encryption_key
MONGODB_URI=mongodb://127.0.0.1:27017/securewhisper
```

## Security Notes
- Passwords are hashed with bcrypt rather than stored as plaintext.
- Authentication uses signed JWT tokens.
- Message content is encrypted with AES-256-GCM before database storage.
- Secrets are supplied through environment variables.
- For production, use strong randomly generated secrets and managed TLS/HTTPS/WSS.

## Limitations and Future Improvements
- Move encryption to the client for genuine E2EE.
- Add public-key key exchange and per-conversation keys.
- Improve attachment encryption and secure key management.
- Add stronger production security controls such as rate limiting, CSRF protection where applicable, security headers, and audit logging.
- Add automated tests and CI/CD checks.

## Deployment
The repository includes `render.yaml` and `DEPLOYMENT.md` for deployment configuration.

## License
MIT License.
