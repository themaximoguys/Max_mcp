<div align="center">

# IBM Maximo MAS 9.x MCP Server

### By The Maximo Guys

#### The most comprehensive Model Context Protocol server for IBM Maximo Application Suite

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Node.js Version](https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen)](https://nodejs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.2+-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![MCP SDK](https://img.shields.io/badge/MCP_SDK-0.5+-blueviolet)](https://modelcontextprotocol.io/)
[![Build Status](https://img.shields.io/badge/build-passing-brightgreen)]()
[![Coverage](https://img.shields.io/badge/coverage-%3E70%25-green)]()
[![npm version](https://img.shields.io/npm/v/@themaximoguys/maximo-mcp?logo=npm)](https://www.npmjs.com/package/@themaximoguys/maximo-mcp)
[![Docker](https://img.shields.io/badge/Docker-ready-2496ED?logo=docker&logoColor=white)]()

**175 tools** across **20 modules** — Work Orders, Assets, Inventory, Service Requests, Purchase Orders, Preventive Maintenance, Job Plans, Persons & Labor, Locations, Classifications, Attachments, Analytics, Scheduling, Query & Search, Bulk Operations, Developer Tools, Security Groups, Automation Scripts & Admin, Domain Setup, and Integration Utilities.

[Quick Start](#-quick-start) · [Documentation](#-documentation) · [Examples](#-usage-examples)

</div>

---

## Table of Contents

- [Overview](#-overview)
- [Supported Modules](#-supported-modules)
- [Quick Start](#-quick-start)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Configuration](#configuration)
  - [Claude Desktop Integration](#claude-desktop-integration)
- [Docker](#-docker)
  - [Quick Start with Docker](#quick-start-with-docker)
  - [Docker Compose](#docker-compose)
  - [Claude Desktop with Docker](#claude-desktop-with-docker)
- [Usage Examples](#-usage-examples)
  - [Work Orders](#work-orders)
  - [Assets](#assets)
  - [Inventory](#inventory)
  - [Service Requests](#service-requests)
  - [Purchase Orders](#purchase-orders)
  - [Preventive Maintenance](#preventive-maintenance)
  - [Analytics & Reporting](#analytics--reporting)
  - [OSLC Queries](#oslc-queries)
  - [Bulk Operations](#bulk-operations)
- [Architecture](#-architecture)
  - [High-Level Design](#high-level-design)
  - [Module Structure](#module-structure)
  - [Project Structure](#project-structure)
  - [Core Infrastructure](#core-infrastructure)
- [Configuration Reference](#-configuration-reference)
- [Development](#-development)
  - [Building from Source](#building-from-source)
  - [Testing](#testing)
  - [Code Quality](#code-quality)
- [Performance](#-performance)
- [Troubleshooting](#-troubleshooting)
- [FAQ](#-faq)
- [Security](#-security)
- [Contributing](#-contributing)
- [Roadmap](#-roadmap)
- [License](#-license)
- [Acknowledgments](#-acknowledgments)

---

## Overview

This MCP server enables AI assistants (like Claude) and developers to interact with IBM Maximo Application Suite 9.x through **175 purpose-built tools** spanning every major Maximo functional area. Designed for enterprise development, testing, and automation workflows.

### Why This Server?

- **Complete Coverage** — Every major Maximo module is represented, from work order lifecycle management to preventive maintenance scheduling
- **AI-Native** — Built on the [Model Context Protocol](https://modelcontextprotocol.io/) for seamless integration with Claude and other MCP-compatible AI assistants
- **Enterprise-Ready** — Rate limiting, caching, retry logic, multi-environment configs, and comprehensive error handling out of the box
- **Developer-Friendly** — Built-in API exploration tools, schema inspection, and connection testing for rapid development
- **Type-Safe** — Full TypeScript with Zod validation on every tool input

### Key Features

| Feature | Description |
|---------|-------------|
| **175 MCP Tools** | Complete coverage across 20 Maximo modules |
| **Dual Authentication** | API Key and Username/Password (Basic Auth) support |
| **OSLC Query Engine** | Full OSLC query support with a built-in query builder |
| **Bulk Operations** | Batch create, update, delete, and process operations |
| **Analytics Dashboard** | Work order summaries, asset health, PM compliance, and more |
| **Work Scheduling** | Schedule management, conflict detection, backlog analysis |
| **Job Plan Management** | Full CRUD with task, labor, material, and service planning |
| **Multi-Environment** | Seamless switching between dev, test, staging, and production |
| **Smart Caching** | In-memory cache with configurable TTL and size limits |
| **Rate Limiting** | Token bucket algorithm prevents Maximo API throttling |
| **Retry Logic** | Exponential backoff with configurable retry attempts |
| **Connection Pooling** | HTTP keep-alive for sustained throughput |
| **Structured Logging** | Winston-based logging with configurable levels |
| **Input Validation** | Zod schemas validate every tool input at runtime |

---

## Supported Modules

| Module | Tools | Key Operations |
|--------|:-----:|----------------|
| **Work Orders** | 15 | CRUD, status changes, labor/material/service assignment, tasks, work logs, close |
| **Purchase Orders** | 15 | CRUD, line items, approval workflows, receiving, receipts |
| **Preventive Maintenance** | 13 | CRUD, WO generation, job plans, scheduling, frequency, activate/deactivate |
| **Persons & Labor** | 13 | Person management, crafts, labor transactions, crews, availability, cost summaries |
| **Assets** | 12 | CRUD, meter readings, moves, hierarchy, specifications, downtime, status changes |
| **Service Requests** | 12 | CRUD, status management, WO conversion, escalation, solutions, work logs |
| **Inventory** | 11 | Items, issue/return/transfer, adjustments, reorder points, stock levels |
| **Job Plans** | 11 | CRUD, tasks, labor/material/service requirements, linked work orders |
| **Analytics** | 7 | WO summaries, asset health, inventory reports, PM compliance, dashboards |
| **Locations** | 6 | CRUD, hierarchy navigation, search |
| **Dev Tools** | 6 | Connection testing, API exploration, schema inspection, health checks, metadata |
| **Scheduling** | 6 | Work schedules, unscheduled work, backlog, conflicts, upcoming PMs |
| **Query & Search** | 4 | OSLC queries, advanced search, saved queries, query builder |
| **Bulk Operations** | 4 | Bulk create, update, delete, batch processing |
| **Classifications** | 4 | Classification trees, hierarchy, specifications, spec value updates |
| **Attachments** | 4 | Upload, download, list, delete document attachments |
| **Security** | 8 | Security groups CRUD, user-group assignments, group user/role listing |
| **Admin** | 9 | Automation scripts CRUD + execution, cron tasks, endpoints, custom actions |
| **Setup** | 9 | Domain management (ALN, table, synonym), document types |
| **Integration** | 6 | Max object structures, system properties, measurement units |
| | **175** | |

---

## Quick Start

### Prerequisites

- **Node.js** 18.0.0 or higher
- **npm** 9.0.0 or higher
- **IBM Maximo MAS 9.x** instance with REST API enabled
- **API key** or credentials with appropriate permissions

### Installation

**From npm (recommended):**

```bash
npm install -g @themaximoguys/maximo-mcp
```

**From source:**

```bash
git clone https://github.com/themaximoguys/maximo-mcp-server.git
cd maximo-mcp-server
npm install
npm run build
```

### Configuration

Create a `.env` file in the project root:

```bash
# Required
MAXIMO_HOST=https://your-maximo-instance.com
MAXIMO_API_KEY=your-api-key-here

# Optional
MAXIMO_TIMEOUT=30000        # Request timeout in ms (default: 30000)
LOG_LEVEL=info              # debug | info | warn | error (default: info)
CACHE_ENABLED=true          # Enable response caching (default: false)
```

**Multi-environment setup** using `config.json`:

```json
{
  "environments": {
    "dev": {
      "host": "https://dev-maximo.example.com",
      "apiKey": "${DEV_API_KEY}"
    },
    "staging": {
      "host": "https://staging-maximo.example.com",
      "apiKey": "${STAGING_API_KEY}"
    },
    "prod": {
      "host": "https://prod-maximo.example.com",
      "apiKey": "${PROD_API_KEY}"
    }
  },
  "defaultEnvironment": "dev"
}
```

> Environment variables referenced as `${VAR_NAME}` in `config.json` are interpolated at runtime from your shell environment or `.env` file.

### Claude Desktop Integration

Add the following to your Claude Desktop configuration file:

**macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
**Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "maximo": {
      "command": "node",
      "args": ["/path/to/maximo-mcp-server/dist/index.js"],
      "env": {
        "MAXIMO_HOST": "https://your-maximo-instance.com",
        "MAXIMO_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

**Using npx (no local install needed):**

```json
{
  "mcpServers": {
    "maximo": {
      "command": "npx",
      "args": ["-y", "@themaximoguys/maximo-mcp"],
      "env": {
        "MAXIMO_HOST": "https://your-maximo-instance.com",
        "MAXIMO_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

After saving, restart Claude Desktop. You should see the Maximo tools available in the tool picker.

### Running Standalone

```bash
# Production
npm start

# Development with hot reload
npm run dev

# With custom config
maximo-mcp-server --config config.json
```

The server communicates over **stdio** using the MCP protocol. Use Claude Desktop, Claude Code, or any MCP-compatible client to interact with it.

---

## Docker

The server ships with a production-ready Docker setup featuring multi-stage builds, non-root execution, and a read-only filesystem.

### Quick Start with Docker

**Build the image:**

```bash
docker build -t maximo-mcp-server .
```

**Run interactively (stdio mode):**

```bash
docker run -i --rm \
  -e MAXIMO_HOST=https://your-maximo-instance.com \
  -e MAXIMO_API_KEY=your-api-key \
  maximo-mcp-server
```

> The `-i` flag is required because MCP communicates over stdin/stdout.

### Docker Compose

**Production mode:**

```bash
# Build and run (production — uses compiled dist/)
docker compose -f docker-compose.yml run --rm maximo-mcp

# Build image only
docker compose build
```

**Development mode** (auto-applied via override file):

```bash
# Runs ts-node with source mounting and debug logging
docker compose run --rm maximo-mcp
```

To run production-only (skip the dev override):

```bash
docker compose -f docker-compose.yml run --rm maximo-mcp
```

**Environment variables** can be set in `.env` or passed directly:

```bash
docker compose run --rm \
  -e MAXIMO_HOST=https://dev-maximo.example.com \
  -e MAXIMO_API_KEY=your-key \
  maximo-mcp
```

### Claude Desktop with Docker

Configure Claude Desktop to use the Docker container:

```json
{
  "mcpServers": {
    "maximo": {
      "command": "docker",
      "args": [
        "run", "-i", "--rm",
        "-e", "MAXIMO_HOST=https://your-maximo-instance.com",
        "-e", "MAXIMO_API_KEY=your-api-key",
        "maximo-mcp-server"
      ]
    }
  }
}
```

### Docker Architecture

| Layer | Details |
|-------|---------|
| **Base image** | `node:22-alpine` (minimal footprint) |
| **Build strategy** | Multi-stage — compile in stage 1, ship only `dist/` in stage 2 |
| **Security** | Non-root user (`mcpuser:1001`), read-only filesystem, no-new-privileges |
| **Health check** | Verifies entry point is loadable every 30s |
| **Logs** | Mounted volume at `/app/logs` |
| **Secrets** | Never baked in — always passed as runtime env vars |

---

## Usage Examples

### Work Orders

**Create a work order:**

```json
{
  "tool": "maximo_create_workorder",
  "arguments": {
    "description": "Repair centrifugal pump bearing failure",
    "assetnum": "PUMP-001",
    "location": "BR-300",
    "worktype": "CM",
    "priority": 2,
    "siteid": "BEDFORD"
  }
}
```

**Search work orders with filters:**

```json
{
  "tool": "maximo_search_workorders",
  "arguments": {
    "where": "status=\"WAPPR\" and priority<=2",
    "select": "wonum,description,status,priority,reportdate",
    "orderBy": "+priority,-reportdate",
    "pageSize": 25
  }
}
```

**Add labor to a work order:**

```json
{
  "tool": "maximo_add_labor",
  "arguments": {
    "wonum": "WO-1001",
    "laborcode": "SMITH",
    "craft": "ELECT",
    "hours": 4.5,
    "siteid": "BEDFORD"
  }
}
```

**Change work order status:**

```json
{
  "tool": "maximo_change_workorder_status",
  "arguments": {
    "wonum": "WO-1001",
    "status": "APPR",
    "siteid": "BEDFORD"
  }
}
```

### Assets

**Record a meter reading:**

```json
{
  "tool": "maximo_record_meter",
  "arguments": {
    "assetnum": "PUMP-001",
    "metername": "RUNTIME",
    "newreading": 12500.5,
    "newreadingdate": "2026-02-20T10:00:00Z"
  }
}
```

**Get asset hierarchy:**

```json
{
  "tool": "maximo_get_asset_hierarchy",
  "arguments": {
    "assetnum": "PLANT-A",
    "siteid": "BEDFORD"
  }
}
```

**Check asset downtime:**

```json
{
  "tool": "maximo_get_asset_downtime",
  "arguments": {
    "assetnum": "CONV-200",
    "siteid": "BEDFORD"
  }
}
```

### Inventory

**Issue inventory:**

```json
{
  "tool": "maximo_issue_inventory",
  "arguments": {
    "itemnum": "BEARING-6205",
    "storeloc": "CENTRAL",
    "quantity": 2,
    "wonum": "WO-1001",
    "siteid": "BEDFORD"
  }
}
```

**Check items below reorder point:**

```json
{
  "tool": "maximo_get_items_below_reorder",
  "arguments": {
    "storeloc": "CENTRAL",
    "siteid": "BEDFORD"
  }
}
```

### Service Requests

**Create and escalate a service request:**

```json
{
  "tool": "maximo_create_sr",
  "arguments": {
    "description": "HVAC system not cooling in Building A, Floor 3",
    "location": "BLD-A-FL3",
    "reportedby": "JSMITH",
    "siteid": "BEDFORD"
  }
}
```

```json
{
  "tool": "maximo_escalate_sr",
  "arguments": {
    "ticketid": "SR-1042",
    "escalation_reason": "Affecting 50+ employees, temperature exceeding safe limits",
    "siteid": "BEDFORD"
  }
}
```

**Convert service request to work order:**

```json
{
  "tool": "maximo_convert_sr_to_wo",
  "arguments": {
    "ticketid": "SR-1042",
    "siteid": "BEDFORD"
  }
}
```

### Purchase Orders

**Create a PO with line items:**

```json
{
  "tool": "maximo_create_po",
  "arguments": {
    "description": "Quarterly bearing stock replenishment",
    "vendor": "ACME-PARTS",
    "siteid": "BEDFORD"
  }
}
```

```json
{
  "tool": "maximo_add_po_line",
  "arguments": {
    "ponum": "PO-4500",
    "itemnum": "BEARING-6205",
    "quantity": 50,
    "unitcost": 24.99,
    "siteid": "BEDFORD"
  }
}
```

**Submit for approval and receive:**

```json
{
  "tool": "maximo_submit_po_approval",
  "arguments": { "ponum": "PO-4500", "siteid": "BEDFORD" }
}
```

```json
{
  "tool": "maximo_receive_po_line",
  "arguments": {
    "ponum": "PO-4500",
    "polinenum": 1,
    "quantity": 50,
    "siteid": "BEDFORD"
  }
}
```

### Preventive Maintenance

**Generate work orders from a PM:**

```json
{
  "tool": "maximo_generate_pm_wo",
  "arguments": {
    "pmnum": "PM-PUMP-QUARTERLY",
    "siteid": "BEDFORD"
  }
}
```

**Update PM frequency:**

```json
{
  "tool": "maximo_update_pm_frequency",
  "arguments": {
    "pmnum": "PM-PUMP-QUARTERLY",
    "frequency": 90,
    "frequnit": "DAYS",
    "siteid": "BEDFORD"
  }
}
```

### Analytics & Reporting

**Get a maintenance dashboard:**

```json
{
  "tool": "maximo_dashboard",
  "arguments": {
    "siteid": "BEDFORD"
  }
}
```

**Check PM compliance:**

```json
{
  "tool": "maximo_pm_compliance",
  "arguments": {
    "siteid": "BEDFORD"
  }
}
```

**Find overdue work orders:**

```json
{
  "tool": "maximo_overdue_workorders",
  "arguments": {
    "siteid": "BEDFORD"
  }
}
```

**Identify top downtime assets:**

```json
{
  "tool": "maximo_top_downtime_assets",
  "arguments": {
    "siteid": "BEDFORD",
    "limit": 10
  }
}
```

### OSLC Queries

**Ad-hoc query with the OSLC engine:**

```json
{
  "tool": "maximo_query",
  "arguments": {
    "objectStructure": "mxwodetail",
    "select": "wonum,description,status,priority,assetnum,location",
    "where": "status in [\"WAPPR\",\"APPR\"] and worktype=\"CM\"",
    "orderBy": "+priority,-reportdate",
    "pageSize": 50
  }
}
```

**Build a complex query interactively:**

```json
{
  "tool": "maximo_build_query",
  "arguments": {
    "objectStructure": "mxasset",
    "conditions": [
      { "field": "status", "operator": "=", "value": "OPERATING" },
      { "field": "assettype", "operator": "=", "value": "PRODUCTION" }
    ],
    "select": "assetnum,description,location,status",
    "orderBy": "+assetnum"
  }
}
```

### Bulk Operations

**Create multiple work orders in one call:**

```json
{
  "tool": "maximo_bulk_create",
  "arguments": {
    "objectStructure": "mxwodetail",
    "records": [
      { "description": "Monthly inspection - Line A", "worktype": "PM", "siteid": "BEDFORD" },
      { "description": "Monthly inspection - Line B", "worktype": "PM", "siteid": "BEDFORD" },
      { "description": "Monthly inspection - Line C", "worktype": "PM", "siteid": "BEDFORD" }
    ]
  }
}
```

---

## Architecture

### High-Level Design

```
┌──────────────────────────────────────────────────────────────────┐
│                    MCP Client (Claude / AI Assistant)             │
└───────────────────────────┬──────────────────────────────────────┘
                            │ MCP Protocol (stdio)
┌───────────────────────────▼──────────────────────────────────────┐
│                         MCP Server                                │
│                                                                   │
│  ┌──────────────┐  ┌───────────────┐  ┌────────────────────────┐ │
│  │ Auth Manager  │  │  Tool Router  │  │  Response Formatter    │ │
│  │  (API Key /   │  │  (175 tools)  │  │  (Normalize + Format)  │ │
│  │  Basic Auth)  │  │               │  │                        │ │
│  └──────────────┘  └───────────────┘  └────────────────────────┘ │
│                                                                   │
│  ┌──────────────┐  ┌───────────────┐  ┌────────────────────────┐ │
│  │ Rate Limiter  │  │    Cache      │  │   Error Handler        │ │
│  │ (Token Bucket)│  │  (TTL + Size) │  │  (Context-Aware)       │ │
│  └──────────────┘  └───────────────┘  └────────────────────────┘ │
└───────────────────────────┬──────────────────────────────────────┘
                            │
┌───────────────────────────▼──────────────────────────────────────┐
│                       Module Layer (20 modules)                   │
│                                                                   │
│  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐        │
│  │Work Ord│ │ Assets │ │  Inv   │ │  S.R.  │ │  P.O.  │        │
│  └────────┘ └────────┘ └────────┘ └────────┘ └────────┘        │
│  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐        │
│  │  P.M.  │ │ Plans  │ │Persons │ │  Locs  │ │ Class  │        │
│  └────────┘ └────────┘ └────────┘ └────────┘ └────────┘        │
│  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐        │
│  │ Attach │ │Analytic│ │Schedule│ │ Query  │ │  Bulk  │        │
│  └────────┘ └────────┘ └────────┘ └────────┘ └────────┘        │
│  ┌────────┐                                                      │
│  │DevTools│                                                      │
│  └────────┘                                                      │
│  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐                    │
│  │Securty │ │ Admin  │ │ Setup  │ │  Integ │                    │
│  └────────┘ └────────┘ └────────┘ └────────┘                    │
└───────────────────────────┬──────────────────────────────────────┘
                            │ HTTPS (REST API)
┌───────────────────────────▼──────────────────────────────────────┐
│               IBM Maximo Application Suite 9.x                    │
│                      (OSLC REST API)                              │
└──────────────────────────────────────────────────────────────────┘
```

### Module Structure

Every module follows a consistent five-file pattern:

```
src/modules/<module-name>/
├── operations.ts    # Business logic — makes HTTP calls via MaximoClient
├── tools.ts         # MCP tool definitions — name, description, schema, handler
├── types.ts         # TypeScript interfaces for requests and responses
├── validators.ts    # Zod schemas for runtime input validation
└── index.ts         # Public exports
```

**Design principle:** `operations.ts` owns the business logic; `tools.ts` is a thin MCP adapter. This separation allows operations to be reused by multiple tools, direct API calls, or future interfaces without duplication.

### Project Structure

```
maximo-mcp-server/
├── src/
│   ├── index.ts                    # Server entry point & tool registration
│   ├── auth/                       # Authentication (API key + Basic Auth)
│   ├── config/                     # ConfigManager — env, JSON, interpolation
│   ├── core/                       # Infrastructure layer
│   │   ├── maximo-client.ts        #   HTTP client (retry, cache, rate limit)
│   │   ├── error-handler.ts        #   Error transformation & context
│   │   ├── response-formatter.ts   #   Response normalization
│   │   ├── rate-limiter.ts         #   Token bucket rate limiter
│   │   ├── cache-manager.ts        #   In-memory TTL cache
│   │   └── types.ts                #   Shared core type definitions
│   ├── modules/                    # 20 Maximo functional modules
│   │   ├── work-orders/            #   15 tools
│   │   ├── assets/                 #   12 tools
│   │   ├── inventory/              #   11 tools
│   │   ├── purchase-orders/        #   15 tools
│   │   ├── service-requests/       #   12 tools
│   │   ├── preventive-maintenance/ #   13 tools
│   │   ├── persons-labor/          #   13 tools
│   │   ├── plans/                  #   11 tools (Job Plans)
│   │   ├── analytics/              #    7 tools
│   │   ├── locations/              #    6 tools
│   │   ├── scheduler/              #    6 tools
│   │   ├── dev-tools/              #    6 tools
│   │   ├── query-search/           #    4 tools
│   │   ├── bulk-operations/        #    4 tools
│   │   ├── classifications/        #    4 tools
│   │   ├── attachments/            #    4 tools
│   │   ├── security/               #    8 tools (MAS 9 Security Groups)
│   │   ├── admin/                  #    9 tools (Automation Scripts, Cron, Endpoints)
│   │   ├── setup/                  #    9 tools (Domains, Doc Types)
│   │   └── integration/            #    6 tools (Object Structures, System Props)
│   ├── utils/                      # Utility functions
│   ├── resources/                  # MCP resource definitions
│   └── tools/                      # Tool registry helpers
├── tests/
│   ├── unit/                       # Unit tests (per module)
│   ├── integration/                # Integration tests (mocked API)
│   └── fixtures/                   # Test data & mock responses
├── docs/
│   ├── planning/                   # Architecture, roadmap, tool catalog
│   └── api/                        # API guides, module documentation
├── dist/                           # Compiled output (git-ignored)
├── logs/                           # Runtime logs (git-ignored)
├── package.json
├── tsconfig.json
├── jest.config.js
└── .env                            # Environment config (git-ignored)
```

### Core Infrastructure

| Component | Purpose | Implementation |
|-----------|---------|----------------|
| **MaximoClient** | HTTP communication with Maximo REST API | Axios with interceptors, keep-alive pooling |
| **AuthManager** | Credential management and session handling | API Key headers or Basic Auth with session tokens |
| **RateLimiter** | Prevent exceeding Maximo API limits | Token bucket algorithm with configurable windows |
| **CacheManager** | Reduce redundant API calls | In-memory cache via `node-cache` with TTL and size limits |
| **ErrorHandler** | Transform API errors into actionable messages | HTTP status mapping, context preservation, custom error classes |
| **ResponseFormatter** | Normalize API responses | Consistent format, pagination metadata, OSLC parsing |
| **ConfigManager** | Load and merge configuration sources | `.env` files, `config.json`, environment variable interpolation |

---

## Configuration Reference

### Environment Variables

| Variable | Required | Default | Description |
|----------|:--------:|---------|-------------|
| `MAXIMO_HOST` | Yes | — | Base URL of your Maximo instance |
| `MAXIMO_API_KEY` | Yes* | — | API key for authentication |
| `MAXIMO_USERNAME` | Yes* | — | Username (if using Basic Auth) |
| `MAXIMO_PASSWORD` | Yes* | — | Password (if using Basic Auth) |
| `MAXIMO_TIMEOUT` | No | `30000` | Request timeout in milliseconds |
| `LOG_LEVEL` | No | `info` | Logging level: `debug`, `info`, `warn`, `error` |
| `CACHE_ENABLED` | No | `false` | Enable in-memory response caching |
| `CACHE_TTL` | No | `300` | Cache time-to-live in seconds |
| `CACHE_MAX_SIZE` | No | `100` | Maximum cached entries |

> \* Provide either `MAXIMO_API_KEY` **or** `MAXIMO_USERNAME` + `MAXIMO_PASSWORD`.

### Authentication Modes

**API Key (recommended for automation):**

```
apikey: your-api-key-here
Content-Type: application/json
```

**Basic Auth (for development):**

```
Authorization: Basic base64(username:password)
Content-Type: application/json
```

---

## Development

### Building from Source

```bash
# Install dependencies
npm install

# Build TypeScript to dist/
npm run build

# Build with esbuild bundle
npm run build:bundle

# Development mode with hot reload
npm run dev

# Clean build artifacts
npm run clean
```

### Testing

```bash
# Run all tests
npm test

# Watch mode for development
npm run test:watch

# Coverage report (70% threshold enforced)
npm run test:coverage

# Single test file
npm test -- path/to/test.spec.ts

# Pattern matching
npm test -- --testNamePattern="WorkOrder"
```

**Coverage thresholds** (enforced in `jest.config.js`):

| Metric | Minimum |
|--------|:-------:|
| Branches | 70% |
| Functions | 70% |
| Lines | 70% |
| Statements | 70% |

### Code Quality

```bash
# Lint with ESLint
npm run lint

# Auto-fix lint issues
npm run lint:fix

# Format with Prettier
npm run format

# Type check without emitting
npm run type-check
```

---

## Performance

| Feature | Implementation | Benefit |
|---------|----------------|---------|
| **Response Caching** | In-memory with TTL | Eliminates redundant API calls |
| **Connection Pooling** | Axios keep-alive | Reuses TCP connections |
| **Rate Limiting** | Token bucket algorithm | Prevents Maximo API throttling |
| **Retry with Backoff** | Exponential (3 retries default) | Handles transient failures |
| **Bulk Operations** | Batch API calls | Reduces round trips for multi-record operations |
| **Lazy Module Loading** | On-demand initialization | Faster server startup |

---

## Troubleshooting

### Connection Issues

**Problem:** `ECONNREFUSED` or `ETIMEDOUT` when connecting to Maximo.

```bash
# Verify connectivity
curl -I https://your-maximo-instance.com/maximo/api/os

# Check your .env
echo $MAXIMO_HOST
```

**Solutions:**
- Verify `MAXIMO_HOST` includes the full base URL with protocol (`https://`)
- Check network/VPN connectivity to the Maximo server
- Increase `MAXIMO_TIMEOUT` if the instance is slow to respond

### Authentication Errors

**Problem:** `401 Unauthorized` responses.

**Solutions:**
- Verify your API key is valid and not expired
- Ensure the API key has permissions for the Maximo object structures you're accessing
- For Basic Auth, confirm the account is not locked or expired
- Check that the `apikey` header name matches your Maximo configuration

### OSLC Query Errors

**Problem:** `400 Bad Request` on query operations.

**Solutions:**
- Validate field names against your Maximo schema using `maximo_inspect_schema`
- Enclose string values in double quotes: `status="WAPPR"` not `status=WAPPR`
- Use `maximo_build_query` to construct queries interactively
- Check OSLC `where` clause syntax — Maximo uses its own dialect

### Rate Limiting

**Problem:** `429 Too Many Requests` or throttled responses.

**Solutions:**
- The built-in rate limiter should handle this automatically
- If you're still hitting limits, reduce `pageSize` in queries
- Avoid concurrent bulk operations against the same Maximo instance
- Check your Maximo admin for rate limit configuration

### Debug Mode

Enable verbose logging to diagnose issues:

```bash
LOG_LEVEL=debug npm run dev
```

Logs are written to the `logs/` directory with structured JSON output. Sensitive data (API keys, passwords) is automatically sanitized.

---

## FAQ

<details>
<summary><strong>Which Maximo versions are supported?</strong></summary>

This server is built for **IBM Maximo Application Suite (MAS) 9.x** and its OSLC-based REST API. It may work with Maximo 7.6.1.x instances that have the REST API enabled, but this is not officially tested.
</details>

<details>
<summary><strong>Can I use this with Claude Desktop?</strong></summary>

Yes. See the [Claude Desktop Integration](#claude-desktop-integration) section for configuration instructions. The server communicates over stdio using the MCP protocol.
</details>

<details>
<summary><strong>Does this modify data in Maximo?</strong></summary>

Yes. Tools like `maximo_create_workorder`, `maximo_update_asset`, and `maximo_delete_po` perform write operations. Always test against a development or sandbox environment first.
</details>

<details>
<summary><strong>How do I add a custom Maximo module?</strong></summary>

1. Create a new directory under `src/modules/`
2. Follow the five-file pattern: `operations.ts`, `tools.ts`, `types.ts`, `validators.ts`, `index.ts`
3. Register the module in `src/index.ts`
4. Add tests under `tests/unit/modules/` and `tests/integration/modules/`

See the [Module Structure](#module-structure) section for details.
</details>

<details>
<summary><strong>What's the difference between <code>maximo_query</code> and <code>maximo_advanced_search</code>?</strong></summary>

`maximo_query` executes raw OSLC queries with full control over `where`, `select`, `orderBy`, and pagination. `maximo_advanced_search` provides a higher-level interface with pre-built search patterns. Use `maximo_build_query` to construct complex OSLC queries interactively.
</details>

<details>
<summary><strong>Can I run multiple instances for different environments?</strong></summary>

Yes. Use `config.json` with multiple environment definitions and the `defaultEnvironment` setting. You can also run separate server processes with different `.env` files.
</details>

---

## Security

### Best Practices

- **Never commit credentials** — Use `.env` files (git-ignored) or environment variables
- **Use API keys over passwords** — API keys can be scoped and rotated independently
- **HTTPS only** — All connections to Maximo should use TLS
- **Principle of least privilege** — Use API keys with minimal required permissions
- **Rotate regularly** — Implement key rotation policies
- **Audit logging** — Enable `LOG_LEVEL=info` or higher in production
- **Input validation** — All tool inputs are validated with Zod schemas before reaching Maximo

### Reporting Vulnerabilities

If you discover a security vulnerability, please report it responsibly:

1. **Do not** open a public GitHub issue
2. Email **info@themaximoguys.com** with details
3. Include steps to reproduce, impact assessment, and suggested fix if possible
4. We will acknowledge receipt within 48 hours and provide a timeline for resolution

---

## Contributing

Contributions are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines, and open an issue or pull request on GitHub.

If you'd like to report a bug or request a feature, please contact **info@themaximoguys.com**.

---

## Roadmap

### v1.0

- 143 tools across 16 modules
- Dual authentication (API Key + Basic Auth)
- OSLC query engine with query builder
- Analytics and scheduling modules
- Bulk operations and batch processing
- Comprehensive error handling, caching, and rate limiting

### v2.0 — Current

- **175 tools across 20 modules**
- 4 new MAS 9 modules: Security, Admin, Setup, Integration
- Security group management with user-group assignments
- Automation script CRUD, execution, and deployment
- Domain management (ALN, table, synonym) and document types
- System property management and object structure introspection
- x-method-override PATCH support for MAS 9 OSLC endpoints

### v2.1 — Planned

- Webhook support for Maximo event notifications
- Custom saved query management
- Enhanced analytics with trend analysis
- Tool usage metrics and telemetry

### v3.0 — Future

- GraphQL adapter layer
- WebSocket support for real-time Maximo events
- AI-powered query optimization
- Predictive maintenance insights
- Natural language to OSLC query translation

---

## License

Released under the [MIT License](LICENSE). Free to use, modify and distribute.

Copyright (c) 2026 **TheMaximoGuys LLC**.

---

## Acknowledgments

- **IBM** — for the Maximo Application Suite and its comprehensive REST API
- **Anthropic** — for the [Model Context Protocol](https://modelcontextprotocol.io/) specification
- **MCP Community** — for the SDK, tooling, and ecosystem

---

<div align="center">

**[Back to Top](#ibm-maximo-mas-9x-mcp-server)**

Copyright (c) 2026 TheMaximoGuys LLC · [MIT License](LICENSE)

</div>
