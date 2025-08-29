# RELMS v2 - Real Estate Lottery Management System

A comprehensive Next.js application for managing real estate projects, applications, and lottery-based property allocation system.

## Architecture Overview

```mermaid
graph TB
    subgraph "Frontend Layer"
        A[Next.js App Router] --> B[Admin Dashboard]
        A --> C[User Dashboard]
        A --> D[Booking System]
        A --> E[Public Pages]
    end

    subgraph "Authentication"
        F[NextAuth.js] --> G[Google OAuth]
        F --> H[Credentials Auth]
        F --> I[Session Management]
    end

    subgraph "API Layer"
        J[Next.js API Routes] --> K[Project Management]
        J --> L[Application Processing]
        J --> M[Lottery System]
        J --> N[User Management]
        J --> O[File Upload]
    end

    subgraph "Business Logic"
        P[Controllers] --> Q[Project Controller]
        P --> R[Application Controller]
        P --> S[Lottery Controller]
        P --> T[User Controller]
        P --> U[Phase Controller]
        
        V[Services] --> W[Application Service]
        V --> X[Lottery Service]
        V --> Y[Project Service]
        V --> Z[User Service]
    end

    subgraph "Data Layer"
        AA[MongoDB Atlas] --> BB[Projects Collection]
        AA --> CC[Users Collection]
        AA --> DD[Applications Collection]
        AA --> EE[Phases Collection]
        AA --> FF[Units Collection]
        AA --> GG[Lottery Results Collection]
    end

    subgraph "External Services"
        HH[Email Service] --> II[Nodemailer]
        JJ[File Storage] --> KK[Google Cloud Storage]
        LL[PDF Generation] --> MM[jsPDF]
    end

    %% Connections
    A --> F
    A --> J
    J --> P
    P --> V
    V --> AA
    J --> HH
    J --> JJ
    J --> LL

    %% Styling
    classDef frontend fill:#e1f5fe
    classDef auth fill:#f3e5f5
    classDef api fill:#e8f5e8
    classDef business fill:#fff3e0
    classDef data fill:#ffebee
    classDef external fill:#f1f8e9

    class A,B,C,D,E frontend
    class F,G,H,I auth
    class J,K,L,M,N,O api
    class P,Q,R,S,T,U,V,W,X,Y,Z business
    class AA,BB,CC,DD,EE,FF,GG data
    class HH,II,JJ,KK,LL,MM external
```

## System Components

### Frontend Architecture
- **Next.js 15** with App Router and Turbopack
- **React 19** with modern hooks and context
- **Tailwind CSS 4** for styling
- **Radix UI** components for accessibility
- **TypeScript** for type safety

### Key Features

#### 🏢 **Admin Dashboard**
- **Project Management**: Create and manage real estate projects
- **Inventory Management**: Units, phases, unit types, and tags
- **Application Processing**: Review and manage user applications
- **Lottery System**: Configure and execute property allocation lotteries
- **Bulk Operations**: Excel-based bulk unit uploads
- **Kit Management**: Generate application kits and forms

#### 👥 **User System** 
- **Multi-role Authentication**: Admin/Buyer roles with Google OAuth
- **Application Forms**: Dynamic form builder with conditional fields
- **Booking Process**: Multi-step application workflow
- **Payment Integration**: Kit payment processing
- **Document Generation**: PDF applications and receipts

#### 🎲 **Lottery System**
- **Advanced Configuration**: Unit preferences, user preferences
- **Multi-round Lotteries**: Complex allocation algorithms
- **Result Management**: Automated result generation and notifications
- **Audit Trail**: Complete lottery history and transparency

#### 📋 **Application Management**
- **Dynamic Forms**: JSON-based form definitions
- **Auto-save**: Real-time form data persistence  
- **Status Tracking**: Application lifecycle management
- **Print/Export**: PDF generation and kit management

## Tech Stack

| Layer | Technology |
|-------|------------|
| **Frontend** | Next.js 15, React 19, TypeScript |
| **Styling** | Tailwind CSS 4, Radix UI |
| **Authentication** | NextAuth.js, Google OAuth |
| **Database** | MongoDB Atlas, Mongoose ODM |
| **File Storage** | Google Cloud Storage |
| **Email** | Nodemailer |
| **PDF Generation** | jsPDF, html2canvas |
| **Validation** | Zod schemas |
| **State Management** | React Context, Hooks |

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

### Environment Setup

