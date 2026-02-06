# Me-API Playground

A RESTful backend system for managing developer profiles and projects with skill-based filtering capabilities.

## Overview

Me-API Playground is designed to manage developer profiles and projects, enabling profile creation, retrieval, and skill-based project filtering. This makes it ideal for:

- Developer portfolio platforms
- Talent discovery systems
- AI-powered profile analysis models

### Integration Capabilities

The API is optimized for integration with:
- Frontend clients (React)
- Pitch models (Predusk)
- AI/LLM-based evaluation systems

## Technology Stack

- **Backend:** Express.js (Node.js)
- **Database:** MongoDB (Mongoose ODM)
- **API Style:** REST
- **Frontend Consumer:** React

## System Architecture

```
Client (React) → REST APIs → Express.js (Routing & Controllers) → MongoDB
                                                                      ↓
                                                            JSON Response
```

- Client (React) communicates via REST APIs
- Express.js handles routing and controllers
- MongoDB stores structured profile documents
- Data is returned in JSON format

## API Endpoints

### Get All Profiles

**Endpoint:** `GET /api/profiles`

**Description:** Fetches all developer profiles stored in the system

**Access:** Public

**Response:** Array of profile objects

---

### Get Profile by ID

**Endpoint:** `GET /api/profiles/:id`

**Description:** Retrieves a single profile using its unique MongoDB ObjectId

**Access:** Public

**Parameters:**
- `id` (path parameter) - MongoDB ObjectId

---

### Create Profile

**Endpoint:** `POST /api/profiles`

**Description:** Creates a new developer profile with skills, projects, and work experience

**Access:** Public

**Request Body Example:**
```json
{
  "name": "David Kim",
  "email": "dkim@fullstack.io",
  "education": "B.S. Engineering, UCLA",
  "skills": ["Next.js", "TypeScript", "Prisma", "PostgreSQL"],
  "projects": [
    {
      "title": "SaaS Starter",
      "description": "Boilerplate for SaaS apps",
      "links": ["https://saas-starter.com"]
    }
  ],
  "work": [
    {
      "company": "StartupX",
      "position": "Fullstack Dev",
      "description": "Built the MVP from scratch."
    }
  ],
  "links": {
    "github": "github.com/dkim",
    "linkedin": "linkedin.com/in/dkim",
    "portfolio": "davidkim.dev"
  }
}
```

---

### Get Projects by Skill

**Endpoint:** `GET /api/projects?skills=Python`

**Description:** Returns projects filtered by a specific skill and associated profile IDs

**Access:** Public

**Query Parameters:**
- `skills` - Technology skill to filter by (e.g., Python, JavaScript, React)

## Route Mapping

```javascript
const { getProfiles, getProfileById, createProfile, getProjects } 
  = require('../controllers/profileController');

router.get('/projects', getProjects);
router.get('/', getProfiles);
router.get('/:id', getProfileById);
router.post('/', createProfile);
```

## Database Schema

The system uses a single `Profile` collection with nested sub-documents.

### Schema Field Specification

| Field | Type | Storage Method | Description |
|-------|------|----------------|-------------|
| `id` | ObjectId | Auto-generated | Unique primary key for each profile |
| `name` | String | Direct Field | Required full name of the user |
| `email` | String | Indexed Field | Unique identifier for contact or login |
| `skills` | Array | List of Strings | Technology skills (e.g., JavaScript, React) |
| `projects` | Array | Sub-documents | Project title, description, and links |
| `work` | Array | Sub-documents | Professional experience history |
| `links` | Object | Nested Object | GitHub, LinkedIn, and Portfolio URLs |
| `timestamps` | Date | Auto-generated | createdAt and updatedAt fields |

### Sample Document

```json
{
  "_id": "507f1f77bcf86cd799439011",
  "name": "David Kim",
  "email": "dkim@fullstack.io",
  "education": "B.S. Engineering, UCLA",
  "skills": ["Next.js", "TypeScript", "Prisma", "PostgreSQL"],
  "projects": [
    {
      "title": "SaaS Starter",
      "description": "Boilerplate for SaaS apps",
      "links": ["https://saas-starter.com"]
    }
  ],
  "work": [
    {
      "company": "StartupX",
      "position": "Fullstack Dev",
      "description": "Built the MVP from scratch."
    }
  ],
  "links": {
    "github": "github.com/dkim",
    "linkedin": "linkedin.com/in/dkim",
    "portfolio": "davidkim.dev"
  },
  "createdAt": "2024-01-15T10:30:00.000Z",
  "updatedAt": "2024-01-15T10:30:00.000Z"
}
```

## AI and Pitch Model Compatibility

This API is suitable for AI-driven systems because:

- **Structured and predictable schema** - Consistent data format for reliable processing
- **Skill-based filtering** - Enables semantic matching and talent discovery
- **Nested documents** - Ideal for embedding generation in ML models
- **Clean separation of concerns** - Clear distinction between profiles and projects

## Installation

```bash
# Clone the repository
git clone <repository-url>

# Navigate to project directory
cd me-api-playground

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env

# Start the server
npm start
```

## Environment Variables

Create a `.env` file in the root directory:

```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/me-api
NODE_ENV=development
```

## Usage

### Starting the Server

```bash
npm start
```

The API will be available at `http://localhost:5000`

### Development Mode

```bash
npm run dev
```

## Use Cases

- **Developer Portfolio Platforms** - Showcase developer skills and projects
- **Talent Discovery Systems** - Filter and match developers based on skills
- **AI Profile Analysis** - Feed structured data to ML models for evaluation
- **Investor Pitch Evaluations** - Analyze developer capabilities and experience

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License.

## Contact

For questions or support, please open an issue in the repository.

---

**Assessment Submission** | RESTful Profile Project Management API
