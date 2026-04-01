# Detailed Codebase Reference

## Complete Directory Structure & Purpose

### Root Level Files

| File | Purpose |
|------|---------|
| `main.tsx` | Entry point for CLI application with startup profiling |
| `commands.ts` | Central registry for all CLI commands |
| `context.ts` | Global context management (user, system, environment) |
| `history.ts` | Session history tracking and persistence |
| `cost-tracker.ts` | Token usage and cost calculation |
| `costHook.ts` | React hook for cost tracking |
| `QueryEngine.ts` | Core engine for query processing and execution |
| `Task.ts` | Task class for async execution |
| `Tool.ts` | Base class and interfaces for tools |
| `tasks.ts` | Task registry and utilities |
| `tools.ts` | Tool registry and utilities |
| `ink.ts` | Ink terminal UI setup and utilities |
| `replLauncher.tsx` | REPL launch component |
| `dialogLaunchers.tsx` | Dialog launching utilities |
| `interactiveHelpers.tsx` | Interactive UI helpers |
| `projectOnboardingState.ts` | Project onboarding state management |
| `setup.ts` | Initial setup and configuration |

---

## Core Modules

### 1. Assistant Module (`assistant/`)
- `sessionHistory.ts` - Manages conversation history within sessions

**Purpose**: Handle AI assistant interactions and conversation state

### 2. Bootstrap Module (`bootstrap/`)
- `state.ts` - Bootstrap state management
  - Cached Claude.md content
  - Additional directory information
  - Initial configuration loading

**Purpose**: Initialize application state on startup

### 3. Bridge Module (`bridge/`)
Complete message passing and session management system

**Key Files**:
- `bridgeMain.ts` - Main bridge orchestration
- `replBridge.ts` - REPL-specific bridge
- `bridgeMessaging.ts` - Message handling and routing
- `bridgeUI.ts` - UI integration for bridge
- `bridgeStatusUtil.ts` - Status tracking
- `bridgeAPI.ts` - API interface
- `bridgeConfig.ts` - Configuration
- `bridgeDebug.ts` - Debugging utilities
- `bridgeEnabled.ts` - Feature flags
- `bridgePermissionCallbacks.ts` - Permission handling
- `bridgePointer.ts` - Pointer/reference management
- `remoteBridgeCore.ts` - Remote bridge implementation
- `replBridgeHandle.ts` - Bridge handle management
- `replBridgeTransport.ts` - Transport layer
- `codeSessionApi.ts` - Code execution API
- `createSession.ts` - Session creation
- `sessionRunner.ts` - Session execution
- `sessionIdCompat.ts` - Session ID compatibility
- `workSecret.ts` - Workspace secrets
- `trustedDevice.ts` - Device trust management
- `jwtUtils.ts` - JWT token utilities
- `debugUtils.ts` - Debug utilities
- `flushGate.ts` - Message flushing control
- `inboundMessages.ts` - Inbound message handling
- `inboundAttachments.ts` - File attachment handling
- `initReplBridge.ts` - Bridge initialization
- `pollConfig.ts` & `pollConfigDefaults.ts` - Polling configuration
- `capacityWake.ts` - Capacity management
- `types.ts` - Bridge type definitions

**Purpose**: Enable communication between local and remote systems, manage sessions, handle permissions

### 4. Buddy Module (`buddy/`)
Companion system for interactive assistance

**Files**:
- `companion.ts` - Companion logic
- `CompanionSprite.tsx` - Visual sprite component
- `prompt.ts` - Prompting utilities
- `sprites.ts` - Sprite definitions
- `types.ts` - Type definitions
- `useBuddyNotification.tsx` - Notification hook

**Purpose**: Provide interactive buddy/companion features

### 5. CLI Module (`cli/`)
Command-line output and transport handling

**Files**:
- `exit.ts` - Process exit handling
- `print.ts` - Terminal printing
- `remoteIO.ts` - Remote I/O
- `structuredIO.ts` - Structured output
- `update.ts` - Update notifications
- `ndjsonSafeStringify.ts` - NDJSON serialization
- `handlers/` - Output handlers
- `transports/` - Transport mechanisms

**Purpose**: Handle all CLI output and input operations