1. **Clone the repository**
2. **Install dependencies**: `npm install`
3. **Set up environment variables**: Create `.env.local` with:
   ```env
   MONGODB_URI=your_mongodb_connection_string
   NEXTAUTH_SECRET=your_nextauth_secret
   NEXTAUTH_URL=http://localhost:3000
   GOOGLE_CLIENT_ID=your_google_oauth_client_id
   GOOGLE_CLIENT_SECRET=your_google_oauth_client_secret
   ```
4. **Run the development server**: `npm run dev`

### Available Scripts

- `npm run dev` - Start development server with Turbopack
- `npm run build` - Build for production
- `npm run start` - Start production server
- `npm run lint` - Run ESLint
- `npm run seedForms` - Seed form definitions
- `npm run seedKit` - Seed application kits
- `npm run testEmail` - Test email functionality

## Project Structure

```
relms-v2/
├── app/                          # Next.js App Router
│   ├── admin/                    # Admin dashboard pages
│   │   └── dashboard/[projectId]/
│   │       ├── inventory-management/  # Unit/Phase management
│   │       ├── kit-management/        # Application kit management
│   │       └── lottery/              # Lottery configuration
│   ├── api/                      # API routes
│   │   ├── applications/         # Application CRUD operations
│   │   ├── project/             # Project management APIs
│   │   └── auth/                # Authentication endpoints
│   ├── bookings/                # User booking workflow
│   └── user/                    # User dashboard
├── components/                  # Reusable UI components
│   └── ui/                     # Base UI components
├── controllers/                # Business logic controllers
├── services/                   # Data access services
├── schemas/                    # MongoDB schemas
├── types/                      # TypeScript type definitions
├── lib/                        # Utility libraries
└── middleware.ts               # Next.js middleware
```

## Technical Architecture

### System Architecture Layers

```mermaid
graph TB
    subgraph "Client Layer"
        A1[Web Browser] --> A2[React Components]
        A2 --> A3[Context Providers]
        A3 --> A4[Custom Hooks]
    end

    subgraph "Presentation Layer"
        B1[Next.js App Router] --> B2[Server Components]
        B1 --> B3[Client Components]
        B1 --> B4[Route Handlers]
        B2 --> B5[Streaming SSR]
        B3 --> B6[Hydration]
    end

    subgraph "Authentication Layer"
        C1[NextAuth.js Middleware] --> C2[JWT Strategy]
        C1 --> C3[OAuth Providers]
        C1 --> C4[Session Management]
        C2 --> C5[Token Validation]
        C3 --> C6[Google OAuth 2.0]
    end

    subgraph "API Gateway Layer"
        D1[Next.js API Routes] --> D2[Route Protection]
        D1 --> D3[Request Validation]
        D1 --> D4[Response Formatting]
        D2 --> D5[Role-based Access]
        D3 --> D6[Zod Schemas]
    end

    subgraph "Business Logic Layer"
        E1[Controllers] --> E2[Input Validation]
        E1 --> E3[Business Rules]
        E1 --> E4[Error Handling]
        E3 --> E5[Lottery Algorithms]
        E3 --> E6[Application Workflows]
    end

    subgraph "Service Layer"
        F1[Data Services] --> F2[CRUD Operations]
        F1 --> F3[Data Aggregation]
        F1 --> F4[Transaction Management]
        F2 --> F5[Query Optimization]
        F4 --> F6[MongoDB Transactions]
    end

    subgraph "Data Access Layer"
        G1[Mongoose ODM] --> G2[Schema Validation]
        G1 --> G3[Connection Pooling]
        G1 --> G4[Index Management]
        G2 --> G5[Type Safety]
        G3 --> G6[Performance Optimization]
    end

    subgraph "Data Layer"
        H1[MongoDB Atlas] --> H2[Replica Set]
        H1 --> H3[Sharding Strategy]
        H1 --> H4[Backup & Recovery]
        H2 --> H5[High Availability]
        H3 --> H6[Horizontal Scaling]
    end

    subgraph "External Services"
        I1[Google Cloud Storage] --> I2[File Management]
        I3[Email Service] --> I4[Notification System]
        I5[PDF Generation] --> I6[Document Processing]
    end

    %% Layer Connections
    A1 --> B1
    B1 --> C1
    B1 --> D1
    D1 --> E1
    E1 --> F1
    F1 --> G1
    G1 --> H1
    D1 --> I1
    D1 --> I3
    D1 --> I5
```

