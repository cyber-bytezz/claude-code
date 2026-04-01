# System Architecture & Design Documentation

## Executive Summary

This codebase implements a sophisticated **AI CLI Framework** designed to provide:
- Interactive command-line interface for Claude AI interactions
- Secure bridging between local and remote systems
- Extensible plugin architecture
- Comprehensive session and state management
- Enterprise-grade security and permissions
- Real-time cost and usage tracking

---

## High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     CLI Entry Point (main.tsx)              │
│  - Startup profiling                                        │
│  - Parallel initialization (MDM, Keychain)                 │
│  - Command routing                                          │
└──────────────────────┬──────────────────────────────────────┘
                       │
        ┌──────────────┼──────────────┐
        │              │              │
        ▼              ▼              ▼
   ┌─────────┐  ┌──────────┐  ┌────────────┐
   │Bootstrap │   │Context   │  │Plugin      │
   │System    │  │System    │  │System      │
   └─────────┘  └──────────┘  └────────────┘
        │
        ▼
┌─────────────────────────────────────────────────────────────┐
│               Command Dispatcher (commands.ts)              │
│  - 50+ commands registered                                  │
│  - Argument parsing (Commander.js)                         │
│  - Help and documentation                                   │
└─────────────────┬───────────────────────────────────────────┘
                  │
        ┌─────────┴──────────┬──────────────┬──────────────┐
        │                    │              │              │
        ▼                    ▼              ▼              ▼
    ┌───────┐          ┌──────────┐   ┌─────────┐   ┌──────────┐
    │Command │         │Query     │   │Service  │   │Bridge    │
    │Handler │         │Engine    │   │Layer    │   │System    │
    └───────┘         └──────────┘   └─────────┘   └──────────┘
        │
        ▼
┌─────────────────────────────────────────────────────────────┐
│              Service Layer (services/)                      │
│  ├─ API Services (Bootstrap, Files)                        │
│  ├─ Authentication (OAuth, JWT)                            │
│  ├─ Analytics (GrowthBook, Tracking)                       │
│  ├─ Policy & Permissions                                   │
│  ├─ Plugin Management                                      │
│  ├─ Session Memory                                         │
│  ├─ Settings Sync                                          │
│  └─ Tool Management                                        │
└──────────────┬──────────────────────────────────────────────┘
               │
   ┌───────────┼───────────┬──────────┐
   │           │           │          │
   ▼           ▼           ▼          ▼
┌──────┐  ┌────────┐  ┌──────┐  ┌────────┐
│Bridge│  │Storage │  │OAuth │  │Tools   │
│API   │  │(Keys)  │  │Prov  │  │Catalog │
└──────┘  └────────┘  └──────┘  └────────┘
   │
   ▼
┌─────────────────────────────────────────────────────────────┐
│        Bridge Communication System (bridge/)                │
│  - Message passing                                          │
│  - Session management                                       │
│  - Remote bridge core                                       │
│  - Permission callbacks                                     │
└──────────────┬──────────────────────────────────────────────┘
               │
   ┌───────────┼───────────┐
   │           │           │
   ▼           ▼           ▼
