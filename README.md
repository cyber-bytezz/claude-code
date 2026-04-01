# Claude Code Repository

A comprehensive TypeScript/React-based CLI and integration framework for Claude AI interactions. This is a multi-faceted project that provides command-line utilities, bridge integrations, and rich interactive experiences for working with Claude.

## 📋 Table of Contents

- [Overview](#overview)
- [Project Structure](#project-structure)
- [Technology Stack](#technology-stack)
- [Key Components](#key-components)
- [Commands](#commands)
- [Services](#services)
- [Architecture](#architecture)
- [Getting Started](#getting-started)

## Overview

This codebase is a sophisticated CLI framework that:
- Manages Claude AI interactions through a command-line interface
- Provides bridging capabilities for integrating Claude with various systems
- Offers rich interactive UI components built with React and Ink
- Handles authentication, configuration, and session management
- Includes extensive plugin and extension support
- Manages costs, usage tracking, and permissions

## Project Structure

```
src/
├── assistant/              # Assistant-related core functionality
├── bootstrap/              # Application bootstrapping and initialization
├── bridge/                 # Bridge integrations for external systems
├── buddy/                  # Companion/buddy system features
├── cli/                    # Command-line interface utilities
├── commands/               # Command implementations (50+ commands)
├── components/             # React components for UI rendering
├── constants/              # Application constants
├── context/               # Context management and user context
├── coordinator/           # Coordination logic
├── entrypoints/          # Application entry points
├── hooks/                # Custom React hooks
├── ink/                  # Ink terminal UI utilities
├── keybindings/          # Keyboard binding definitions
├── memdir/               # Memory directory management
├── migrations/           # Database/state migrations
├── moreright/            # Additional utility functions
├── native-ts/            # Native code bindings
├── outputStyles/         # Output formatting styles
├── plugins/              # Plugin system and management
├── query/                # Query engine implementation
├── remote/               # Remote interaction utilities
├── schemas/              # Data validation schemas
├── screens/              # Screen/page components
├── server/               # Server-side logic
├── services/             # Business logic services
├── skills/               # Skills/capabilities system
├── state/                # State management
├── tasks/                # Task execution and management
├── tools/                # Tool definitions and handlers
├── types/                # TypeScript type definitions
├── upstreamproxy/        # Upstream proxy functionality
├── utils/                # Utility functions
├── vim/                  # Vi/Vim integration
├── voice/                # Voice interaction features
├── main.tsx              # Main entry point
├── commands.ts           # Command registry
├── context.ts            # Context provider
├── cost-tracker.ts       # Cost tracking logic
├── history.ts            # History management
├── QueryEngine.ts        # Query execution engine
├── Task.ts              # Task class definitions
├── Tool.ts              # Tool class definitions
└── tools.ts             # Tool registry
```

## Technology Stack

- **Language**: TypeScript
- **Runtime**: Bun (as indicated by build configuration)
- **UI Framework**: React + Ink (terminal UI)
- **CLI Framework**: Commander.js (extra-typings)
- **Styling**: Chalk (terminal colors)
- **State Management**: React hooks and memoization
- **Configuration Management**: MDM (Mobile Device Management), environment variables
- **Authentication**: OAuth, JWT, Keychain

## Key Components

### 1. **Commands System**
The `commands/` directory contains 50+ command implementations including:

#### Core Commands
- `init` - Initialize new sessions
- `login`/`logout` - Authentication
- `status` - Status information
- `help` - Help documentation

#### Git & Dev Tools
- `commit` - Git commit assistance
- `commit-push-pr` - Full PR workflow
- `diff` - Diff analysis
- `review` - Code review
- `branch` - Branch management

#### AI Features
- `advisor` - AI advisor functionality
- `agents` - Agent orchestration
- `brief` - Brief generation
- `summary` - Session summaries
- `thinkback` - Thinking/reflection features

#### Productivity
- `tasks` - Task management
- `context` - Context management
- `memory` - Memory/knowledge management
- `resume` - Resume interrupted sessions
- `session` - Session management

#### Configuration & Analytics
- `config` - Configuration settings
- `cost` - Cost tracking
- `usage` - Usage analytics
- `permissions` - Permission management
- `settings` - Application settings

#### Advanced Features
- `mobile` - Mobile integration
- `voice` - Voice interaction
- `desktop` - Desktop features
- `mcp` - MCP server management
- `plugins` - Plugin management
- `skills` - Skills catalog

### 2. **Bridge System**
The `bridge/` directory provides message passing and session management:
- `bridgeMain.ts` - Main bridge logic
- `replBridge.ts` - REPL bridge implementation
- `bridgeMessaging.ts` - Message handling
- `bridgePermissionCallbacks.ts` - Permission management
- `remoteBridgeCore.ts` - Remote bridge core
- Supports both local and remote communication

### 3. **Services**
The `services/` directory contains business logic:
- `analytics/` - Analytics and GrowthBook
- `api/` - API integration (bootstrap, files)
- `mcp/` - Model Context Protocol integration
- `oauth/` - OAuth authentication
- `plugins/` - Plugin management
- `policyLimits/` - Policy enforcement
- `remoteManagedSettings/` - Remote configuration
- `SessionMemory/` - Session memory management

### 4. **UI Components**
- React components in `components/`
- Terminal UI with Ink in `ink/`
- Dialog launchers for interactive prompts
- Output styling system

### 5. **State Management**
- Context-based state with `context.ts`
- Bootstrap state in `bootstrap/state.ts`
- Memoization for performance optimization
- Hooks system in `hooks/`

### 6. **Configuration**
- Environment-based configuration
- MDM (Mobile Device Management) integration
- Keychain/secure storage integration
- Remote managed settings

### 7. **Tool System**
Custom tool implementation with:
- Tool registry in `tools.ts`
- Tool definitions in `Tool.ts`
- Tool catalog in `tools/` directory
- JSON schema-based tool definitions

### 8. **Query Engine**
- `QueryEngine.ts` - Main query processing
- `query.ts` - Query utilities
- `query/` - Query-related modules

## Commands

The CLI supports 50+ commands organized into categories:

### Development
- `commit` - Intelligent commit message generation
- `commit-push-pr` - Full workflow automation
- `diff` - Code diff analysis
- `review` - Code review assistance
- `branch` - Branch management
- `issue` - Issue tracking

### AI & Analysis
- `advisor` - AI advisor mode
- `brief` - Generate briefings
- `summary` - Summarize sessions
- `thinkback` - Reflective analysis
- `bughunter` - Bug detection

### Content & Knowledge
- `memory` - Knowledge management
- `context` - Context control
- `skills` - Skill management
- `knowledge` - Knowledge base

### Configuration
- `config` - Settings management
- `login`/`logout` - Authentication
- `permissions` - Permission settings
- `keybindings` - Keyboard shortcuts
- `theme` - Theme customization

### Productivity
- `tasks` - Task tracking
- `session` - Session management
- `resume` - Resume sessions
- `copy` - Copy utilities
- `export` - Data export

### Analytics & Monitoring
- `cost` - Cost monitoring
- `usage` - Usage analytics
- `status` - System status
- `doctor` - Diagnostics

### Integration
- `mcp` - MCP server management
- `plugins` - Plugin system
- `mobile` - Mobile features
- `voice` - Voice interaction
- `desktop` - Desktop integration

## Services

### Analytics & Monitoring
- **GrowthBook**: Feature flag management
- **Diagnostic Tracking**: Event tracking
- **Cost Tracking**: Token and API cost monitoring
- **Usage Analytics**: User behavior tracking

### API Integration
- **Bootstrap API**: Initial data loading
- **Files API**: File management
- **OAuth**: Third-party authentication
- **Referral System**: Referral tracking

### Plugin System
- Plugin discovery and installation
- Marketplace integration
- Dependency resolution
- Plugin lifecycle management

### Session Management
- Multi-session support
- Session memory persistence
- Session history tracking
- Backfill and recovery

### Security
- Permission system with rules
- Policy limits enforcement
- Secure credential storage (Keychain/secure store)
- JWT token management
- Trusted device tracking

## Architecture

### Data Flow
1. **Entry Point** (`main.tsx`) - Application initialization
2. **Bootstrap** - Load initial configuration and data
3. **Command Dispatch** - Route to command handlers
4. **Service Layer** - Execute business logic
5. **State Management** - Update application state
6. **Output Rendering** - Render results via Ink/terminal

### Session Management
- Sessions track conversation state
- Persistent session history
- Session recovery and resumption
- Remote session synchronization

### Bridge Architecture
- Message-based communication
- Session isolation
- Permission callbacks
- Remote bridge support

### Plugin System
- Dynamic plugin loading
- Command and hook registration
- Service integration
- Lifecycle management

## Getting Started

### Prerequisites
- Node.js/Bun runtime
- TypeScript knowledge for development
- Git for version control

### Installation
```bash
# Clone repository
git clone https://github.com/cyber-bytezz/claude-code.git

# Install dependencies (if package.json exists)
npm install
# or
bun install

# Initialize application
bun run ./main.tsx init
```

### Basic Usage
```bash
# Get help
bun run ./main.tsx help

# Initialize new session
bun run ./main.tsx init

# Login
bun run ./main.tsx login

# Run a command
bun run ./main.tsx <command> [options]
```

### Common Commands
```bash
# Manage configuration
bun run ./main.tsx config set <key> <value>

# View usage/cost
bun run ./main.tsx cost

# Manage tasks
bun run ./main.tsx tasks add <task>

# Begin session
bun run ./main.tsx session start

# Get system status
bun run ./main.tsx status
```

## Key Files

| File | Purpose |
|------|---------|
| `main.tsx` | Application entry point with startup profiling |
| `commands.ts` | Command registry and routing |
| `context.ts` | Context management (user, system, environment) |
| `QueryEngine.ts` | Core query processing engine |
| `Tool.ts` | Tool base class and definitions |
| `Task.ts` | Task execution framework |
| `tool.ts` | Tool registry |
| `tools.ts` | Tool catalog and utilities |
| `history.ts` | Session history management |
| `cost-tracker.ts` | Token and cost tracking |

## Performance Optimizations

- **Startup Profiling**: Profile checkpoint tracking from entry
- **Parallel Initialization**: MDM and keychain reads run in parallel
- **Memoization**: Context memoization for performance
- **Lazy Loading**: On-demand module loading for commands
- **Caching**: Configuration and metadata caching

## Development Guidelines

### Adding Commands
1. Create new command file in `commands/<command-name>/`
2. Implement command handler
3. Register in `commands.ts`
4. Add help documentation

### Adding Services
1. Create service module in `services/`
2. Implement business logic
3. Export public API
4. Integrate with command handlers

### Adding Tools
1. Define tool interface in `Tool.ts`
2. Implement tool in `tools/`
3. Register in `tools.ts`
4. Document tool usage

### State Management
Use React hooks and context for state:
- `useState` for local component state
- `useCallback` for memoized functions
- Custom hooks for shared logic
- Context for global state

## External Integrations

- **OAuth Providers**: Multiple OAuth integrations
- **Git**: Git integration for commits, branches
- **GitHub**: PR and issue management
- **Slack**: Slack app integration
- **MCP Servers**: Model Context Protocol
- **Voice Services**: Voice input/output
- **Desktop**: Platform-specific integrations

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Ensure TypeScript compilation passes
5. Commit with meaningful messages
6. Push and create a pull request

## License

See repository for license information.

## Support

For issues, questions, or contributions:
- Check the `help` command: `bun run ./main.tsx help`
- Review command-specific help: `bun run ./main.tsx <command> --help`
- Check existing issues and documentation

---

**Last Updated**: April 2026  
**Repository**: https://github.com/cyber-bytezz/claude-code.git