### Component Architecture

```mermaid
graph TB
    subgraph "Frontend Architecture"
        A[App Router] --> B[Layout Components]
        A --> C[Page Components]
        
        subgraph "Admin Dashboard"
            D[Admin Layout] --> E[Project Management]
            D --> F[Inventory Management]
            D --> G[Lottery System]
            D --> H[Application Management]
            
            E --> E1[Project CRUD]
            F --> F1[Unit Management]
            F --> F2[Phase Management]
            F --> F3[Bulk Upload]
            G --> G1[Lottery Config]
            G --> G2[Result Processing]
            H --> H1[Application Review]
        end
        
        subgraph "User Interface"
            I[User Layout] --> J[Booking Flow]
            J --> J1[Kit Selection]
            J --> J2[Application Form]
            J --> J3[Payment Process]
            J --> J4[Status Tracking]
        end
        
        subgraph "Shared Components"
            K[UI Components] --> K1[Forms]
            K --> K2[Tables]
            K --> K3[Modals]
            K --> K4[Charts]
        end
    end

    subgraph "State Management"
        L[React Context] --> L1[Auth Context]
        L --> L2[Application Context]
        L --> L3[Project Context]
        L --> L4[Toast Context]
        
        M[Custom Hooks] --> M1[useApplications]
        M --> M2[useProjects]
        M --> M3[useAuth]
        M --> M4[useFormKit]
    end

    C --> D
    C --> I
    B --> K
    D --> L
    I --> L
    K --> M
```

### Data Flow Architecture

```mermaid
sequenceDiagram
    participant U as User
    participant UI as React Component
    participant Hook as Custom Hook
    participant API as API Route
    participant MW as Middleware
    participant C as Controller
    participant S as Service
    participant DB as MongoDB
    participant Ext as External Service

    Note over U,Ext: Complete Application Submission Flow

    U->>UI: Fill Application Form
    UI->>Hook: useApplications.submit()
    Hook->>API: POST /api/applications
    
    Note over API,MW: Authentication & Validation
    API->>MW: Request Processing
    MW->>API: Authenticated User
    API->>API: Zod Schema Validation
    
    Note over API,S: Business Logic Processing
    API->>C: ApplicationController.create()
    C->>C: Business Rule Validation
    C->>S: ApplicationService.create()
    
    Note over S,DB: Data Persistence
    S->>DB: Begin Transaction
    S->>DB: Insert Application
    S->>DB: Update Phase Statistics
    S->>DB: Create Audit Log
    DB->>S: Transaction Complete
    
    Note over S,Ext: External Operations
    S->>Ext: Send Email Notification
    S->>Ext: Generate PDF Receipt
    Ext->>S: Operations Complete
    
    Note over S,UI: Response Flow
    S->>C: Application Data
    C->>API: Formatted Response
    API->>Hook: JSON Response
    Hook->>UI: State Update
    UI->>U: Success Feedback
```

### Lottery System Architecture

```mermaid
graph TB
    subgraph "Lottery Engine"
        A[Lottery Controller] --> B[Configuration Validator]
        A --> C[Eligibility Engine]
        A --> D[Allocation Algorithm]
        A --> E[Result Processor]
        
        C --> C1[User Eligibility Check]
        C --> C2[Unit Availability Check]
        C --> C3[Preference Validation]
        
        D --> D1[Random Number Generator]
        D --> D2[Preference Scorer]
        D --> D3[Fairness Algorithm]
        D --> D4[Multi-Round Processor]
        
        E --> E1[Winner Selection]
        E --> E2[Waitlist Management]
        E --> E3[Result Notification]
        E --> E4[Audit Trail Creation]
    end

    subgraph "Data Dependencies"
        F[Applications Collection] --> C
        G[Units Collection] --> C
        H[User Preferences] --> D
        I[Lottery Config] --> D
        J[Previous Results] --> D
    end

    subgraph "Output Systems"
        E1 --> K[Winner Database]
        E2 --> L[Waitlist Database]
        E3 --> M[Email System]
        E4 --> N[Audit Database]
    end
```

### Security Architecture

