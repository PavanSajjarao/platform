# Module Structure

## Core Modules

```mermaid
graph TB
    subgraph Core Modules
        Core[Core Module] --> Auth[Auth Module]
        Core --> API[API Module]
        Core --> DB[Database Module]
        
        Auth --> JWT[JWT Service]
        Auth --> RBAC[RBAC Service]
        
        API --> Validation[Validation Service]
        API --> Transform[Transform Service]
        
        DB --> Models[Data Models]
        DB --> Migrations[Database Migrations]
    end
```

### Core Module
- Central module for core functionality
- Provides shared services and utilities
- Manages application lifecycle

### Auth Module
- Handles authentication and authorization
- JWT token management
- Role-based access control
- Session management

### API Module
- Request/Response handling
- Data validation
- Response transformation
- Error handling

## Feature Modules

```mermaid
graph TB
    subgraph Feature Modules
        Project[Project Module] --> Task[Task Module]
        Project --> Schedule[Schedule Module]
        Project --> Workflow[Workflow Module]
        
        Schedule --> Calendar[Calendar Service]
        Schedule --> WBS[WBS Service]
        Schedule --> Resource[Resource Service]
        
        Task --> Assignment[Assignment Service]
        Task --> Status[Status Service]
        
        Workflow --> State[State Machine]
        Workflow --> Transition[Transition Service]
    end
```

### Project Module
- Project management
- Project configuration
- Project lifecycle

### Schedule Module
- Calendar management
- Work breakdown structure (WBS)
- Resource scheduling
- Timeline management

### Task Module
- Task management
- Task assignments
- Task status tracking
- Task dependencies

### Workflow Module
- Workflow definition
- State management
- Transition rules
- Workflow execution

## Cost Control Modules

```mermaid
graph TB
    subgraph Cost Control
        CostSheet[Cost Sheet Module] --> Codes[Cost Codes Module]
        CostSheet --> Props[Column Props Module]
        
        Codes --> Categories[Cost Categories]
        Codes --> Hierarchy[Code Hierarchy]
        
        Props --> Validation[Property Validation]
        Props --> Format[Format Rules]
    end
```

### Cost Sheet Module
- Cost sheet management
- Budget tracking
- Cost allocation

### Cost Codes Module
- Cost code management
- Code hierarchy
- Code validation

### Column Props Module
- Column configuration
- Property validation
- Format rules

## Integration Modules

```mermaid
graph TB
    subgraph Integration
        Webhook[Webhook Module] --> Queue[Message Queue]
        Webhook --> Log[Execution Log]
        
        Queue --> Processor[Webhook Processor]
        Queue --> Retry[Retry Service]
        
        Log --> Storage[Log Storage]
        Log --> Monitor[Monitoring Service]
    end
```

### Webhook Module
- Webhook registration
- Event handling
- Payload processing

### Message Queue
- Async processing
- Retry mechanism
- Error handling

### Execution Log
- Log management
- Monitoring
- Debugging

## Module Dependencies

```mermaid
graph LR
    subgraph Core Dependencies
        Common[Common Library]
        DB[Database Library]
        Auth[Auth Library]
    end
    
    subgraph Feature Dependencies
        Project --> Common
        Schedule --> Common
        Task --> Common
        Workflow --> Common
    end
    
    subgraph Integration Dependencies
        Webhook --> Common
        Webhook --> Queue
    end
``` 