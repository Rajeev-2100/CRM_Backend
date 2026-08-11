# CRM Backend

This is the backend service for the CRM application. It is built with Node.js, Express, and MongoDB using Mongoose. The API handles sales agents, leads, comments, tags, and reporting data used by the frontend dashboard and management screens.

## Features

- Manage sales agents
- Create, read, update, and delete leads
- Add comments to leads
- Track lead status and reporting metrics
- Seed bulk data for demo or testing purposes
- Expose tag data for CRM filtering and categorization

## Tech Stack

- Node.js
- Express.js
- MongoDB
- Mongoose
- CORS
- dotenv

## Project Structure

```bash
CRM_Backend/
├── db/
│   └── db.connect.js
├── models/
│   ├── comment.model.js
│   ├── lead.model.js
│   ├── salesAgent.model.js
│   └── tag.model.js
├── .env
├── index.js
├── package.json
└── readme.md
```

## Prerequisites

Before running the backend, make sure you have:

- Node.js installed
- MongoDB running locally or a valid MongoDB connection string
- A `.env` file configured with your database URL

## Environment Variables

Create a `.env` file in the backend root with the following:

```env
MONGO_URL=mongodb://localhost:27017/crm_db
```

If you're using a remote MongoDB Atlas connection, replace the value with your connection string.

## Installation

From the backend folder:

```bash
npm install
```

## Running the Server

Start the backend with:

```bash
node index.js
```

The server listens on:

```bash
http://localhost:3001
```

## API Endpoints

### Sales Agents

- `POST /agents` - Create a new sales agent
- `GET /agents` - Get all sales agents
- `DELETE /agents/:salesPerson` - Delete an agent by name
- `POST /api/bulk-agents` - Insert multiple agents

### Leads

- `POST /leads` - Create a lead
- `POST /seed/leads` - Seed leads in bulk
- `GET /leads` - Get all leads with populated sales agent details
- `GET /leads/specific` - Get a simplified lead list
- `GET /leads/status-count` - Get lead counts grouped by status
- `GET /leads/:leadStatus` - Get leads by status
- `PUT /leads/:leadId` - Update a lead
- `DELETE /leads/:leadId` - Delete a lead
- `POST /api/bulk-leads` - Insert multiple leads

### Comments

- `POST /leads/:id/comments` - Add a comment to a lead
- `GET /leads/:leadId/comments` - Get all comments for a lead
- `POST /api/bulk-comments` - Insert multiple comments

### Tags

- `GET /tags` - Get all tags
- `POST /api/bulk-tags` - Insert multiple tags

### Reports

- `GET /report/last-week` - Fetch leads closed in the last 7 days
- `GET /report/pipeline` - Get total open leads in pipeline

## Database Models

### SalesAgent

```js
{
  name: String,
  email: String,
  createdAt: Date
}
```

### Lead

```js
{
  name: String,
  source: String,
  salesAgent: ObjectId,
  status: String,
  tags: [String],
  timeToClose: Number,
  priority: String,
  createdAt: Date,
  updatedAt: Date,
  closedAt: Date
}
```

### Comment

```js
{
  lead: ObjectId,
  author: ObjectId,
  commentText: String,
  createdAt: Date
}
```

### Tag

```js
{
  name: String,
  createdAt: Date
}
```

## Notes

- The backend uses CORS with `origin: "*"` to allow frontend requests during development.
- The database connection is initialized when the server starts via `initializeDatabase()`.
- Some routes return 201 status codes even for retrieval routes; this is part of the current implementation and may be cleaned up in future versions.
- There are no automated tests configured in the current project setup.

## Future Improvements

- Add validation middleware and route-level error handling
- Add authentication and authorization
- Add proper environment-based configuration
- Add automated tests for API endpoints
- Standardize response codes and payload formats

## License

This project is currently using the ISC license as defined in `package.json`.
