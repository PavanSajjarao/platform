# Database Schema

## Database Architecture

```mermaid
graph TB
    subgraph MongoDB Cluster
        Primary[(Primary DB)]
        Secondary1[(Secondary 1)]
        Secondary2[(Secondary 2)]
        
        Primary --> Secondary1
        Primary --> Secondary2
    end
    
    subgraph Collections
        Users[Users Collection]
        Projects[Projects Collection]
        Tasks[Tasks Collection]
        Schedule[Schedule Collection]
        Cost[Cost Collection]
    end
```

## Collection Schemas

### 1. Users Collection

```mermaid
graph LR
    subgraph User Schema
        User[User] --> ID[_id]
        User --> Email[email]
        User --> Name[name]
        User --> Roles[roles]
        User --> Status[status]
        User --> Created[createdAt]
        User --> Updated[updatedAt]
        
        Roles --> Admin[admin]
        Roles --> Manager[manager]
        Roles --> User[user]
    end
```

#### Schema Definition
```typescript
interface User {
  _id: ObjectId;
  email: string;
  name: string;
  roles: string[];
  status: 'active' | 'inactive';
  createdAt: Date;
  updatedAt: Date;
}
```

### 2. Projects Collection

```mermaid
graph TB
    subgraph Project Schema
        Project[Project] --> ID[_id]
        Project --> Name[name]
        Project --> Description[description]
        Project --> Status[status]
        Project --> StartDate[startDate]
        Project --> EndDate[endDate]
        Project --> Manager[manager]
        Project --> Team[team]
        
        Status --> Planning[planning]
        Status --> Active[active]
        Status --> Completed[completed]
        Status --> Cancelled[cancelled]
    end
```

#### Schema Definition
```typescript
interface Project {
  _id: ObjectId;
  name: string;
  description: string;
  status: 'planning' | 'active' | 'completed' | 'cancelled';
  startDate: Date;
  endDate: Date;
  manager: ObjectId; // Reference to User
  team: ObjectId[]; // References to Users
}
```

### 3. Tasks Collection

```mermaid
graph TB
    subgraph Task Schema
        Task[Task] --> ID[_id]
        Task --> Title[title]
        Task --> Description[description]
        Task --> Status[status]
        Task --> Priority[priority]
        Task --> AssignedTo[assignedTo]
        Task --> Project[project]
        Task --> Dependencies[dependencies]
        
        Status --> Todo[todo]
        Status --> InProgress[in_progress]
        Status --> Review[review]
        Status --> Done[done]
    end
```

#### Schema Definition
```typescript
interface Task {
  _id: ObjectId;
  title: string;
  description: string;
  status: 'todo' | 'in_progress' | 'review' | 'done';
  priority: 'low' | 'medium' | 'high';
  assignedTo: ObjectId; // Reference to User
  project: ObjectId; // Reference to Project
  dependencies: ObjectId[]; // References to Tasks
}
```

### 4. Schedule Collection

```mermaid
graph TB
    subgraph Schedule Schema
        Schedule[Schedule] --> ID[_id]
        Schedule --> Project[project]
        Schedule --> WBS[wbs]
        Schedule --> Resources[resources]
        Schedule --> Timeline[timeline]
        
        WBS --> Items[items]
        WBS --> Dependencies[dependencies]
        
        Resources --> Assignments[assignments]
        Resources --> Availability[availability]
    end
```

#### Schema Definition
```typescript
interface Schedule {
  _id: ObjectId;
  project: ObjectId; // Reference to Project
  wbs: {
    items: WBSItem[];
    dependencies: WBSDependency[];
  };
  resources: {
    assignments: ResourceAssignment[];
    availability: ResourceAvailability[];
  };
  timeline: {
    startDate: Date;
    endDate: Date;
    milestones: Milestone[];
  };
}
```

### 5. Cost Collection

```mermaid
graph TB
    subgraph Cost Schema
        CostSheet[Cost Sheet] --> ID[_id]
        CostSheet --> Project[project]
        CostSheet --> Items[items]
        CostSheet --> Budget[budget]
        CostSheet --> Actual[actual]
        
        Items --> Code[costCode]
        Items --> Amount[amount]
        Items --> Category[category]
    end
```

#### Schema Definition
```typescript
interface CostSheet {
  _id: ObjectId;
  project: ObjectId; // Reference to Project
  items: {
    costCode: string;
    amount: number;
    category: string;
  }[];
  budget: {
    total: number;
    breakdown: Record<string, number>;
  };
  actual: {
    total: number;
    breakdown: Record<string, number>;
  };
}
```

## Database Indexes

```mermaid
graph LR
    subgraph Indexes
        Users[Users] --> EmailIdx[email_idx]
        Projects[Projects] --> StatusIdx[status_idx]
        Tasks[Tasks] --> ProjectIdx[project_idx]
        Schedule[Schedule] --> ProjectIdx[project_idx]
        Cost[Cost] --> ProjectIdx[project_idx]
        
        EmailIdx --> Unique[unique]
        ProjectIdx --> Compound[compound]
    end
```

## Database Relationships

```mermaid
graph TB
    subgraph Relationships
        User[User] --> Projects[Projects]
        Project[Project] --> Tasks[Tasks]
        Project --> Schedule[Schedule]
        Project --> Cost[Cost]
        
        User --> AssignedTasks[Assigned Tasks]
        Task --> Dependencies[Task Dependencies]
    end
```

## Data Flow

```mermaid
sequenceDiagram
    participant App
    participant API
    participant DB
    
    App->>API: Request Data
    API->>DB: Query
    DB-->>API: Return Data
    API-->>App: Response
    
    Note over App,DB: Write Operation
    App->>API: Send Data
    API->>DB: Validate & Save
    DB-->>API: Confirmation
    API-->>App: Success Response
``` 