### 6. Commands Module (`commands/`)
50+ command implementations organized by category

**Subdirectories**:
- `agents/` - Agent-related commands
- `add-dir/` - Directory management
- `autofix-pr/` - PR auto-fixing
- `backfill-sessions/` - Session recovery
- `branch/` - Git branch operations
- `bridge/` - Bridge commands
- `commit.ts` - Git commit assistance
- `commit-push-pr.ts` - Full PR workflow
- `config/` - Configuration commands
- `context/` - Context management
- `cost/` - Cost tracking
- `debug-tool-call/` - Tool debugging
- `diff/` - Code diff analysis
- `export/` - Data export
- `help/` - Help system
- `init/` - Initialization
- `login/`/`logout/` - Authentication
- `mcp/` - MCP server management
- `mobile/` - Mobile features
- `plugins/` - Plugin management
- `review/` - Code review
- `session/` - Session management
- `skills/` - Skill management
- `tasks/` - Task operations
- `voice/` - Voice features
- And 20+ more...

**Purpose**: Implement all CLI commands with specific functionality

### 7. Components Module (`components/`)
React components for rendering

**Purpose**: Reusable UI components for CLI and interactive features

### 8. Constants Module (`constants/`)
Application-wide constants

**Common Files**:
- `oauth.ts` - OAuth configuration
- `product.ts` - Product information
- `common.ts` - Common constants

**Purpose**: Centralize constant values

### 9. Context Module (`context/`)
Context-specific logic and providers

**Purpose**: Manage application context and environment data

### 10. Coordinator Module (`coordinator/`)
Coordination logic for complex operations

**Purpose**: Orchestrate multi-step workflows

### 11. Entrypoints Module (`entrypoints/`)
Application initialization entry points

**Files**:
- `init.ts` - Main initialization

**Purpose**: Define how application starts

### 12. Hooks Module (`hooks/`)
Custom React hooks

**Purpose**: Reusable hook logic for state and effects

### 13. Ink Module (`ink/`)
Terminal UI with Ink framework

**Files**:
- Terminal rendering components
- Box layouts
- Color and styling

**Purpose**: Terminal-based UI rendering

### 14. Keybindings Module (`keybindings/`)
Keyboard shortcut definitions

**Purpose**: Map keyboard inputs to actions

### 15. Memory Module (`memdir/`)
Memory file management

**Purpose**: Manage persistent memory/knowledge files

### 16. Migrations Module (`migrations/`)
Database and state migrations

**Purpose**: Handle version upgrades and data transformations

### 17. Native Module (`native-ts/`)
Native code bindings

**Purpose**: Integration with native libraries if needed

### 18. Output Styles Module (`outputStyles/`)
Terminal output styling definitions

**Purpose**: Define consistent output formatting

### 19. Plugins Module (`plugins/`)
Plugin system implementation

**Features**:
- Plugin discovery
- Marketplace integration
- Command/hook registration
- Lifecycle management

**Purpose**: Enable extensibility through plugins

### 20. Query Module (`query/`)
Query engine and processing

**Files**:
- Query execution
- Query parsing
- Query optimization

**Purpose**: Process and execute queries

### 21. Remote Module (`remote/`)
Remote operations and APIs

**Purpose**: Handle remote server interactions

### 22. Schemas Module (`schemas/`)
Data validation schemas

**Purpose**: Define and validate data structures

### 23. Screens Module (`screens/`)
Screen/page components

**Purpose**: Define different UI screens

### 24. Server Module (`server/`)
Server-side logic

**Purpose**: Backend functionality

### 25. Services Module (`services/`)
Business logic services

**Key Services**:
- `api/` - API integrations (bootstrap, files)
- `analytics/` - Analytics (GrowthBook, tracking)
- `mcp/` - Model Context Protocol
- `oauth/` - OAuth authentication
- `policyLimits/` - Policy enforcement
- `plugins/` - Plugin management system
- `remoteManagedSettings/` - Remote configuration
- `SessionMemory/` - Session memory
- `settingsSync/` - Settings synchronization
- `lsp/` - Language server protocol
- `tools/` - Tool management

**Purpose**: Centralized business logic

### 26. Skills Module (`skills/`)
Skills/capabilities system

**Purpose**: Define and manage AI skills