```mermaid
graph TB
    subgraph "Security Layers"
        A[HTTPS/TLS 1.3] --> B[Next.js Middleware]
        B --> C[NextAuth.js]
        C --> D[JWT Verification]
        D --> E[Role-Based Access Control]
        E --> F[API Rate Limiting]
        F --> G[Input Sanitization]
        G --> H[MongoDB Security]
    end

    subgraph "Authentication Flow"
        I[User Login] --> J[OAuth Provider]
        J --> K[Authorization Code]
        K --> L[Token Exchange]
        L --> M[JWT Creation]
        M --> N[Session Storage]
    end

    subgraph "Authorization Matrix"
        O[Admin Role] --> P[Full System Access]
        Q[User Role] --> R[Limited Access]
        
        P --> P1[Project Management]
        P --> P2[User Management]
        P --> P3[Lottery Control]
        P --> P4[System Settings]
        
        R --> R1[Own Applications]
        R --> R2[Public Project Info]
        R --> R3[Application Submission]
    end
```

### Database Architecture

```mermaid
erDiagram
    PROJECT {
        ObjectId _id PK
        string name
        string description
        Date createdAt
        Date updatedAt
        ObjectId createdBy FK
        ProjectStatus status
        ProjectConfig config
    }

    PHASE {
        ObjectId _id PK
        ObjectId projectId FK
        string name
        Date startDate
        Date endDate
        PhaseStatus status
        PhaseConfig config
        number totalUnits
        number availableUnits
    }

    UNIT {
        ObjectId _id PK
        ObjectId phaseId FK
        ObjectId unitTypeId FK
        string unitNumber
        UnitStatus status
        UnitConfig specifications
        number price
        string[] tags
    }

    APPLICATION {
        ObjectId _id PK
        ObjectId userId FK
        ObjectId phaseId FK
        ObjectId unitPreferences FK
        ApplicationStatus status
        Object formData
        Date submittedAt
        string applicationNumber
        Object auditTrail
    }

    USER {
        ObjectId _id PK
        string email UK
        string name
        UserRole role
        string profileImage
        Date createdAt
        Object preferences
    }

    LOTTERY_RESULT {
        ObjectId _id PK
        ObjectId phaseId FK
        ObjectId lotteryConfigId FK
        Date executedAt
        Object winners
        Object waitlist
        Object statistics
        LotteryStatus status
    }

    PROJECT ||--o{ PHASE : contains
    PHASE ||--o{ UNIT : contains
    PHASE ||--o{ APPLICATION : receives
    USER ||--o{ APPLICATION : submits
    PHASE ||--o{ LOTTERY_RESULT : generates
    APPLICATION ||--o{ LOTTERY_RESULT : participates
```

### Performance Architecture

```mermaid
graph TB
    subgraph "Frontend Performance"
        A[Next.js Turbopack] --> B[Fast Refresh]
        A --> C[Code Splitting]
        A --> D[Image Optimization]
        A --> E[Font Optimization]
        
        F[React Optimization] --> G[Memo & Callback]
        F --> H[Lazy Loading]
        F --> I[Suspense Boundaries]
        F --> J[Virtual Scrolling]
    end

    subgraph "Backend Performance"
        K[MongoDB Indexing] --> L[Query Optimization]
        K --> M[Connection Pooling]
        K --> N[Read Replicas]
        
        O[Caching Strategy] --> P[Redis Cache]
        O --> Q[Browser Cache]
        O --> R[CDN Cache]
        
        S[API Optimization] --> T[Response Compression]
        S --> U[Pagination]
        S --> V[Field Selection]
    end

    subgraph "Monitoring & Metrics"
        W[Performance Monitoring] --> X[Core Web Vitals]
        W --> Y[API Response Times]
        W --> Z[Database Queries]
        
        AA[Error Tracking] --> BB[Client Errors]
        AA --> CC[Server Errors]
        AA --> DD[Performance Issues]
    end
```

### Deployment Architecture

```mermaid
graph TB
    subgraph "Production Environment"
        A[Load Balancer] --> B[Next.js Application]
        A --> C[Static Assets CDN]
        
        subgraph "Application Tier"
            B --> D[Node.js Runtime]
            D --> E[PM2 Process Manager]
            E --> F[Application Instances]
        end
        
        subgraph "Database Tier"
            G[MongoDB Atlas] --> H[Primary Replica]
            G --> I[Secondary Replicas]
            G --> J[Arbiter Node]
        end
        
        subgraph "Storage Tier"
            K[Google Cloud Storage] --> L[Document Storage]
            K --> M[Image Storage]
            K --> N[Backup Storage]
        end
        
        subgraph "Monitoring & Logging"
            O[Application Monitoring] --> P[Performance Metrics]
            O --> Q[Error Tracking]
            O --> R[User Analytics]
            
            S[System Monitoring] --> T[Server Metrics]
            S --> U[Database Metrics]
            S --> V[Network Metrics]
        end
    end

    subgraph "Development Pipeline"
        W[Git Repository] --> X[GitHub Actions]
        X --> Y[Build Process]
        Y --> Z[Testing Suite]
        Z --> AA[Deployment]
        AA --> BB[Production Release]
    end

    F --> G
    F --> K
    F --> O
    F --> S
```

