# Runtime Configuration

## Environment Variables

### Required Variables
| Variable | Description | Default | Example |
|----------|-------------|---------|---------|
| `SERENA_PROJECT_ROOT` | Active project directory | Current working directory | `/path/to/project` |

### Optional Variables  
| Variable | Description | Default | Example |
|----------|-------------|---------|---------|
| `SERENA_CONFIG_DIR` | Configuration directory | `~/.serena` | `/custom/config/path` |
| `SERENA_LOG_LEVEL` | Logging verbosity | `INFO` | `DEBUG`, `WARNING`, `ERROR` |
| `SERENA_DASHBOARD_PORT` | Web dashboard port | `5000` | `8080` |
| `SERENA_DASHBOARD_HOST` | Dashboard bind address | `127.0.0.1` | `0.0.0.0` |
| `ANTHROPIC_API_KEY` | Claude API key for AI features | None | `sk-ant-api03-...` |
| `OPENAI_API_KEY` | OpenAI API key (optional) | None | `sk-...` |
| `PYDEVD_DISABLE_FILE_VALIDATION` | Disable PyCharm debugger validation | `1` | `0` or `1` |

### Language Server Configuration
| Variable | Description | Default |
|----------|-------------|---------|
| `SERENA_PYTHON_LSP` | Python language server path | Auto-detected |
| `SERENA_NODE_PATH` | Node.js installation path | Auto-detected |
| `SERENA_JAVA_HOME` | Java installation path | Auto-detected |
| `SERENA_GO_ROOT` | Go installation path | Auto-detected |

## Application Configuration

### Core Settings (`~/.serena/serena_config.yml`)
```yaml
# Default configuration template
log_level: INFO
dashboard:
  enabled: true
  port: 5000
  host: "127.0.0.1"
  
language_servers:
  timeout_seconds: 30
  max_retries: 3
  auto_restart: true
  
memory:
  max_memories: 100
  auto_cleanup: true
  
tools:
  default_context: "agent"
  parallel_execution: true
```

### Project Configuration (`.serena/project.yml`)
```yaml
# Project-specific settings
name: "Project Name"
description: "Project description"
language: "python"  # Primary language
root_path: "/path/to/project"

ignored_patterns:
  - "*.pyc"
  - "__pycache__/"
  - ".git/"
  - "node_modules/"
  - ".vscode/"
  
language_servers:
  python:
    enabled: true
    server_type: "pyright"
  typescript:
    enabled: false
    
memory:
  enabled: true
  categories:
    - "architecture"
    - "patterns"
    - "decisions"
```

## Feature Flags

### Available Flags
```yaml
features:
  enhanced_memory: true          # Advanced memory features
  parallel_language_servers: true # Multiple LSP instances
  web_dashboard: true            # Enable web interface
  analytics: false               # Usage analytics
  experimental_tools: false     # Beta features
  auto_project_detection: true  # Automatic project setup
  symbol_caching: true          # Cache LSP symbol results
  smart_completions: true       # AI-enhanced completions
```

## Performance Tuning

### Language Server Settings
```yaml
language_servers:
  # Memory limits
  max_memory_mb: 512
  
  # Connection settings  
  connection_timeout: 10
  request_timeout: 30
  
  # Caching
  symbol_cache_size: 1000
  document_cache_ttl: 300
  
  # Parallel processing
  max_concurrent_requests: 5
  worker_threads: 2
```

### Memory Management
```yaml
memory:
  # Storage limits
  max_memory_files: 100
  max_file_size_mb: 10
  
  # Cleanup settings
  auto_cleanup_days: 30
  vacuum_interval_hours: 24
  
  # Performance
  index_enabled: true
  compression: true
```

## Security Configuration

### API Security
```yaml
security:
  # API key validation
  require_api_key: false
  api_key_header: "X-API-Key"
  
  # Dashboard security
  dashboard_auth: false
  csrf_protection: true
  
  # File access controls
  restrict_file_access: true
  allowed_extensions:
    - ".py"
    - ".js" 
    - ".ts"
    - ".java"
    - ".go"
    - ".rs"
    - ".md"
```

### File System Security
```yaml
file_system:
  # Path validation
  restrict_to_project: true
  follow_symlinks: false
  
  # Directory traversal protection
  normalize_paths: true
  validate_paths: true
  
  # File permissions
  respect_gitignore: true
  honor_file_permissions: true
```

## Configuration Loading Order

1. **Environment Variables** - Highest priority
2. **Command Line Arguments** - Override config files
3. **Project Config** (`.serena/project.yml`) - Project-specific
4. **User Config** (`~/.serena/serena_config.yml`) - User defaults
5. **System Defaults** - Built-in fallbacks

## Common Configuration Patterns

### Development Setup
```yaml
# Development-friendly settings
log_level: DEBUG
dashboard:
  enabled: true
  auto_open_browser: true
features:
  experimental_tools: true
  enhanced_memory: true
language_servers:
  auto_restart: true
  verbose_logging: true
```

### Production Deployment
```yaml
# Production-optimized settings
log_level: WARNING
dashboard:
  enabled: false
security:
  restrict_file_access: true
  validate_paths: true
performance:
  max_memory_mb: 1024
  cache_enabled: true
```

### Multi-Language Project
```yaml
# Support for multiple languages
language_servers:
  python:
    enabled: true
    server_type: "pyright"
  typescript:
    enabled: true
    server_type: "typescript-language-server"
  java:
    enabled: true
    server_type: "eclipse-jdtls"
  go:
    enabled: true
    server_type: "gopls"
```

## Troubleshooting Configuration

### Common Issues
1. **Language Server Not Starting**
   - Check `SERENA_LOG_LEVEL=DEBUG` for detailed logs
   - Verify language server installation in `~/.serena/language_servers/`
   - Check project root permissions

2. **Memory Issues**
   - Adjust `max_memory_mb` in configuration
   - Enable `auto_cleanup` for memory management
   - Monitor with `serena dashboard`

3. **Performance Problems**
   - Enable `symbol_caching` for faster responses
   - Increase `max_concurrent_requests` for parallel processing
   - Check `ignored_patterns` to exclude unnecessary files

### Configuration Validation
```bash
# Validate configuration
uv run serena config validate

# Show current configuration
uv run serena config show

# Test language server setup
uv run serena test-lsp --language python
```

## Keywords <!-- #keywords -->
configuration, environment variables, settings, feature flags, performance tuning, security config, language servers, project config, user config, deployment settings