### 27. State Module (`state/`)
State management

**Purpose**: Application state persistence and management

### 28. Tasks Module (`tasks/`)
Task management system

**Purpose**: Define and execute tasks

### 29. Tools Module (`tools/`)
Tool definitions and registry

**Purpose**: Available tools for AI operations

### 30. Types Module (`types/`)
TypeScript type definitions

**Purpose**: Type safety throughout codebase

### 31. Upstream Proxy Module (`upstreamproxy/`)
Upstream proxy handling

**Purpose**: Forward requests to upstream services

### 32. Utils Module (`utils/`)
Comprehensive utility functions

**Major Utilities**:
- `git.ts` - Git operations
- `array.ts` - Array utilities
- `log.ts` - Logging
- `execFileNoThrow.ts` - Safe command execution
- `envUtils.ts` - Environment handling
- `claudemd.ts` - Claude.md processing
- `diagLogs.ts` - Diagnostic logging
- `memoize.ts` - Memoization
- `startup*` - Startup optimizations
- `permissions/` - Permission system
- `model/` - Model configuration
- `settings/` - Settings management
- `secureStorage/` - Secure credential storage
- `plugins/` - Plugin utilities
- `memory/` - Memory utilities
- And many more...

**Purpose**: Reusable utility functions

### 33. Vim Module (`vim/`)
Vi/Vim editor integration

**Purpose**: Vim keybindings and integration

### 34. Voice Module (`voice/`)
Voice interaction features

**Files**:
- Voice recognition
- Voice output
- Keyword terms

**Purpose**: Voice interface support

---

## Architecture Patterns

### 1. Command Pattern
Each command is a module with:
- Handler function
- Help text
- Argument parsing
- Error handling

### 2. Service Locator Pattern
Services accessed through:
- Context providers
- Utility functions
- Service registries

### 3. Observer Pattern
- Event tracking/analytics
- Telemetry
- State change notifications

### 4. Factory Pattern
- Session creation
- Command instantiation
- Tool creation

### 5. Middleware Pattern
- Permission checking
- Logging
- Error handling

---

## Data Flow Examples

### Command Execution Flow
```
User Input
    ↓
Command Parser (Commander.js)
    ↓
Command Registry (commands/index)
    ↓
Command Handler
    ↓
Service Layer (services/)
    ↓
API/Bridge (bridge/, services/api/)
    ↓
State Update (state/)
    ↓
Output Rendering (Ink/CLI)
    ↓
Terminal Output
```

### Session Initialization Flow
```
main.tsx Entry
    ↓
Bootstrap (bootstrap/state.ts)
    ↓
Load Configuration
    ↓
Initialize Context (context.ts)
    ↓
Load Plugins (plugins/)
    ↓
Setup Services (services/)
    ↓
Ready for Commands
```

### Query Processing Flow
```
User Query
    ↓
QueryEngine.ts
    ↓
Parse & Validate
    ↓
Tool Selection
    ↓
Execute Tools (tools/)
    ↓
Aggregate Results
    ↓
Format Output
    ↓
Display Result
```

---

## Key Features & Components

### Authentication
- OAuth integration (`services/oauth/`)
- JWT token management (`bridge/jwtUtils.ts`)
- Secure credential storage (`utils/secureStorage/`)
- Keychain integration (macOS/Linux)

### Communication
- Bridge messaging (`bridge/bridgeMessaging.ts`)
- Remote operations (`remote/`)
- Session management (`bridge/sessionRunner.ts`)
- Message queuing

### Permissions & Security
- Permission rules system (`utils/permissions/`)
- Policy limits enforcement (`services/policyLimits/`)
- Device trust tracking (`bridge/trustedDevice.ts`)
- Secure operations

### Performance
- Startup profiling (`utils/startupProfiler.ts`)
- Memoization throughout codebase
- Parallel initialization (MDM, Keychain)
- Lazy command loading
- Caching (config, metadata)

### Analytics & Monitoring
- GrowthBook integration (`services/analytics/growthbook.ts`)
- Diagnostic tracking (`services/diagnosticTracking.ts`)
- Cost tracking (`cost-tracker.ts`)
- Usage analytics

