# Configuration

Configuration is supplied in code through constructors and filter builders, or on the command line through Commons CLI options. There are no repository configuration files for API keys, proxies, or runtime defaults.

## API key

Valve Web API calls require an API key:

```java
Dota2Stats stats = new Dota2StatsImpl("YOUR_API_KEY");
```

The CLI requires `-k` / `--key` when using `-s` / `--stats`:

```bash
java -jar target/dota2stats-1.0.0-SNAPSHOT.jar -s 123456 -n 100 -k YOUR_API_KEY
```

## Proxy

The implementation supports an HTTP proxy through the three-argument constructor:

```java
Dota2Stats stats = new Dota2StatsImpl("YOUR_API_KEY", "proxy.example.com", 8080);
```

Internally, `Dota2StatsImpl` creates an Apache HttpClient `HttpHost` with scheme `http`.

CLI proxy mode requires both options:

```bash
java -jar target/dota2stats-1.0.0-SNAPSHOT.jar \
  -s 123456 \
  -n 100 \
  -k YOUR_API_KEY \
  -pUrl proxy.example.com \
  -pPort 8080
```

## Match history filters

`MatchHistoryFilter` maps Java builder methods to Valve query parameter names.

| Builder method | Query parameter | Value source |
| --- | --- | --- |
| `forSkill(Skill)` | `skill` | `Skill.Any`, `Skill.Normal`, `Skill.High`, `Skill.Very_High` |
| `forGameMode(GameMode)` | `game_mode` | `GameMode` enum value |
| `forPlayerName(String)` | `player_name` | Player name string |
| `forAccountId(long)` | `account_id` | 32-bit account ID |
| `forDateMinimum(long)` | `date_min` | Unix timestamp |
| `forDateMaximum(long)` | `date_max` | Unix timestamp |
| `forMinimumPlayersNumber(int)` | `min_players` | Minimum player count |
| `forStartingMatchId(long)` | `start_at_match_id` | Match ID used for paging |
| `forMaximumNumberOfResults(int)` | `matches_requested` | Requested result count |

Example:

```java
MatchHistoryFilter filter = new MatchHistoryFilter()
    .forAccountId(123456)
    .forDateMinimum(1349395200)
    .forDateMaximum(1349827200)
    .forMaximumNumberOfResults(100);
```

## Game modes

`GameMode` defines these numeric values:

| Enum | Value |
| --- | ---: |
| `All_Pick` | 1 |
| `Captains_Mode` | 2 |
| `Random_Draft` | 3 |
| `Single_Draft` | 4 |
| `All_Random` | 5 |
| `INTRO_DEATH` | 6 |
| `The_Diretide` | 7 |
| `Reverse_Captains_Mode` | 8 |
| `Greeviling` | 9 |
| `Tutorial` | 10 |
| `Mid_Only` | 11 |
| `Least_Played` | 12 |
| `New_PlayerPool` | 13 |

## Build settings

The Maven project is configured with:

| Setting | Value |
| --- | --- |
| Packaging | `jar` |
| Java source/target | `1.8` |
| Main class | `de.inkvine.dota2stats.commandline.Dota2StatsCLI` |
| Runtime packaging | `maven-shade-plugin` bound to `package` |

The declared dependencies are Apache HttpClient modules, Gson, Jsoup, and Commons CLI.