### Microservice Communication

```mermaid
sequenceDiagram
    participant Client as Web Client
    participant Gateway as API Gateway
    participant Auth as Auth Service
    participant App as Application Service
    participant Lot as Lottery Service
    participant Email as Email Service
    participant DB as Database
    participant Storage as File Storage

    Note over Client,Storage: End-to-End Application Flow

    Client->>Gateway: Submit Application
    Gateway->>Auth: Validate JWT Token
    Auth-->>Gateway: User Authenticated
    
    Gateway->>App: Process Application
    App->>DB: Validate Business Rules
    DB-->>App: Rules Valid
    
    App->>DB: Save Application
    DB-->>App: Application Saved
    
    App->>Storage: Upload Documents
    Storage-->>App: Documents Stored
    
    App->>Email: Send Confirmation
    Email-->>App: Email Sent
    
    Note over Gateway,Lot: Lottery Execution Process
    Gateway->>Lot: Execute Lottery
    Lot->>DB: Fetch Applications
    DB-->>Lot: Application Data
    
    Lot->>Lot: Run Algorithm
    Lot->>DB: Save Results
    DB-->>Lot: Results Saved
    
    Lot->>Email: Notify Winners
    Email-->>Lot: Notifications Sent
    
    Lot-->>Gateway: Lottery Complete
    Gateway-->>Client: Success Response
```

## Technical Implementation Details

### Authentication & Authorization

```typescript
// NextAuth.js Configuration
interface AuthUser {
  id: string;
  email: string;
  name: string;
  role: 'ADMIN' | 'BUYER';
  image?: string;
}

// JWT Token Structure
interface JWTPayload {
  id: string;
  email: string;
  role: UserRole;
  picture?: string;
  iat: number;
  exp: number;
}

// Middleware Protection
const protectedRoutes = [
  '/admin/**',
  '/api/admin/**',
  '/user/dashboard',
  '/bookings/**'
];
```

### Database Schema & Indexing

```javascript
// MongoDB Indexes for Performance
db.applications.createIndex({ "userId": 1, "phaseId": 1 });
db.applications.createIndex({ "status": 1, "submittedAt": -1 });
db.applications.createIndex({ "phaseId": 1, "status": 1 });

db.units.createIndex({ "phaseId": 1, "status": 1 });
db.units.createIndex({ "unitTypeId": 1, "availabilityStatus": 1 });
db.units.createIndex({ "tags": 1, "price": 1 });

db.users.createIndex({ "email": 1 }, { unique: true });
db.users.createIndex({ "role": 1, "createdAt": -1 });

// Compound Indexes for Complex Queries
db.lotteryResults.createIndex({ 
  "phaseId": 1, 
  "executedAt": -1, 
  "status": 1 
});
```

### API Layer Architecture

```typescript
// Route Handler Pattern
export async function POST(request: NextRequest) {
  try {
    // 1. Authentication
    const session = await getServerSession(authOptions);
    if (!session) {
      return NextResponse.json({ error: 'Unauthorized' }, { status: 401 });
    }

    // 2. Authorization
    const hasPermission = await checkUserPermission(
      session.user.id, 
      'CREATE_APPLICATION'
    );
    if (!hasPermission) {
      return NextResponse.json({ error: 'Forbidden' }, { status: 403 });
    }

    // 3. Input Validation
    const body = await request.json();
    const validatedData = applicationSchema.parse(body);

    // 4. Business Logic
    const result = await ApplicationController.create(
      session.user.id,
      validatedData
    );

    // 5. Response
    return NextResponse.json(result, { status: 201 });
  } catch (error) {
    return handleAPIError(error);
  }
}
```

### Lottery Algorithm Implementation

