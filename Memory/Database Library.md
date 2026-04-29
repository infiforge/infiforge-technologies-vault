# Database Library

## Overview

Library module for database connections supporting MongoDB, MySQL, MariaDB, PostgreSQL, and SQLite.

## Location

`/home/dave/work/libraries/deno/database/`

## Supported Database Types

| Type | Enum Value | Status |
|------|-----------|--------|
| MongoDB | `mongodb` | ✅ Supported |
| MySQL | `mysql` | ✅ Supported |
| MariaDB | `mariadb` | ✅ Supported |
| PostgreSQL | `postgres` | 🔄 Planned |
| SQLite | `sqlite` | 🔄 Planned |

## Configuration Interface

### DatabaseConnectionConfig

```typescript
interface DatabaseConnectionConfig {
  type: DatabaseType;
  name: string;
  priority?: number;
  maxRetries?: number;        // Default: 3
  retryDelayMs?: number;       // Default: 1000 (MongoDB), 2000 (MySQL)
  maxRetryDelayMs?: number;    // Default: 30000
  config: MongoConfig | MySqlConfig | PostgresConfig | SqliteConfig;
}
```

### DatabaseOptions

```typescript
interface DatabaseOptions {
  activeDatabases?: DatabaseType[];
  connections?: DatabaseConnectionConfig[];
  transactionStrategy?: TransactionStrategy;
  defaultDatabase?: string;
  maxDatabaseRetries?: number;     // Default: -1 (infinite loop)
  databaseRetryDelayMs?: number;  // Default: 30000ms
  // Legacy support
  uri?: string;
  uriCert?: string;
  uriLocal?: string;
  database?: string;
  config?: MongoConfig;
}
```

## Retry Configuration

### Per-Database Connection Retries

Each database connection supports:
- `maxRetries`: Maximum connection attempts before giving up (default: 3)
- `retryDelayMs`: Initial delay between retries in milliseconds (default: 1000 for MongoDB, 2000 for MySQL)
- `maxRetryDelayMs`: Maximum delay cap for exponential backoff (default: 30000ms)

### Database-Level Retry Loop

The `connectMultiple()` method tries all configured databases in priority order:
- `maxDatabaseRetries`: Number of full database loops before giving up (default: -1 = infinite)
- `databaseRetryDelayMs`: Delay between database loop iterations (default: 30000ms)

## Service Configuration

### All 11 Services Updated

| Service | Database Type | maxRetries | retryDelayMs | maxRetryDelayMs | maxDatabaseRetries | databaseRetryDelayMs |
|---------|---------------|-----------|--------------|-----------------|-------------------|-------------------|
| bliss | mongodb | 3 | 1000 | 30000 | -1 | 30000 |
| compete | mongodb | 3 | 1000 | 30000 | -1 | 30000 |
| farmup | mongodb | 3 | 1000 | 30000 | -1 | 30000 |
| hail | mongodb | 3 | 1000 | 30000 | -1 | 30000 |
| infiforge | mongodb | 3 | 1000 | 30000 | -1 | 30000 |
| letease | mongodb | 3 | 1000 | 30000 | -1 | 30000 |
| proxly | mongodb | 3 | 1000 | 30000 | -1 | 30000 |
| qihms | mongodb | 3 | 1000 | 30000 | -1 | 30000 |
| ringly | mongodb | 3 | 1000 | 30000 | -1 | 30000 |
| synch | mongodb | 3 | 1000 | 30000 | -1 | 30000 |
| kilimo | mysql | 3 | 2000 | 30000 | -1 | 30000 |

### MongoDB Atlas Credentials

Each MongoDB config has explicit user, password, and database fields:

