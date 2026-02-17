---
id: frontend-doc-generation
name: Frontend Documentation Generation
description: Generate frontend development documentation based on backend API design
invoked_by: developer
triggers:
  - "#frontend-doc"
dependencies:
  - workspace/context/architecture.yaml
  - workspace/artifacts/{change-id}/design.md
outputs:
  - frontend-api-doc (markdown)
---

# Frontend Documentation Generation Skill

Generate frontend development documentation based on backend API design. This skill helps bridge the gap between backend implementation and frontend development by providing clear API documentation, interaction flows, and integration guidelines.

## Usage

This skill is invoked by: **Developer** (via `#frontend-doc` command)

## Knowledge Dependencies

Before executing this skill, load the following knowledge files:

| Path | Description | Required |
|------|-------------|----------|
| `workspace/context/architecture.yaml` | Architecture design | Yes |
| `workspace/artifacts/{change-id}/design.md` | Detailed design document | Yes (if exists) |
| `workspace/context/requirements.yaml` | Requirements context | Yes (if exists) |

## Capabilities

### Requirement Background
- Extract business context from requirements
- Summarize user stories and use cases
- Provide feature purpose explanation

### API Interface Design
- List all related API endpoints
- Document HTTP methods and URL patterns
- Identify API groupings by feature

### Interaction Flow
- Generate frontend-backend interaction diagrams
- Document request/response flow
- Create mermaid sequence diagrams

### Integration Suggestions
- Identify special interaction patterns
- Provide state management recommendations
- Document error handling strategies

## Execution

When invoked, perform these steps:

1. **Load Context**: Read architecture design and requirements
2. **Identify APIs**: Extract API endpoints from design documents
3. **Analyze Flow**: Understand the interaction patterns
4. **Generate Doc**: Create structured frontend documentation
5. **Add Diagrams**: Generate mermaid diagrams for flows
6. **Review Output**: Validate completeness and accuracy

## Input Parameters

| Parameter | Description | Required |
|-----------|-------------|----------|
| `scope` | Specific API or feature to document | No (defaults to all) |
| `change-id` | The change/feature identifier | Yes |

## Output Format

The generated documentation follows this structure:

```markdown
# Frontend API Documentation: {Feature Name}

## 1. Requirement Background

### Business Context
[Brief description of the business need]

### User Stories
- As a [user type], I want to [action] so that [benefit]

---

## 2. API Interface Design

### API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/v1/resource` | Get resource list |
| POST | `/api/v1/resource` | Create new resource |
| PUT | `/api/v1/resource/{id}` | Update resource |
| DELETE | `/api/v1/resource/{id}` | Delete resource |

### API Grouping
- **Resource Management**: CRUD operations for resources
- **Query Operations**: Search and filter APIs

---

## 3. Frontend-Backend Interaction Flow

### Main Flow

\`\`\`mermaid
sequenceDiagram
    participant User
    participant Frontend
    participant Backend
    participant Database

    User->>Frontend: Trigger action
    Frontend->>Backend: API Request
    Backend->>Database: Query/Update
    Database-->>Backend: Result
    Backend-->>Frontend: Response
    Frontend-->>User: Display result
\`\`\`

### Flow Description
1. User initiates action in the frontend
2. Frontend sends request to backend API
3. Backend processes request and interacts with database
4. Backend returns response to frontend
5. Frontend updates UI based on response

---

## 4. Integration Suggestions

> Note: This section is included only when special interaction patterns exist.

### Special Considerations
- [List any special handling requirements]

### State Management
- [Recommendations for frontend state management]

### Error Handling
- [Suggested error handling patterns]

### Performance Considerations
- [Any caching or optimization suggestions]
```

## Example Invocation

```
User: #frontend-doc for user-management feature
Developer: [Generates frontend documentation for user management APIs]
```

## Output Location

Generated documents are saved to:
- `workspace/artifacts/{change-id}/frontend-api-doc.md`

## Notes

- This skill focuses on API interface documentation, not implementation details
- Request parameters and response formats are intentionally omitted (backend handles detailed API specs)
- Use mermaid syntax for all diagrams to ensure compatibility with markdown viewers
