# AI Agent Instructions for Homer

CRITICAL: When you encounter a file reference (e.g., @README.md, @PLUGIN_RELEASE.md), use your Read tool to load it on a need-to-know basis. They're relevant to the SPECIFIC task at hand.

## Project Overview

Homer is a Slack bot designed to help teams share and track GitLab merge requests directly within Slack channels. The bot facilitates code review workflows by creating interactive Slack messages that automatically update as merge requests progress through various states (opened, approved, merged, etc.).

**Core Functionality:**

- Share GitLab merge requests in Slack channels using `/homer review` command or GitLab labels
- Track merge request status updates via GitLab webhooks
- Manage project-channel associations
- Generate changelogs between release tags
- Support custom release management through a plugin system

## Technology Stack

**Runtime & Language:**

- Language: Node.js v20 (see `.nvmrc`)
- TypeScript: 5.6.3
- Target: ES2020

**Core Framework:**

- Framework: Express 4.21.1 (HTTP server)
- ORM: Sequelize 6.28.0
- Database: PostgreSQL (pg 8.9.0)

**Key Dependencies:**

- @slack/web-api 6.8.1 - Slack API integration
- slackify-markdown 4.3.1 - Markdown to Slack formatting
- dd-trace 3.13.2 - DataDog APM tracing
- pino 8.10.0 - Structured logging
- ajv 8.17.1 - JSON schema validation
- dayjs 1.11.13 - Date manipulation

**Build & Development:**

- Build Tool: TypeScript compiler with path aliases (@/_ and @root/_)
- Testing: Jest 29.7.0 with ts-jest
- Linting: ESLint 8.33.0 + Prettier 2.8.4
- Git Hooks: Husky 8.0.3 + exec-staged 1.0.2

See `package.json` for complete dependency information and available npm scripts.

## Resources

**Essential Documentation:**

- `README.md` - Complete installation guide, usage instructions, configuration, and architecture overview
- `PLUGIN_RELEASE.md` - Custom release manager plugin system documentation
- `CONTRIBUTING.md` - Contribution guidelines (references ManoMano's ALaMano repository)
- `manifest.json` - Slack app configuration and required permissions
- `examples/deploy/` - Deployment examples using the Homer Docker image

**Key Source Directories:**

- `src/` - TypeScript source code
  - `src/index.ts` - Application entry point
  - `src/start.ts` - Express server initialization
  - `src/router.ts` - API route definitions
  - `src/config.ts` - Centralized environment variable configuration
  - `src/core/` - Core services (Slack client, GitLab client, database, logger, middlewares)
  - `src/changelog/` - Changelog generation logic
  - `src/project/` - Project-channel management commands
  - `src/release/` - Release management system
  - `src/review/` - Merge request review functionality

**Configuration:**

- `config/homer/projects.json` - Release-enabled projects configuration
- `.nvmrc` - Node.js version specification
- `tsconfig.json` - TypeScript compiler configuration
- `.env` - Environment variables (not in repo, see README.md for required variables)

**Documentation & Assets:**

- `docs/` - Architecture diagrams and documentation assets
- `emojis/` - Custom Slack emojis used by Homer

**Plugins:**

- `plugins/release/` - Custom release manager plugins directory

## Rules

**ManoMano Organizational Standards:**

- Follow contribution guidelines from [ManoMano/ALaMano](https://github.com/ManoManoTech/ALaMano/blob/master/CONTRIBUTING.md)
- Maintain existing code style enforced by ESLint + Prettier configuration
- Use conventional commits pattern (see recent git history for examples)

**Code Quality:**

- TypeScript strict mode is enabled
- All code must pass pre-commit hooks (lint, format, type checking)
- Tests run with `yarn test` (Jest with --runInBand --forceExit)
- Use path aliases: @/_ for src/, @root/_ for project root

**Database:**

- Use Sequelize ORM for all database interactions
- Models are defined in `src/core/services/data.ts`
- PostgreSQL is the target database

## Behaviour

**Documentation Maintenance:**

- Keep `README.md` installation steps and commands up to date when adding/modifying features
- Update `PLUGIN_RELEASE.md` if release manager plugin system changes
- Keep `manifest.json` synchronized with Slack app requirements when adding new permissions or features
- Update environment variable documentation in `README.md` when adding new config options to `src/config.ts`
- Maintain accuracy of architecture diagrams in `docs/assets/` when system design changes

**When Making Changes:**

1. Always reference existing documentation before implementing features
2. Check `config/homer/projects.json` structure before modifying release functionality
3. Verify environment variables in `src/config.ts` match `README.md` documentation
4. Update relevant sections of `README.md` if adding new commands or features
5. If modifying the plugin system, ensure `PLUGIN_RELEASE.md` stays synchronized
6. Run tests after making code changes to ensure nothing breaks

## Utils

No MCP servers are configured for this project.
