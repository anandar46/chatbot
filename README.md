# Nexus AI - Smart College Chatbot

Nexus AI is a next-generation, highly interactive, scalable, and visually stunning chatbot platform designed for educational institutions. It features an advanced AI assistant powered by OpenAI, a dynamic knowledge base via RAG (Retrieval-Augmented Generation), and real-time chat capabilities.

## 📁 Project Structure

```text
chatbot/
├── client/                 # Next.js Frontend
│   ├── src/app/            # App Router (pages & layouts)
│   ├── package.json        # Frontend dependencies
│   └── tailwind.config.ts  # Tailwind CSS configuration
└── server/                 # Express.js Backend
    ├── src/index.js        # Core server & WebSocket logic
    ├── prisma/             # Database Schema
    ├── .env                # Environment variables
    └── package.json        # Backend dependencies
```

---

## 🚀 Step-by-Step Setup Instructions

### Prerequisites
1. **Node.js**: Ensure you have Node.js v18+ installed on your machine. (Currently, Node is missing in your environment).
2. **PostgreSQL**: Install PostgreSQL locally or use a cloud provider like Supabase or Neon.
3. **API Keys**: You will need an OpenAI API Key and a Pinecone API Key for the RAG architecture.

### 1. Backend Setup (`/server`)

1. Navigate to the server directory:
   ```bash
   cd server
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Update the `.env` file with your actual Database URL, JWT Secret, OpenAI API Key, and Pinecone API Key.
4. Run Prisma to push the schema to your database and generate the client:
   ```bash
   npx prisma db push
   npx prisma generate
   ```
5. Start the development server:
   ```bash
   npm run dev
   ```
   *The server will run on `http://localhost:5000`.*

### 2. Frontend Setup (`/client`)

1. Open a new terminal and navigate to the client directory:
   ```bash
   cd client
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Start the Next.js development server:
   ```bash
   npm run dev
   ```
   *The web application will run on `http://localhost:3000`.*

---

## 🌍 Deployment Guide

This project is structured optimally for a split deployment: Vercel for the Next.js Frontend and Render for the Express/WebSocket Backend.

### 1. Deploying the Database
- **Option 1**: Use **Supabase** or **Neon** to instantly provision a free PostgreSQL database.
- Obtain the Database Connection URL and keep it safe.

### 2. Deploying the Backend (Render)
Render is ideal for WebSocket-heavy Express applications.

1. Push your `server` code to a GitHub repository.
2. Go to [Render](https://render.com) and create a new **Web Service**.
3. Connect your GitHub repository.
4. Set the **Build Command**: `npm install && npx prisma generate`
5. Set the **Start Command**: `npm start`
6. Add all Environment Variables from your `.env` file (including the `DATABASE_URL` from Supabase/Neon).
7. Deploy! Once deployed, copy the Render app URL (e.g., `https://nexus-api.onrender.com`).

### 3. Deploying the Frontend (Vercel)
Vercel is the native platform for Next.js applications.

1. Push your `client` code to a GitHub repository (or use a monorepo approach).
2. Go to [Vercel](https://vercel.com) and click **Add New Project**.
3. Import your GitHub repository. Ensure the "Framework Preset" is Next.js.
4. In the Environment Variables, add your Backend API URL (e.g., `NEXT_PUBLIC_API_URL=https://nexus-api.onrender.com`).
5. Click **Deploy**.

### Future Enhancements for AWS Deployment
If you wish to scale to AWS:
- **Frontend**: Deploy via AWS Amplify.
- **Backend**: Containerize the Express server using Docker and deploy via AWS ECS (Elastic Container Service) with AWS Application Load Balancer (ALB) configured to support WebSockets.
- **Database**: Use Amazon RDS for PostgreSQL.
