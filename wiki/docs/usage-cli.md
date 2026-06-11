# Command Line Tool

The CLI entry point is `de.inkvine.dota2stats.commandline.Dota2StatsCLI`. The Maven jar manifest points to that class, so the packaged jar can be started with `java -jar`.

```bash
mvn package
java -jar target/dota2stats-1.0.0-SNAPSHOT.jar
```

Running without options prints help.

## Syntax

```text
dota2stats <options>
```

## Options

| Short option | Long option | Argument | Purpose |
| --- | --- | --- | --- |
| `-f` | `--findplayer` | `name` | Search for players and print matching names and 32-bit Steam account IDs. |
| `-s` | `--stats` | `accountid` | Aggregate stats for a player account ID. |
| `-k` | `--key` | `apikey` | Valve Web API key. Required for `--stats`. |
| `-n` | `--number` | `numberofmatches` | Number of recent matches to aggregate. |
| `-dto` | `--dateto` | `timestamp` | Date limit used with `--stats`; implemented as `forDateMinimum`. |
| `-dsince` | `--datesince` | `timestamp` | Date limit used with `--stats`; implemented as `forDateMaximum`. |
| `-pUrl` | `--proxyUrl` | `url` | HTTP proxy host. |
| `-pPort` | `--proxyPort` | `port` | HTTP proxy port. |

!!! note
    The CLI only enables proxy mode when both `--proxyUrl` and `--proxyPort` are present.

## Examples

Search for players named `Hans`:

```bash
java -jar target/dota2stats-1.0.0-SNAPSHOT.jar -f Hans
```

Aggregate the most recent 100 matches for account ID `123456`:

```bash
java -jar target/dota2stats-1.0.0-SNAPSHOT.jar \
  -s 123456 \
  -n 100 \
  -k YOUR_API_KEY
```

Aggregate stats with a date bound:

```bash
java -jar target/dota2stats-1.0.0-SNAPSHOT.jar \
  -s 123456 \
  -dsince 1355356800 \
  -k YOUR_API_KEY
```

Use a proxy:

```bash
java -jar target/dota2stats-1.0.0-SNAPSHOT.jar \
  -s 123456 \
  -n 100 \
  -k YOUR_API_KEY \
  -pUrl proxy.example.com \
  -pPort 8080
```