| Service | uriCert | uriPassword | user | password | database |
|---------|--------|------------|------|----------|----------|
| bliss | mongodb+srv://bliss.utn0dbs.mongodb.net/?authSource=%24external&authMechanism=MONGODB-X509&appName=bliss | mongodb+srv://bliss:TYH5AnHA0BYRT81q@bliss.utn0dbs.mongodb.net/?appName=bliss | bliss | TYH5AnHA0BYRT81q | bliss |
| compete | mongodb+srv://compete.z3onkxx.mongodb.net/?authSource=%24external&authMechanism=MONGODB-X509&appName=Compete | mongodb+srv://compete:qLh3aWXOmEBrOTet@compete.z3onkxx.mongodb.net/?appName=Compete | compete | qLh3aWXOmEBrOTet | compete |
| farmup | mongodb+srv://farmup.w2dive2.mongodb.net/?authSource=%24external&authMechanism=MONGODB-X509&appName=farmup | mongodb+srv://farmup:CgC9SX6LYWLWPVRC@farmup.w2dive2.mongodb.net/?appName=farmup | farmup | CgC9SX6LYWLWPVRC | farmup |
| hail | mongodb+srv://hail.05hw8ji.mongodb.net/?authSource=%24external&authMechanism=MONGODB-X509&appName=Hail | mongodb+srv://hail:B5ouarOppMh8ld0b@hail.05hw8ji.mongodb.net/?appName=Hail | hail | B5ouarOppMh8ld0b | hail |
| infiforge | mongodb+srv://infiforge.rky7yc4.mongodb.net/?authSource=%24external&authMechanism=MONGODB-X509&appName=infiforge | mongodb+srv://infiforge:YAUug6mv3YvDtxMf@infiforge.rky7yc4.mongodb.net/?appName=infiforge | infiforge | bHJ1VX5PfNRMRj3D | infiforge |
| letease | mongodb+srv://letease.sugqgur.mongodb.net/?authSource=%24external&authMechanism=MONGODB-X509&appName=letease | mongodb+srv://letease:N5LQ8VeweZQNgfXp@letease.sugqgur.mongodb.net/?appName=letease | letease | N5LQ8VeweZQNgfXp | letease |
| proxly | mongodb+srv://proxly.47g8cyv.mongodb.net/?authSource=%24external&authMechanism=MONGODB-X509&appName=proxly | mongodb+srv://proxly:qzaFzF6blY5mHNBG@proxly.47g8cyv.mongodb.net/?appName=proxly | proxly | 9qcDaCiD2KzXbtWI | proxly |
| qihms | mongodb+srv://qihms.nq5n4cw.mongodb.net/?authSource=%24external&authMechanism=MONGODB-X509&appName=qihms | mongodb+srv://qihms:bey5ftrMQwDIIQgr@qihms.nq5n4cw.mongodb.net/?appName=qihms | qihms | NItfbIVzPE9Zj34n | qihms |
| ringly | mongodb+srv://ringly.ugnypue.mongodb.net/?authSource=%24external&authMechanism=MONGODB-X509&appName=ringly | mongodb+srv://ringly:vAIf7auXvJqjvvxO@ringly.ugnypue.mongodb.net/?appName=ringly | ringly | vAIf7auXvJqjvvxO | ringly |
| synch | mongodb+srv://synch.evxlexo.mongodb.net/?authSource=%24external&authMechanism=MONGODB-X509&appName=Synch | mongodb+srv://synch:MvnxeUFBRy9f7UJP@synch.evxlexo.mongodb.net/?appName=Synch | synch | mkTiwtsz1GOC8JJh | synch |

### MySQL Credentials (kilimo)

| Service | Host | Port | User | Password | Database |
|---------|------|------|------|----------|----------|
| kilimo | 127.0.0.1 | 3306 | kilimo | kilimo | kilimo |

## Library Implementation

### MongoConnection.connect()

Lines 92-100 in `database.ts`:
- Uses `connConfig.maxRetries`, `retryDelayMs`, `maxRetryDelayMs`
- Falls back to defaults if not configured
- Logs warning when using defaults

### MySqlConnection.connect()

Lines 333-384 in `database.ts`:
- Uses `connConfig.maxRetries`, `retryDelayMs`
- Retry loop with configurable delay

### DatabaseService.connectMultiple()

Lines 620-718 in `database.ts`:
- Database-level retry loop
- Sorts by priority
- Returns true if ANY database connects
- Respects `maxDatabaseRetries` and `databaseRetryDelayMs`

## Usage

```typescript
import { DatabaseModule } from "@infiforge/database";

const dbModule = new DatabaseModule(options);
await dbModule.initialize();
await dbModule.configure(serviceInstance, options);
await dbModule.start();
```

## Related Notes

- [[Infiforge Services Memory]] - Service overview
- [[Infiforge Observability Library]] - Monitoring and metrics
- [[Backend Development]] - Deno backend patterns