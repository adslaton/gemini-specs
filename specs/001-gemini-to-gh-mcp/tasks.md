# Tasks: Integrate GitHub Remote MCP

**Input**: Design documents from `/specs/001-gemini-to-gh-mcp/`
**Prerequisites**: plan.md (required), research.md, data-model.md, contracts/

## Phase 3.1: Setup
- [ ] T001 Create project structure in `src/` and `tests/` per implementation plan
- [ ] T002 Initialize Python project with `requests` and `pytest` dependencies
- [ ] T003 [P] Configure linting and formatting tools (`black`, `ruff`)

## Phase 3.2: Tests First (TDD) ⚠️ MUST COMPLETE BEFORE 3.3
**CRITICAL: These tests MUST be written and MUST FAIL before ANY implementation**
- [ ] T004 [P] Integration test `gemini mcp config` in `tests/integration/test_mcp_config.py`
- [ ] T005 [P] Integration test repository access via MCP in `tests/integration/test_mcp_access.py`

## Phase 3.3: Core Implementation (ONLY after tests are failing)
- [ ] T006 Implement `GitHubMcpServerConfig` model in `src/models/mcp_config.py`
- [ ] T007 Implement `McpService` in `src/services/mcp_service.py`
- [ ] T008 Implement `gemini mcp config` command in `src/cli/mcp_commands.py`
- [ ] T009 Implement MCP configuration usage in existing commands

## Phase 3.4: Integration
- [ ] T010 Integrate `McpService` with secure file system storage

## Phase 3.5: Polish
- [ ] T011 [P] Unit tests for `McpService` in `tests/unit/test_mcp_service.py`
- [ ] T012 [P] Update documentation for the `gemini mcp` command

## Dependencies
- Tests (T004-T005) before implementation (T006-T009)
- T006 blocks T007
- T007 blocks T008, T010
- Implementation before polish (T011-T012)

## Parallel Example
```
# Launch T004-T005 together:
Task: "Integration test `gemini mcp config` in `tests/integration/test_mcp_config.py`"
Task: "Integration test repository access via MCP in `tests/integration/test_mcp_access.py`"
```
