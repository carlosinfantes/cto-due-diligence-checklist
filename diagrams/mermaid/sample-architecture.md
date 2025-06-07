# Sample Architecture Diagrams

> **Mermaid diagrams** - Copy the code below and paste into any Markdown file or Mermaid editor.

## Basic Web Application Architecture

```mermaid
graph TB
    User[👤 User] --> LB[Load Balancer]
    LB --> App1[App Server 1]
    LB --> App2[App Server 2]
    LB --> App3[App Server 3]
    
    App1 --> Cache[Redis Cache]
    App2 --> Cache
    App3 --> Cache
    
    App1 --> DB[(Primary Database)]
    App2 --> DB
    App3 --> DB
    
    DB --> Replica[(Read Replica)]
    
    App1 --> Queue[Message Queue]
    App2 --> Queue
    App3 --> Queue
    
    Queue --> Worker1[Background Worker 1]
    Queue --> Worker2[Background Worker 2]
    
    Worker1 --> Storage[File Storage]
    Worker2 --> Storage
```

## Microservices Architecture

```mermaid
graph TB
    subgraph "Frontend"
        Web[Web App]
        Mobile[Mobile App]
    end
    
    subgraph "API Gateway"
        Gateway[API Gateway]
    end
    
    subgraph "Microservices"
        Auth[Auth Service]
        User[User Service]
        Order[Order Service]
        Payment[Payment Service]
        Notification[Notification Service]
    end
    
    subgraph "Data Layer"
        AuthDB[(Auth DB)]
        UserDB[(User DB)]
        OrderDB[(Order DB)]
        PaymentDB[(Payment DB)]
    end
    
    subgraph "External Services"
        PaymentGW[Payment Gateway]
        EmailSvc[Email Service]
    end
    
    Web --> Gateway
    Mobile --> Gateway
    
    Gateway --> Auth
    Gateway --> User
    Gateway --> Order
    Gateway --> Payment
    
    Auth --> AuthDB
    User --> UserDB
    Order --> OrderDB
    Payment --> PaymentDB
    
    Payment --> PaymentGW
    Notification --> EmailSvc
    
    Order --> Notification
    Payment --> Notification
```

## Data Flow Diagram

```mermaid
flowchart TD
    A[User Request] --> B{Authentication}
    B -->|Valid| C[Process Request]
    B -->|Invalid| D[Return Error]
    
    C --> E{Check Cache}
    E -->|Hit| F[Return Cached Data]
    E -->|Miss| G[Query Database]
    
    G --> H[Process Data]
    H --> I[Update Cache]
    I --> J[Return Response]
    
    C --> K{Write Operation?}
    K -->|Yes| L[Validate Data]
    K -->|No| E
    
    L --> M{Valid?}
    M -->|Yes| N[Write to Database]
    M -->|No| O[Return Validation Error]
    
    N --> P[Invalidate Cache]
    P --> Q[Trigger Events]
    Q --> R[Return Success]
```

## Deployment Architecture

```mermaid
graph TB
    subgraph "Production Environment"
        subgraph "Kubernetes Cluster"
            subgraph "Namespace: app"
                Pod1[App Pod 1]
                Pod2[App Pod 2]
                Pod3[App Pod 3]
            end
            
            subgraph "Namespace: data"
                Redis[Redis Pod]
                DB[Database Pod]
            end
            
            Ingress[Ingress Controller]
            Service[App Service]
        end
        
        subgraph "External Services"
            RDS[(AWS RDS)]
            S3[AWS S3]
            CloudWatch[CloudWatch]
        end
    end
    
    subgraph "CI/CD Pipeline"
        GitHub[GitHub Repo]
        Actions[GitHub Actions]
        Registry[Container Registry]
    end
    
    Internet[🌐 Internet] --> Ingress
    Ingress --> Service
    Service --> Pod1
    Service --> Pod2
    Service --> Pod3
    
    Pod1 --> Redis
    Pod2 --> Redis
    Pod3 --> Redis
    
    Pod1 --> RDS
    Pod2 --> RDS
    Pod3 --> RDS
    
    Pod1 --> S3
    Pod2 --> S3
    Pod3 --> S3
    
    GitHub --> Actions
    Actions --> Registry
    Registry --> Pod1
    Registry --> Pod2
    Registry --> Pod3
    
    Pod1 --> CloudWatch
    Pod2 --> CloudWatch
    Pod3 --> CloudWatch
```

## Security Architecture

```mermaid
graph TB
    subgraph "DMZ"
        WAF[Web Application Firewall]
        LB[Load Balancer]
    end
    
    subgraph "Application Tier"
        App1[App Server 1]
        App2[App Server 2]
    end
    
    subgraph "Database Tier"
        DB[(Database)]
        Backup[(Backup)]
    end
    
    subgraph "Security Services"
        Auth[Auth Service]
        Vault[Secret Management]
        Monitor[Security Monitoring]
    end
    
    Internet[🌐 Internet] --> WAF
    WAF --> LB
    LB --> App1
    LB --> App2
    
    App1 --> Auth
    App2 --> Auth
    
    App1 --> Vault
    App2 --> Vault
    
    App1 --> DB
    App2 --> DB
    
    DB --> Backup
    
    App1 --> Monitor
    App2 --> Monitor
    Auth --> Monitor
    DB --> Monitor
    
    classDef security fill:#ff9999
    classDef data fill:#99ccff
    classDef app fill:#99ff99
    
    class WAF,Auth,Vault,Monitor security
    class DB,Backup data
    class App1,App2 app
```

## Event-Driven Architecture

```mermaid
sequenceDiagram
    participant User
    participant API
    participant OrderService
    participant PaymentService
    participant InventoryService
    participant NotificationService
    participant EventBus
    
    User->>API: Create Order
    API->>OrderService: Process Order
    OrderService->>EventBus: OrderCreated Event
    
    EventBus->>PaymentService: OrderCreated
    EventBus->>InventoryService: OrderCreated
    
    PaymentService->>EventBus: PaymentProcessed Event
    InventoryService->>EventBus: InventoryReserved Event
    
    EventBus->>OrderService: PaymentProcessed
    EventBus->>OrderService: InventoryReserved
    
    OrderService->>EventBus: OrderConfirmed Event
    EventBus->>NotificationService: OrderConfirmed
    
    NotificationService->>User: Order Confirmation Email
    OrderService->>API: Order Complete
    API->>User: Success Response
```

## How to Use These Diagrams

### 1. Copy and Paste
Copy any diagram code and paste it into:
- GitHub README files
- GitLab documentation
- Mermaid Live Editor (https://mermaid.live/)
- VS Code with Mermaid extension

### 2. Customize for Your Architecture
- Replace service names with your actual services
- Add/remove components as needed
- Adjust relationships and data flows
- Update styling and colors

### 3. Version Control Your Diagrams
- Keep diagram code in your repository
- Update diagrams when architecture changes
- Use pull requests to review architecture changes

### 4. Generate Images
```bash
# Install mermaid CLI
npm install -g @mermaid-js/mermaid-cli

# Generate PNG from markdown
mmdc -i architecture.md -o architecture.png
```

## Pro Tips

> 💡 **Keep diagrams simple**: Focus on the most important components and relationships

> 🔄 **Update regularly**: Architecture diagrams should evolve with your system

> 📝 **Add context**: Include brief descriptions of what each component does

> 🎨 **Use consistent styling**: Establish color coding for different types of components
