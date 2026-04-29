---
date: 2026-04-29
updated: 2026-04-29
tags:
  - library
  - deno
  - security
  - cors
  - encryption
---

# Security Library

## Overview

Security library provides security features for Infiforge services including CORS handling, security headers, input sanitization, and encryption.

## Purpose

- Protect services from internet attacks
- Provide CORS handling
- Add security headers (helmet)
- Sanitize user input
- Provide encryption utilities
- Enable IP blocking/whitelisting

## Key Features

- CORS handling
- Security headers (helmet-style)
- Input sanitization
- Email validation
- Encryption utilities (AES, RSA)
- IP blocking/whitelisting

## Module Pattern

```typescript
initialize(): Promise<void>
configure(instance: ServiceInstance, options: SecurityOptions): Promise<void>
start(instance?: ServiceInstance): Promise<void>
stop(): Promise<void>
restart(): Promise<void>
```

## Usage

```typescript
import { SecurityModule } from "@infiforge/security";

// In service initialize()
this.securityModule = new SecurityModule();
await this.securityModule.initialize();
await this.securityModule.configure(this, {
  cors: {
    allowedOrigins: ["https://example.com"],
    allowedMethods: ["GET", "POST", "PUT", "DELETE"]
  },
  headers: {
    frameGuard: true,
    hsts: true,
    noSniff: true
  }
});

// Apply security middleware
const app = this.network.http.getApp();
await this.securityModule.applyMiddleware(app);

// Validate email
const isValid = this.securityModule.isEmail("user@example.com");

// Encrypt data
const encrypted = await this.securityModule.encrypt("sensitive data");
const decrypted = await this.securityModule.decrypt(encrypted);
```

## Configuration Options

```json
{
  "security": {
    "enabled": true,
    "cors": {
      "allowedOrigins": ["*"],
      "allowedMethods": ["GET", "POST", "PUT", "DELETE", "PATCH"],
      "allowedHeaders": ["Content-Type", "Authorization"]
    },
    "headers": {
      "frameGuard": true,
      "hsts": true,
      "noSniff": true,
      "xssProtection": true
    },
    "ip": {
      "blocked": [],
      "whitelisted": []
    }
  }
}
```

## Security Headers

- X-Frame-Options: DENY or SAMEORIGIN
- Strict-Transport-Security (HSTS)
- X-Content-Type-Options: nosniff
- X-XSS-Protection
- Content-Security-Policy

## TODO: Future Enhancements

- Rate limiting (integrate with Redis)
- SQL injection prevention
- Comprehensive XSS protection
- Industry-standard hashing (bcrypt, argon2)
- Request validation (JSON schema)

## Dependencies

- Network library (for middleware application)
- Config library

## Services Using It

All services use Security for protection:
- Bliss, Compete, Farmup, Hail, Letease, Proxly, Qihms, Ringly, Synch, Kilimo

## Location

`/home/dave/work/libraries/deno/security/`