```typescript
interface LotteryConfig {
  algorithm: 'RANDOM' | 'WEIGHTED' | 'PREFERENCE_BASED';
  preferences: {
    unitType: number;
    location: number;
    price: number;
  };
  fairnessRules: {
    maxUnitsPerUser: number;
    priorityGroups: string[];
  };
}

class LotteryEngine {
  async executeLottery(phaseId: string, config: LotteryConfig) {
    const applications = await this.getEligibleApplications(phaseId);
    const availableUnits = await this.getAvailableUnits(phaseId);
    
    const allocations = await this.runAllocationAlgorithm(
      applications,
      availableUnits,
      config
    );
    
    return this.processResults(allocations);
  }

  private async runAllocationAlgorithm(
    applications: Application[],
    units: Unit[],
    config: LotteryConfig
  ) {
    switch (config.algorithm) {
      case 'PREFERENCE_BASED':
        return this.preferenceBasedAllocation(applications, units, config);
      case 'WEIGHTED':
        return this.weightedAllocation(applications, units, config);
      default:
        return this.randomAllocation(applications, units);
    }
  }
}
```

### Performance Optimization Strategies

```typescript
// 1. Database Query Optimization
interface QueryOptimization {
  // Use projection to limit fields
  projection: string[];
  
  // Implement pagination
  pagination: {
    page: number;
    limit: number;
    sort: Record<string, 1 | -1>;
  };
  
  // Use aggregation pipeline
  aggregation: PipelineStage[];
}

// 2. Caching Strategy
interface CacheStrategy {
  // Redis for session data
  sessionCache: {
    ttl: 3600; // 1 hour
    prefix: 'session:';
  };
  
  // Application cache for static data
  staticCache: {
    ttl: 86400; // 24 hours
    data: ['projects', 'phases', 'unitTypes'];
  };
}

// 3. React Performance
const OptimizedComponent = memo(({ data }: Props) => {
  const memoizedValue = useMemo(() => {
    return expensiveCalculation(data);
  }, [data]);
  
  const handleClick = useCallback(() => {
    // Handle click
  }, []);
  
  return <div>{memoizedValue}</div>;
});
```

### Error Handling & Monitoring

```typescript
// Centralized Error Handler
class APIErrorHandler {
  static handle(error: unknown): NextResponse {
    if (error instanceof ZodError) {
      return NextResponse.json({
        error: 'Validation Error',
        details: error.errors
      }, { status: 400 });
    }
    
    if (error instanceof MongoError) {
      console.error('Database Error:', error);
      return NextResponse.json({
        error: 'Database Error'
      }, { status: 500 });
    }
    
    // Log unknown errors
    console.error('Unknown Error:', error);
    return NextResponse.json({
      error: 'Internal Server Error'
    }, { status: 500 });
  }
}

// Monitoring Integration
interface MonitoringMetrics {
  apiResponseTime: number;
  databaseQueryTime: number;
  errorRate: number;
  userActions: {
    type: string;
    timestamp: Date;
    userId: string;
  }[];
}
```

### Security Implementation

```typescript
// Input Sanitization
import DOMPurify from 'dompurify';

const sanitizeInput = (input: string): string => {
  return DOMPurify.sanitize(input);
};

// Rate Limiting
interface RateLimitConfig {
  windowMs: 15 * 60 * 1000; // 15 minutes
  maxRequests: 100; // per windowMs
  keyGenerator: (req: Request) => string;
}

// CSRF Protection
const csrfToken = generateCSRFToken();

// Content Security Policy
const cspHeader = `
  default-src 'self';
  script-src 'self' 'unsafe-inline' 'unsafe-eval';
  style-src 'self' 'unsafe-inline';
  img-src 'self' data: https:;
  connect-src 'self' https://api.mongodb.com;
`;
```

### Infrastructure & Deployment [To DO]

#### Development Environment
```yaml
# docker-compose.yml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=development
      - MONGODB_URI=mongodb://mongo:27017/relms
    depends_on:
      - mongo
      - redis

  mongo:
    image: mongo:7.0
    ports:
      - "27017:27017"
    volumes:
      - mongo_data:/data/db

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data

volumes:
  mongo_data:
  redis_data:
```

#### Production Deployment
```dockerfile
# Multi-stage Dockerfile
FROM node:20-alpine AS base
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

FROM node:20-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:20-alpine AS runtime
WORKDIR /app
RUN addgroup --system --gid 1001 nodejs
RUN adduser --system --uid 1001 nextjs
COPY --from=base /app/node_modules ./node_modules
COPY --from=build --chown=nextjs:nodejs /app/.next ./.next
COPY --from=build /app/public ./public
COPY --from=build /app/package.json ./package.json

USER nextjs
EXPOSE 3000
ENV NODE_ENV=production
CMD ["npm", "start"]
```

