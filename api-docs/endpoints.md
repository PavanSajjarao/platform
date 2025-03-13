# API Endpoints

## API Structure

```mermaid
graph TB
    subgraph API Endpoints
        API[API Gateway] --> V1[Version 1]
        API --> V2[Version 2]
        
        V1 --> Auth[Authentication]
        V1 --> Project[Project]
        V1 --> Schedule[Schedule]
        V1 --> Task[Task]
        V1 --> Cost[Cost Control]
        
        V2 --> Auth2[Authentication V2]
        V2 --> Project2[Project V2]
        V2 --> Schedule2[Schedule V2]
    end
```

## Endpoint Categories

### 1. Authentication Endpoints

```mermaid
graph LR
    subgraph Auth Endpoints
        Login[POST /auth/login] --> Token[JWT Token]
        Refresh[POST /auth/refresh] --> NewToken[New JWT]
        Logout[POST /auth/logout] --> Status[Success]
        Validate[GET /auth/validate] --> Valid[Token Valid]
    end
```

#### Authentication Routes
- `POST /api/v1/auth/login` - User login
- `POST /api/v1/auth/refresh` - Refresh token
- `POST /api/v1/auth/logout` - User logout
- `GET /api/v1/auth/validate` - Validate token

### 2. Project Endpoints

```mermaid
graph TB
    subgraph Project Endpoints
        Projects[Projects] --> Create[POST /projects]
        Projects --> List[GET /projects]
        Projects --> Get[GET /projects/:id]
        Projects --> Update[PUT /projects/:id]
        Projects --> Delete[DELETE /projects/:id]
        
        Create --> Validation[Input Validation]
        Update --> Validation
    end
```

#### Project Routes
- `POST /api/v1/projects` - Create project
- `GET /api/v1/projects` - List projects
- `GET /api/v1/projects/:id` - Get project
- `PUT /api/v1/projects/:id` - Update project
- `DELETE /api/v1/projects/:id` - Delete project

### 3. Schedule Endpoints

```mermaid
graph TB
    subgraph Schedule Endpoints
        Schedule[Schedule] --> Calendar[Calendar]
        Schedule --> WBS[WBS]
        Schedule --> Resource[Resource]
        
        Calendar --> Events[Events]
        Calendar --> Timeline[Timeline]
        
        WBS --> Structure[Structure]
        WBS --> Dependencies[Dependencies]
        
        Resource --> Assignment[Assignments]
        Resource --> Availability[Availability]
    end
```

#### Schedule Routes
- `GET /api/v1/schedule/calendar` - Get calendar
- `POST /api/v1/schedule/events` - Create event
- `GET /api/v1/schedule/wbs` - Get WBS
- `POST /api/v1/schedule/wbs` - Create WBS item
- `GET /api/v1/schedule/resources` - List resources
- `POST /api/v1/schedule/assignments` - Create assignment

### 4. Task Endpoints

```mermaid
graph LR
    subgraph Task Endpoints
        Tasks[Tasks] --> Create[POST /tasks]
        Tasks --> List[GET /tasks]
        Tasks --> Update[PUT /tasks/:id]
        Tasks --> Status[PUT /tasks/:id/status]
        
        Create --> Validation[Validation]
        Update --> Validation
        Status --> Workflow[Workflow]
    end
```

#### Task Routes
- `POST /api/v1/tasks` - Create task
- `GET /api/v1/tasks` - List tasks
- `PUT /api/v1/tasks/:id` - Update task
- `PUT /api/v1/tasks/:id/status` - Update task status

### 5. Cost Control Endpoints

```mermaid
graph TB
    subgraph Cost Control
        CostSheet[Cost Sheet] --> Create[POST /cost-sheets]
        CostSheet --> List[GET /cost-sheets]
        CostSheet --> Update[PUT /cost-sheets/:id]
        
        Codes[Cost Codes] --> CreateCode[POST /cost-codes]
        Codes --> ListCodes[GET /cost-codes]
        Codes --> UpdateCode[PUT /cost-codes/:id]
    end
```

#### Cost Control Routes
- `POST /api/v1/cost-sheets` - Create cost sheet
- `GET /api/v1/cost-sheets` - List cost sheets
- `PUT /api/v1/cost-sheets/:id` - Update cost sheet
- `POST /api/v1/cost-codes` - Create cost code
- `GET /api/v1/cost-codes` - List cost codes
- `PUT /api/v1/cost-codes/:id` - Update cost code

## API Versioning

```mermaid
graph LR
    subgraph API Versions
        V1[Version 1] --> Stable[Stable]
        V2[Version 2] --> Beta[Beta]
        
        Stable --> Deprecated[Deprecated]
        Beta --> Active[Active]
    end
```

## Response Format

```json
{
  "success": true,
  "data": {
    // Response data
  },
  "meta": {
    "timestamp": "2024-03-13T12:00:00Z",
    "requestId": "uuid",
    "version": "1.0"
  },
  "error": null
}
```

## Error Format

```json
{
  "success": false,
  "data": null,
  "meta": {
    "timestamp": "2024-03-13T12:00:00Z",
    "requestId": "uuid",
    "version": "1.0"
  },
  "error": {
    "code": "ERROR_CODE",
    "message": "Error message",
    "details": {
      // Additional error details
    }
  }
}
``` 