┌───────┐  ┌────────┐  ┌────────┐
│Local  │  │Remote  │  │REPL    │
│Ops    │  │Bridge  │  │Bridge  │
└───────┘  └────────┘  └────────┘
```

---

## Layered Architecture

### Layer 1: Presentation & CLI
- **Entry**: `main.tsx`
- **Components**: React + Ink for terminal UI
- **Output**: `cli/print.ts`, `outputStyles/`
- **Responsibility**: User interface and output formatting

### Layer 2: Command & Control
- **Command Router**: `commands.ts`
- **Command Handlers**: `commands/*/index.ts`
- **CLI Framework**: Commander.js
- **Responsibility**: Route user input to appropriate handlers

### Layer 3: Business Logic
- **query/**: Query processing and execution
- **services/**: Domain-specific business logic
- **tools/**: AI tool definitions and execution
- **tasks/**: Asynchronous task execution
- **Responsibility**: Core application logic

### Layer 4: Coordination
- **bridge/**: Inter-system communication
- **state/**: State management
- **context/**: Context provisioning
- **Responsibility**: System coordination and messaging

### Layer 5: Integration & External
- **services/api/**: External API calls
- **services/oauth/**: Authentication
- **services/plugins/**: Plugin system
- **remote/**: Remote operations
- **Responsibility**: External system integration

---

## Module Organization

### By Responsibility

#### 1. Authentication & Security (`bridge/`, `services/oauth/`, `utils/permissions/`)
```
Authentication Flow:
  User Input → OAuth → JWT Token → Keychain Storage → Session Creation
  
Permission Flow:
  Command → Permission Check → Policy Limits → Device Trust → Execution
```

**Key Components**:
- OAuth provider integration
- JWT token management
- Permission rules engine
- Policy limit enforcement
- Device trust tracking
- Secure credential storage

#### 2. Session Management (`bridge/`, `assistant/`)
```
Session Lifecycle:
  Initialize → Load → Execute Commands → Save State → Persist History
  
Session Features:
  - Multi-session support
  - Session history tracking
  - Memory persistence
  - Remote synchronization
```

**Key Components**:
- `bridge/createSession.ts` - Creation
- `bridge/sessionRunner.ts` - Execution
- `assistant/sessionHistory.ts` - History
- State persistence

#### 3. Command Execution (`commands/`, `QueryEngine.ts`, `tools.ts`)
```
Command Execution Pipeline:
  Parse Args → Load Command → Build Context → Execute →
  Collect Results → Format Output → Display
```

**Key Components**:
- 50+ command handlers
- Query engine for processing
- Tool registry and execution
- Output formatting

#### 4. Tool Management (`Tool.ts`, `tools/`, `services/tools/`)
```
Tool System:
  Define → Register → Validate → Execute → Return Results
  
Tool Features:
  - JSON schema-based definitions
  - Parameter validation
  - Error handling
  - Result formatting
```

**Key Components**:
- `Tool.ts` - Base class
- `tools.ts` - Registry
- `tools/` - Tool implementations
- Tool execution engine

#### 5. Analytics & Monitoring (`services/analytics/`, `cost-tracker.ts`, `services/diagnosticTracking.ts`)
```
Metrics Collection:
  Events → Aggregation → Storage → Analysis → Reporting
  
Key Metrics:
  - Token usage and costs
  - Command execution metrics
  - Feature adoption
  - Performance monitoring
```

**Key Components**:
- GrowthBook integration
- Diagnostic tracking
- Cost tracking
- Event logging

#### 6. Plugin System (`plugins/`, `services/plugins/`)
```
Plugin Lifecycle:
  Discover → Install → Load → Register → Execute → Cleanup
  
Plugin Types:
  - Commands
  - Hooks
  - Output styles
  - Tools
```

**Key Components**:
- Plugin discovery
- Marketplace integration
- Dependency resolution
- Lifecycle management
- Command/hook registration

---

## Data Structures

### Session
```typescript
Session {
  id: string
  user: UserContext
  system: SystemContext
  state: ApplicationState
  history: Message[]
  memory: SessionMemory
  startTime: Date
  lastActivity: Date
  remoteSync: RemoteSyncState
}
```

### Context
```typescript
Context {
  user: {
    id: string
    name: string
    settings: UserSettings
    preferences: UserPreferences
  }
  system: {
    platform: string
    environment: EnvConfig
    capabilities: SystemCapabilities
  }
  environment: {
    cwd: string
    vars: Record<string, string>
    git: GitState
  }
}
```

### Tool Definition
```typescript
Tool {
  name: string
  description: string
  parameters: JSONSchema
  execute: (input: unknown) => Promise<unknown>
  validate?: (input: unknown) => boolean
}
```

### Command Definition
```typescript
Command {
  name: string
  description: string
  arguments: Argument[]
  options: Option[]
  action: (args: any, options: any) => Promise<void>
  help?: string
}
```

---

## Key Design Patterns

### 1. Singleton Pattern
- Context providers
- Query engine instance
- Service registries

### 2. Factory Pattern
- Session creation
- Command instantiation
- Tool creation

### 3. Observer Pattern
- Event tracking
- Change notifications
- Analytics events

### 4. Middleware Pattern
- Permission checking
- Error handling
- Logging

### 5. Strategy Pattern
- Multiple bridge implementations
- Different output formatters
- Plugin variations

### 6. Dependency Injection
- Service provisioning
- Context injection via React
- Configuration passing

---

## Communication Patterns

### 1. Bridge Messaging
```
Local Process ──Message──> Bridge API ──Message──> Remote Process
          <──Response──<           <──Response──<
```

**Message Types**:
- Command execution
- State sync
- File operations
- Permission checks

### 2. Event System
```
Event Producer → Event Queue → Event Handlers → Analytics
```

**Event Types**:
- Command execution
- Tool invocation
- Permission decision
- Cost update

### 3. API Integration
```
CLI Command → Service Layer → API Client → External API → Response
```

**APIs Integrated**:
- Bootstrap API (initial data)
- Files API (file operations)
- OAuth providers
- MCP servers

---

## State Management Strategy

### Global State (via Context)
- User information
- System configuration
- Application settings
- Session metadata

### Component State (via React Hooks)
- UI state
- Form inputs
- Loading states
- Error states

### Persistent State
- History
- Session data
- User preferences
- Application settings

### Cache Layer
- Command results
- API responses
- Computed values
- Configuration

**State Flow**:
```
User Action → Component State Update →
Context Update → Persistence → Notification
```

---

## Error Handling Strategy

### Three-Tier Error Handling

#### 1. Immediate Error Handling
```typescript
try {
  // Command execution
} catch (error) {
  // Handle specific error
  logError(error)
  return ErrorResult
}
```

#### 2. Service-Level Error Handling
```typescript
// Try command
// On failure, attempt recovery
// If recovery fails, escalate
```

#### 3. Global Error Handler
```typescript
// Catch uncaught errors
// Format for user
// Provide recovery options
```

### Error Types
- **Validation Errors**: Input validation
- **Permission Errors**: Access denied
- **Resource Errors**: File not found
- **API Errors**: External service failures
- **Network Errors**: Connection issues
- **Internal Errors**: Logic failures

---

## Performance Architecture

### Startup Optimization
```
Sequential Initialization:
  1. profileCheckpoint('entry')
  2. startMdmRawRead() - Parallel in background
  3. startKeychainPrefetch() - Parallel in background
  4. Import heavy modules
  5. Initialize services
  6. Ready for commands
```

**Result**: ~50% reduction in startup time

### Runtime Optimization
```
Memoization:
  - Context memoization
  - Command memoization
  - Computed values caching

Lazy Loading:
  - Plugin loading on demand
  - Command loading on use
  - Service initialization

Batching:
  - Request batching to APIs
  - Event batching for analytics
  - State update batching
```

### Memory Optimization
```
Resource Management:
  - Stream processing for large data
  - Cleanup on command completion
  - Cache eviction policies
  - Garbage collection tuning
```

---

## Security Architecture

### Authentication Flow
```
1. User initiates login
2. OAuth provider redirect
3. Authorization code obtained
4. Exchange code for tokens
5. Store in secure keychain
6. Session created
7. Token refreshed as needed
```

### Permission System
```
1. Command invoked
2. Permission rules evaluated
3. Policy limits checked
4. Device trust verified
5. Execute if allowed, deny otherwise
6. Track decision
```

### Data Security
```
Sensitive Data:
  - Tokens → Keychain storage
  - Credentials → Encrypted at rest
  - API Keys → Environment variables
  - Secrets → Workspace secrets

Transport Security:
  - HTTPS for remote operations
  - Message signing/verification
```

---

## Extensibility Architecture

### Plugin System
```
Plugin Discovery:
  1. Scan plugin directories
  2. Load plugin manifests
  3. Validate dependencies
  4. Check compatibility

Plugin Loading:
  1. Require plugin module
  2. Register commands
  3. Register hooks
  4. Register tools
  5. Start plugin

Plugin Execution:
  1. Route to plugin handler
  2. Execute with context
  3. Capture output
  4. Return results
```

### Command Extension
```
Built-in Commands: 50+ core commands
Plugin Commands: Dynamic command registration
Hook System: Intercept and modify behavior
Output Styles: Custom formatting
```

### Tool Extension
```
Built-in Tools: Core AI tools
Plugin Tools: Register custom tools
Tool Marketplace: Published tools
```

---

## Integration Points

### External Systems
```
1. OAuth Providers (Google, GitHub, etc.)
   - Authentication
   - User information
   - Permissions

2. Git/GitHub
   - Commit operations
   - PR management
   - Issue tracking

3. Slack
   - Notifications
   - Team coordination
   - Integration

4. MCP Servers
   - Tool expansion
   - Model capabilities
   - Custom protocols

5. Voice Services
   - Speech recognition
   - Text-to-speech
   - Voice commands

6. Analytics
   - GrowthBook (feature flags)
   - Custom telemetry
   - Usage tracking
```

---

## Deployment & Runtime

### Deployment Models

#### 1. Standalone CLI
- Single binary or script
- Local execution
- Direct system access

#### 2. Server Mode
- Runs as background service
- Remote bridge enabled
- Session persistence

#### 3. Plugin Mode
- Loaded by host application
- Shared runtime
- Coordinated execution

### Runtime Requirements
- Node.js/Bun runtime
- File system access
- Network access (optional)
- Secure storage (Keychain/TPM)

### Configuration Management
```
Config Resolution:
  1. Environment variables (highest priority)
  2. MDM policies
  3. Remote managed settings
  4. Local config files
  5. Defaults (lowest priority)

Config Areas:
  - API endpoints
  - Feature flags
  - Policy limits
  - Plugin settings
  - Output preferences
```

---

## Monitoring & Observability

### Logging
```
Levels:
  - ERROR: Critical failures
  - WARN: Recoverable issues
  - INFO: Important events
  - DEBUG: Detailed execution
  - TRACE: Complete flow

Sinks:
  - Console output
  - File logs
  - Remote logging
  - Diagnostic tracking
```

### Metrics
```
Categories:
  - Performance (latency, throughput)
  - Business (commands, features)
  - Technical (errors, resources)
  - Security (permissions, access)

Collection:
  - Real-time metrics
  - Aggregated metrics
  - Trend analysis
```

### Tracing
```
Startup Profiling:
  - checkpoints at key stages
  - timing measurements
  - dependency analysis
  - bottleneck identification
```

---

## Testing Strategy

### Unit Testing
- Individual functions
- Utilities
- Services
- Commands

### Integration Testing
- Service interactions
- Command execution
- Bridge communication
- API integrations

### E2E Testing
- Full workflows
- Multi-command sequences
- Real data scenarios
- Error scenarios

### Performance Testing
- Startup time
- Command latency
- Memory usage
- API response times

---

## Future Architecture Considerations

### Planned Improvements
- Enhanced plugin marketplace
- Advanced analytics dashboard
- Improved performance monitoring
- Expanded OAuth providers
- Better plugin sandboxing
- Distributed session management

### Scalability
- Multi-user sessions
- High-volume command processing
- Large data handling
- Remote infrastructure

---

## Architecture Decision Records (ADRs)

### ADR-1: Bun Runtime
**Decision**: Use Bun for runtime
**Rationale**: Performance, TypeScript support, native module handling
**Tradeoffs**: Limited Node.js compatibility, newer ecosystem

### ADR-2: React for CLI
**Decision**: Use React + Ink for CLI UI
**Rationale**: Component reusability, rich interactions, better structure
**Tradeoffs**: Overkill for simple commands, learning curve

### ADR-3: Bridge Architecture
**Decision**: Separate bridge for local/remote communication
**Rationale**: Clean separation, flexibility, future-proof
**Tradeoffs**: Complexity, message overhead

### ADR-4: Plugin System
**Decision**: Dynamic plugin loading with marketplace
**Rationale**: Extensibility, community contributions, modularity
**Tradeoffs**: Security considerations, dependency management

---

**Document Version**: 1.0  
**Last Updated**: April 2026  
**Architecture Owner**: Engineering Team
