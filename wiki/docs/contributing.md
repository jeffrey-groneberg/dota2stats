# Contributing

This repository does not currently include a dedicated contribution guide, test suite, or release instructions. Use the Maven build and the existing package structure as the source of truth when making changes.

## Development workflow

1. Install Java 8 or newer and Maven.
2. Clone the repository.
3. Make focused changes under `src/main/java`.
4. Build the project with Maven:

```bash
mvn package
```

## Coding conventions visible in the repository

- Java packages use the `de.inkvine.dota2stats` namespace.
- Public behavior is exposed through interfaces in the domain packages.
- Implementation classes live in matching `impl` packages.
- External access errors are surfaced through `Dota2StatsAccessException`.
- CLI parsing is handled with Apache Commons CLI in `Dota2StatsCLI`.

## Areas to handle carefully

!!! warning "External APIs"
    Changes to request URLs, query parameters, parsing, or aggregation behavior affect live calls to Valve's Web API or Dotabuff. Keep changes small and verify them against the existing public interfaces.

!!! note "Incomplete fields"
    The README and source comments indicate that some detailed match fields, such as item slots and additional units, are not fully implemented.

## Documentation

The wiki is stored in `wiki/` and configured by `wiki/mkdocs.yml`. Pages live under `wiki/docs/`, and every page should be listed in the `nav` section so it appears in the Material navigation.
