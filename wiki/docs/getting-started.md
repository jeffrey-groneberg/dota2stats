# Getting Started

## Prerequisites

Install the tools and credentials the repository actually uses:

| Requirement | Why it is needed |
| --- | --- |
| Java 8 or newer | `pom.xml` sets `maven.compiler.source` and `maven.compiler.target` to `1.8`. |
| Maven | The project is a Maven `jar` project with dependencies and packaging configured in `pom.xml`. |
| Valve Web API key | Required for Valve statistics calls such as match history, match details, and aggregated stats. |

Get a Valve Web API key from:

```text
http://steamcommunity.com/dev/apikey
```

!!! note
    Player name search uses Dotabuff search in `Dota2StatsImpl`. Valve match and stats calls use the Steam Web API key.

## Clone and build

```bash
git clone https://github.com/jeffrey-groneberg/dota2stats.git
cd dota2stats
mvn package
```

The Maven build is configured to create a runnable jar:

- `maven-jar-plugin` sets the main class to `de.inkvine.dota2stats.commandline.Dota2StatsCLI`;
- `maven-shade-plugin` runs during the `package` phase so runtime dependencies are included in the packaged artifact.

The artifact coordinates in `pom.xml` are:

```xml
<groupId>de.inkvine</groupId>
<artifactId>dota2stats</artifactId>
<version>1.0.0-SNAPSHOT</version>
```

## Use as a local Maven dependency

If you want to use the wrapper from another local Maven project, install it into your local Maven repository:

```bash
mvn install
```

Then reference the artifact coordinates from `pom.xml`:

```xml
<dependency>
  <groupId>de.inkvine</groupId>
  <artifactId>dota2stats</artifactId>
  <version>1.0.0-SNAPSHOT</version>
</dependency>
```

## Quick smoke check

Check that Java is available:

```bash
java -version
```

After packaging, run the CLI jar produced under `target/`:

```bash
java -jar target/dota2stats-1.0.0-SNAPSHOT.jar
```

Running without options prints the Commons CLI help text.