### Extensibility
- Plugin system (`plugins/`, `services/plugins/`)
- Custom commands
- Custom tools (`tools/`)
- Hook system (`commands/hooks/`)

---

## Configuration Management

### Configuration Sources (Priority Order)
1. Environment variables
2. MDM (Mobile Device Management)
3. Local .env files
4. Remote managed settings (`services/remoteManagedSettings/`)
5. Default configuration

### Key Configuration Areas
- API endpoints
- Feature flags
- Policy limits
- Plugin settings
- Performance tuning
- Security policies

---

## Important Utilities

### File Operations
- `execFileNoThrow.ts` - Safe command execution
- Git utilities in `utils/git.ts`
- File API in `services/api/filesApi.ts`

### Environment & System
- `envUtils.ts` - Environment variable parsing
- `platform.ts` - Platform detection
- Settings in `utils/settings/`

### Data Validation
- Schemas in `schemas/`
- Type checking with TypeScript
- Permission validation

### Logging & Diagnostics
- `utils/log.ts` - Logging system
- `diagLogs.ts` - Diagnostic logging
- `debugUtils.ts` in bridge

### State Management
- React hooks system
- Memoization utilities
- Context providers

---

## Development Workflow

### Adding a New Command
1. Create directory in `commands/<command-name>/`
2. Implement `index.ts` with command handler
3. Register in `commands.ts`
4. Add help text and documentation
5. Test with: `bun run ./main.tsx <command>`

### Adding a New Service
1. Create module in `services/<service-name>/`
2. Implement main logic
3. Export public interface
4. Use in commands or other services
5. Add telemetry if needed

### Adding a New Tool
1. Define in `tools/<tool-name>.ts`
2. Implement tool interface from `Tool.ts`
3. Register in `tools.ts`
4. Document parameters and outputs
5. Add error handling

### Adding a Plugin
1. Create plugin directory structure
2. Implement commands/hooks as needed
3. Define package.json with metadata
4. Publish to marketplace
5. Users can install via `plugin install`

---

## Testing Considerations

### Unit Testing
- Individual function testing
- Service testing
- Utility testing

### Integration Testing
- Command execution
- Bridge communication
- API interactions

### E2E Testing
- Full workflow testing
- Session management
- Multi-step operations

---

## Performance Optimization Techniques

1. **Startup Optimization**
   - Profile checkpoints
   - Parallel initialization
   - Lazy imports

2. **Runtime Optimization**
   - Memoization
   - Caching
   - Debouncing

3. **Memory Optimization**
   - Garbage collection awareness
   - Cleanup on unmount
   - Stream processing for large data

4. **API Optimization**
   - Request batching
   - Response caching
   - Connection pooling

---

## Dependencies (Inferred)

### Core
- `@commander-js/extra-typings` - CLI argument parsing
- `chalk` - Terminal colors
- `react` - UI library
- `bun` - runtime

### File Operations
- `fs` - File system

### Data Processing
- `lodash-es` - Utility functions

### Terminal UI
- `ink` - Terminal React framework

### Authentication
- OAuth providers
- JWT handling

### Utilities
- Various internal utilities

---

## Environment Variables

Common environment variables used:
- `NODE_ENV` - Development/production
- `USER_TYPE` - User classification (ant/regular)
- Git-related variables
- API keys and tokens
- Feature flags

---

## Known Integrations

1. **OAuth Providers** - Third-party authentication
2. **Git/GitHub** - Version control and PR management
3. **Slack** - Team collaboration
4. **MCP Servers** - Model Context Protocol
5. **Voice Services** - Voice I/O
6. **Analytics** - GrowthBook, custom tracking

---

## Troubleshooting Guide

### Startup Issues
- Check `utils/startupProfiler.ts` logs
- Verify environment variables
- Check keychain/MDM access

### Command Failures
- Use `doctor` command for diagnostics
- Check command-specific `--help`
- Review error logs

### Performance Issues
- Profile with startup profiler
- Check memory usage
- Review cache hit rates
- Monitor API calls

### Permission Issues
- Review `utils/permissions/`
- Check policy limits
- Verify device trust status

---

**Document Version**: 1.0  
**Last Updated**: April 2026  
**Repository**: https://github.com/cyber-bytezz/claude-code.git