#### CI/CD Pipeline
```yaml
# .github/workflows/deploy.yml
name: Deploy to Production

on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: 'npm'
      - run: npm ci
      - run: npm run lint
      - run: npm run build
      - run: npm test

  deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to Production
        env:
          MONGODB_URI: ${{ secrets.MONGODB_URI }}
          NEXTAUTH_SECRET: ${{ secrets.NEXTAUTH_SECRET }}
        run: |
          docker build -t relms-app .
          docker push registry.com/relms-app:latest
          kubectl apply -f k8s/
```

#### Kubernetes Configuration
```yaml
# k8s/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: relms-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: relms-app
  template:
    metadata:
      labels:
        app: relms-app
    spec:
      containers:
      - name: app
        image: registry.com/relms-app:latest
        ports:
        - containerPort: 3000
        env:
        - name: NODE_ENV
          value: "production"
        - name: MONGODB_URI
          valueFrom:
            secretKeyRef:
              name: relms-secrets
              key: mongodb-uri
        resources:
          requests:
            memory: "256Mi"
            cpu: "250m"
          limits:
            memory: "512Mi"
            cpu: "500m"
        livenessProbe:
          httpGet:
            path: /api/health
            port: 3000
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /api/ready
            port: 3000
          initialDelaySeconds: 5
          periodSeconds: 5
---
apiVersion: v1
kind: Service
metadata:
  name: relms-service
spec:
  selector:
    app: relms-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 3000
  type: LoadBalancer
```

#### Monitoring & Observability
```typescript
// lib/monitoring.ts
import { createLogger, format, transports } from 'winston';

export const logger = createLogger({
  level: 'info',
  format: format.combine(
    format.timestamp(),
    format.errors({ stack: true }),
    format.json()
  ),
  defaultMeta: { service: 'relms-app' },
  transports: [
    new transports.File({ filename: 'error.log', level: 'error' }),
    new transports.File({ filename: 'combined.log' }),
    new transports.Console({
      format: format.simple()
    })
  ],
});

// Metrics collection
export class MetricsCollector {
  static async recordAPICall(
    endpoint: string,
    method: string,
    duration: number,
    statusCode: number
  ) {
    const metric = {
      timestamp: new Date(),
      endpoint,
      method,
      duration,
      statusCode,
      service: 'relms-api'
    };
    
    // Send to monitoring service
    await this.sendToMonitoring(metric);
  }
  
  static async recordDatabaseQuery(
    collection: string,
    operation: string,
    duration: number
  ) {
    const metric = {
      timestamp: new Date(),
      collection,
      operation,
      duration,
      service: 'relms-db'
    };
    
    await this.sendToMonitoring(metric);
  }
}
```

#### Backup & Recovery
```bash
#!/bin/bash
# backup.sh - MongoDB Backup Script

DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_DIR="/backups/mongodb"
DATABASE="relms"

# Create backup directory
mkdir -p $BACKUP_DIR

# Perform backup
mongodump --uri="$MONGODB_URI" --db=$DATABASE --out=$BACKUP_DIR/$DATE

# Compress backup
tar -czf $BACKUP_DIR/backup_$DATE.tar.gz -C $BACKUP_DIR $DATE

# Upload to cloud storage
gsutil cp $BACKUP_DIR/backup_$DATE.tar.gz gs://relms-backups/

# Clean up local files older than 7 days
find $BACKUP_DIR -name "backup_*.tar.gz" -mtime +7 -delete

echo "Backup completed: backup_$DATE.tar.gz"
```

#### Environment Configuration
```bash
# Production Environment Variables
NODE_ENV=production
PORT=3000

# Database
MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/relms?retryWrites=true&w=majority

# Authentication
NEXTAUTH_URL=https://relms.example.com
NEXTAUTH_SECRET=your_nextauth_secret
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret

# External Services
GOOGLE_CLOUD_STORAGE_BUCKET=relms-documents
GOOGLE_CLOUD_PROJECT_ID=relms-project

# Email Service
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=noreply@relms.com
SMTP_PASSWORD=app_specific_password

# Monitoring
LOG_LEVEL=info
METRICS_ENDPOINT=https://metrics.example.com/api/v1/push

# Security
CSRF_SECRET=your_csrf_secret
RATE_LIMIT_MAX=100
RATE_LIMIT_WINDOW=900000

# Performance
DATABASE_POOL_SIZE=10
REDIS_URL=redis://redis-cluster:6379
CACHE_TTL=3600
```

