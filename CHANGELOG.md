# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2026-01-10

### Added
- **Multiple Authentication Methods**: Support for OAuth, HTTP Basic Auth, and no authentication
- `AUTH_TYPE` configuration variable to select authentication method (`oauth`, `basic`, `none`)
- `CB_PROTOCOL` configuration variable to support both HTTP and HTTPS
- Automatic `.env` file loading from MCP's directory using `Path(__file__).parent`
- Comprehensive authentication examples in README for each method
- Debug logging on startup showing AUTH_TYPE, CB_HOST, and PROTOCOL

### Changed
- **BREAKING**: Authentication is now configurable via `AUTH_TYPE` instead of being OAuth-only
- **BREAKING**: Context Broker protocol is now configurable via `CB_PROTOCOL` (default: `https`)
- Updated `make_request()` to handle multiple authentication methods
- Updated `CB_version()` and `fiware_request()` to use `CB_PROTOCOL`
- Improved `.env.example` with detailed examples for each authentication method
- Updated README with comprehensive authentication configuration guide
- Changed header from `fiware-service` to `Fiware-Service` (proper casing)

### Fixed
- `.env` file loading now works correctly when MCP is executed from any directory
- Windows `USERNAME` environment variable conflict (already using `FIWARE_USERNAME`)

### Migration Guide

If you're upgrading from v1.x:

1. **Add to your `.env` file:**
   ```env
   AUTH_TYPE=oauth  # Keep OAuth as default for backward compatibility
   CB_PROTOCOL=https  # Explicitly set protocol
   ```

2. **For OAuth deployments** (Telefónica, etc.):
   - No changes needed, OAuth is still the default
   - Just add `AUTH_TYPE=oauth` and `CB_PROTOCOL=https` to your `.env`

3. **For Basic Auth deployments** (Nginx, etc.):
   ```env
   AUTH_TYPE=basic
   CB_PROTOCOL=http
   FIWARE_USERNAME=admin
   FIWARE_PASSWORD=your_password
   # AUTH_HOST and AUTH_PORT not needed
   ```

4. **For local development** (no auth):
   ```env
   AUTH_TYPE=none
   CB_PROTOCOL=http
   CB_HOST=localhost
   ```

## [1.0.0] - 2025-12-XX

### Added
- Initial release with OAuth authentication
- Smart Data Models integration
- NGSI-v2 API support
- 4 MCP tools, 1 resource, 3 prompts
- OpenStack Keystone authentication with automatic token refresh

[2.0.0]: https://github.com/miguel-escribano/FIWARE-MCP-Server/compare/v1.0.0...v2.0.0
[1.0.0]: https://github.com/miguel-escribano/FIWARE-MCP-Server/releases/tag/v1.0.0
