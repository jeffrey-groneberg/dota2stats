# dota2stats

**dota2stats** is a Java library and command-line tool for reading Dota 2 statistics from Valve's Web API. The project provides a wrapper interface, `de.inkvine.dota2stats.Dota2Stats`, implemented by `Dota2StatsImpl`, plus a CLI entry point at `de.inkvine.dota2stats.commandline.Dota2StatsCLI`.

The current code can:

- search for Dota 2 players by name through Dotabuff search results;
- fetch recent public match history from Valve's `GetMatchHistory` endpoint;
- fetch match history with filters such as account ID, date range, game mode, skill, and result count;
- fetch detailed match data from Valve's `GetMatchDetails` endpoint;
- aggregate player stats such as KDA, KD, kills, deaths, assists, last hits, denies, GPM, and XPM.

!!! note "Repository status"
    The README notes that some response attributes may not be populated yet. The source also contains TODO comments around detailed item and additional-unit data in `MatchDetailPlayer`.

## Main entry points

| Area | Source |
| --- | --- |
| Public wrapper interface | `src/main/java/de/inkvine/dota2stats/Dota2Stats.java` |
| Wrapper implementation | `src/main/java/de/inkvine/dota2stats/impl/Dota2StatsImpl.java` |
| CLI main class | `src/main/java/de/inkvine/dota2stats/commandline/Dota2StatsCLI.java` |
| Maven build | `pom.xml` |

## Documentation map

- [Getting Started](getting-started.md): prerequisites, API key, build, and local installation.
- [Java API Usage](usage-java-api.md): code examples for the wrapper.
- [Command Line Tool](usage-cli.md): CLI options and examples.
- [Configuration](configuration.md): API key, proxy, filters, CLI flags, and build settings.
- [Architecture](architecture.md): package layout and request flow.
- [API Reference](api-reference.md): public interfaces and domain objects.
- [Contributing](contributing.md): how to work safely in this repository.