#### Health Checks & Monitoring
```typescript
// api/health/route.ts
export async function GET() {
  const checks = {
    timestamp: new Date().toISOString(),
    status: 'healthy',
    checks: {
      database: await checkDatabase(),
      redis: await checkRedis(),
      storage: await checkStorage(),
      memory: checkMemoryUsage(),
      uptime: process.uptime()
    }
  };
  
  const isHealthy = Object.values(checks.checks)
    .every(check => check.status === 'healthy');
  
  return Response.json(checks, { 
    status: isHealthy ? 200 : 503 
  });
}

async function checkDatabase() {
  try {
    await mongoose.connection.db.admin().ping();
    return { status: 'healthy', latency: Date.now() };
  } catch (error) {
    return { status: 'unhealthy', error: error.message };
  }
}
```

#### Scalability Considerations
```mermaid
graph TB
    subgraph "Load Balancing"
        A[Load Balancer] --> B[App Instance 1]
        A --> C[App Instance 2]
        A --> D[App Instance 3]
    end
    
    subgraph "Database Scaling"
        E[MongoDB Primary] --> F[Secondary 1]
        E --> G[Secondary 2]
        E --> H[Arbiter]
        
        I[Sharding] --> J[Shard 1]
        I --> K[Shard 2]
        I --> L[Shard 3]
    end
    
    subgraph "Caching Layer"
        M[Redis Cluster] --> N[Redis Master 1]
        M --> O[Redis Master 2]
        M --> P[Redis Master 3]
        
        N --> Q[Redis Slave 1]
        O --> R[Redis Slave 2]
        P --> S[Redis Slave 3]
    end
    
    subgraph "CDN & Static Assets"
        T[CloudFront CDN] --> U[Static Files]
        T --> V[Images]
        T --> W[Documents]
    end
    
    B --> E
    C --> E
    D --> E
    B --> M
    C --> M
    D --> M
```

## Key Features Deep Dive

### 🏗️ Project Management
- **Multi-phase Projects**: Support for complex real estate projects with multiple phases
- **Unit Management**: Detailed unit configuration with types, tags, and inventory tracking  
- **Bulk Operations**: Excel-based bulk import/export functionality
- **Hierarchical Structure**: Project → Phase → Unit Type → Unit

### 📝 Dynamic Forms
- **JSON-based Configuration**: Flexible form definitions stored in database
- **Conditional Logic**: Fields that appear/hide based on user selections
- **Auto-save**: Real-time form data persistence
- **Validation**: Client and server-side validation with Zod schemas

### 🎯 Lottery System
- **Multi-criteria Allocation**: Complex algorithms considering user preferences, unit availability, and fairness
- **Transparency**: Complete audit trail of lottery configuration and results
- **Multi-round Support**: Support for multiple lottery rounds with different criteria
- **Result Management**: Automated notification and result publication

### 🔐 Security & Authentication
- **Role-based Access**: Admin/Buyer role separation
- **OAuth Integration**: Google OAuth with profile synchronization
- **Session Management**: JWT-based session handling
- **API Protection**: Middleware-based route protection

## Database Schema

### Core Collections
- **Projects**: Real estate project information
- **Phases**: Project phases with timing and configuration
- **Units**: Individual property units with details and availability
- **Applications**: User applications with form data and status
- **Users**: User profiles with roles and authentication data
- **LotteryResults**: Lottery execution results and allocations

## API Documentation

### Authentication Endpoints
- `POST /api/auth/signin` - User login
- `POST /api/auth/signout` - User logout
- `GET /api/auth/session` - Get current session

### Application Management
- `GET /api/applications` - List applications with filters
- `POST /api/applications` - Create new application
- `PUT /api/applications/[id]` - Update application
- `DELETE /api/applications/[id]` - Delete application

### Project Management
- `GET /api/project` - List projects
- `POST /api/project` - Create project
- `GET /api/project/[id]` - Get project details
- `PUT /api/project/[id]` - Update project

## Contributing

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Commit changes**: `git commit -m 'Add amazing feature'`
4. **Push to branch**: `git push origin feature/amazing-feature`
5. **Open a Pull Request**

## License

This project is private and proprietary. All rights reserved.

---

Built with ❤️ using Next.js, React, and MongoDB
