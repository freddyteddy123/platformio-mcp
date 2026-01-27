# Copilot Instructions for AI Coding Agents

## Project Overview

- **PlatformIO MCP Server** is a board-agnostic Model Context Protocol (MCP) server for embedded development, enabling AI agents to interact with PlatformIO's ecosystem (1000+ boards, 30+ platforms).
- The server exposes 11 MCP tools for board discovery, project management, build/upload, device monitoring, and library management.
- All board/platform support is dynamic—no hardcoded board configs. Specify board IDs (e.g., `esp32dev`, `uno`).

## Key Architecture & Patterns

- **Entry Point:** `src/index.ts` (registers all MCP tools, stdio transport, error handling)
- **Tool Logic:** Each tool is implemented in `src/tools/` (e.g., `boards.ts`, `projects.ts`, `build.ts`, `upload.ts`, `monitor.ts`, `libraries.ts`).
- **PlatformIO CLI Integration:** All operations wrap PlatformIO CLI commands via `src/platformio.ts` (uses child_process, parses JSON output, handles timeouts/errors).
- **Type Safety:** All tool inputs/outputs are validated with Zod schemas in `src/types.ts`.
- **Error Handling:** Centralized in `src/utils/errors.ts`—all errors include troubleshooting hints for users/agents.
- **Input Validation:** Path and board ID validation in `src/utils/validation.ts` (prevents path traversal/injection).

## Developer Workflows

- **Install dependencies:** `npm install`
- **Build:** `npm run build` (TypeScript → build/)
- **Dev mode (auto-reload):** `npm run dev`
- **Run tests:** `npm test` (unit tests via Vitest)
- **Lint/Format:** `npm run lint`, `npm run format`
- **PlatformIO CLI required:** All tool calls require `pio` in PATH (install via `pip install platformio`).

## Tooling & Usage Examples

- **Board Discovery:** `list_boards`, `get_board_info` (filters by platform/framework/MCU)
- **Project Lifecycle:** `init_project`, `build_project`, `clean_project`, `upload_firmware`, `start_monitor`
- **Library Management:** `search_libraries`, `install_library`, `list_installed_libraries`
- **Device Discovery:** `list_devices` (serial ports)
- **Example:** To create, build, and upload for ESP32:
  1. `listBoards('esp32')`
  2. `initProject({ board: 'esp32dev', framework: 'arduino', projectDir: '/path/to/esp32-blink' })`
  3. `buildProject('/path/to/esp32-blink')`
  4. `uploadFirmware('/path/to/esp32-blink')`

## Project Structure

- `src/index.ts` — Main server, tool registration
- `src/platformio.ts` — CLI wrapper, command execution
- `src/types.ts` — TypeScript types, Zod schemas
- `src/tools/` — Tool implementations (one file per tool group)
- `src/utils/` — Validation and error utilities
- `tests/` — Unit tests (Vitest)

## Project-Specific Conventions

- **All tool input/output is strictly validated.**
- **Board IDs are case-sensitive.**
- **Ports are auto-detected when possible.**
- **Timeouts:** 30s (quick ops), 10min (build), 5min (upload).
- **All errors should be surfaced to users/agents.**

## Integration Points

- **Cline AI agent:** Add this server to Cline MCP settings for natural language workflows.
- **PlatformIO CLI:** All board/project/library/device operations are delegated to PlatformIO CLI.

## Troubleshooting

- If PlatformIO CLI is missing, all operations will fail with a clear error.
- For board/library/project errors, check spelling/case and use the relevant list/search tool for discovery.

## References

- See `README.md` and `llms-install.md` for full usage, installation, and troubleshooting details.
- Example tool schemas and usage: `src/types.ts`, `src/index.ts`

---

For questions or unclear patterns, review the implementation plan (`implementation_plan.md`) or open an issue.
