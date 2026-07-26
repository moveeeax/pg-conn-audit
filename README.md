# pg-conn-audit

> Find out which service is sitting on idle-in-transaction at 3am.

**Status:** 🚧 In development

## Overview

Track connection usage by application_name and state over time, answering which service is holding idle-in-transaction connections at 3am.

## Features

- Samples `pg_stat_activity` on an interval and stores the series, so you can look at last night instead of right now
- Breaks connections down by `application_name`, `usename`, database and state
- Tracks how long each backend has been `idle in transaction` and reports the longest offenders with their query text
- Warns when in-use connections approach `max_connections` or a pooler's pool size
- Correlates waiting backends with the blocking PID
- Prometheus exposition endpoint alongside the CLI report

## Stack

Python + `psycopg` for sampling, `click` for the CLI, `rich` for the terminal report, `prometheus-client` for the metrics endpoint.

## Usage

```bash
pg-conn-audit watch --dsn "$DATABASE_URL" --interval 10s --group-by application_name --idle-tx-threshold 60s
```

## License

MIT
