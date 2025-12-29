# Release Notes

## v1.0.0 - 2024-12-29

Initial release of `tlog` - A reusable Go logging package built on Zap.

### Core Features

**Structured Logging**
- High-performance structured logging powered by Zap
- Support for multiple log levels: debug, info, warn, error, fatal, panic
- Global and sugared logger access via `L()` and `S()`

**Multi-Output Support**
- Console output with colored formatting for development
- JSON output for production environments
- File output with rotation via lumberjack
- Configurable file rotation: size limits, backup count, age limits, compression

**Context-Aware Logging**
- Built-in context keys: `request_id`, `user_id`, `trace_id`
- Context propagation helpers: `WithRequestID`, `WithUserID`, `WithTraceID`
- Context-aware log functions: `InfoCtx`, `ErrorCtx`, `DebugCtx`, `WarnCtx`
- `FromContext` for extracting logger with context fields

**Builder Pattern Configuration**
- Fluent API for configuration
- Methods: `WithEnvironment`, `WithLevel`, `WithAppName`, `WithVersion`, `WithFile`, `WithFileRotation`, `WithTimezone`, `WithConsole`
- Default timezone: Vietnam (UTC+7)

### Gin Integration

**Request Logging Middleware**
- Automatic request ID generation with UUID v7 support
- Request/response body capture on errors (status >= 400)
- Configurable skip paths for health checks and metrics
- Log levels based on status code: INFO (2xx/3xx), WARN (4xx), ERROR (5xx)

**Configuration Options**
- `WithRequestIDHeader` - Custom request ID header name
- `WithMaxBodyLogSize` - Limit body size to log
- `WithLogRequestBody` - Toggle request body logging
- `WithLogResponseBody` - Toggle response body logging
- `WithSkipPaths` - Paths to exclude from logging
- `WithUUIDv7` - Toggle UUID v7 for request IDs

### GORM Integration

**SQL Query Logging**
- Automatic SQL parsing for operation type and table name
- Duration tracking in milliseconds
- Rows affected counting
- Caller information

**Slow Query Detection**
- Configurable threshold (default: 200ms)
- Automatic `slow_query` flag for slow queries

**Configuration Options**
- `WithSlowThreshold` - Slow query threshold duration
- `WithIgnoreRecordNotFound` - Skip ErrRecordNotFound logging
- `WithGormLogLevel` - Set GORM log level (Silent, Error, Warn, Info)

### Dependencies

- go.uber.org/zap v1.27.0
- github.com/gin-gonic/gin v1.9.1
- github.com/google/uuid v1.6.0
- gorm.io/gorm v1.25.7
- gopkg.in/natefinch/lumberjack.v2 v2.2.1

### Requirements

- Go 1.22+
