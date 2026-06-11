# API Reference

This page summarizes the public interfaces present in `src/main/java/de/inkvine/dota2stats`.

## `Dota2Stats`

```java
List<PlayerSearchResult> searchByPlayerName(String name)
    throws Dota2StatsAccessException;

MatchHistory getMostRecentMatchHistory()
    throws Dota2StatsAccessException;

MatchHistory getMatchHistory(MatchHistoryFilter filter)
    throws Dota2StatsAccessException;

MatchDetail getMatchDetails(long matchId)
    throws Dota2StatsAccessException;

PlayerStats getStats(long accountId, MatchHistoryFilter filter)
    throws Dota2StatsAccessException;

PlayerStats getStats(long accountId, int numberOfMatches)
    throws Dota2StatsAccessException;
```

## Match history

`MatchHistory` exposes:

| Method | Return type |
| --- | --- |
| `getStatus()` | `int` |
| `getNumberOfResults()` | `int` |
| `getTotalNumberOfResults()` | `int` |
| `getResultsRemaining()` | `int` |
| `getMatchOverviews()` | `List<MatchOverview>` |

`MatchOverview` exposes players, match ID, match sequence number, start time, and lobby type.

## Match details

`MatchDetail` exposes:

| Method | Return type |
| --- | --- |
| `didRadianWin()` | `boolean` |
| `getDurationOfMatch()` | `int` |
| `getMatchOverview()` | `MatchOverview` |
| `getFirstBloodTime()` | `int` |
| `getHumanPlayer()` | `int` |
| `getLeagueId()` | `int` |
| `getPositiveVotes()` | `int` |
| `getNegativeVotes()` | `int` |
| `getGameMode()` | `GameMode` |
| `getPlayers()` | `List<MatchDetailPlayer>` |

!!! note
    The method name is `didRadianWin()` in the source code.

`MatchDetailPlayer` extends `MatchOverviewPlayer` and adds player performance details such as kills, deaths, assists, leaver status, gold, last hits, denies, GPM, XPM, damage, hero level, and skilled ability order.

## Player search

`PlayerSearchResult` exposes:

| Method | Return type |
| --- | --- |
| `getName()` | `String` |
| `getIconUrl()` | `String` |
| `getAccountId()` | `long` |

## Aggregated player stats

`PlayerStats` exposes:

| Method | Meaning |
| --- | --- |
| `getKillDeathAssistRatio()` | KDA ratio |
| `getKillDeathRatio()` | KD ratio |
| `getOverallKills()` | Total kills |
| `getKillsPerMatch()` | Average kills per match |
| `getOverallDeaths()` | Total deaths |
| `getDeathsPerMatch()` | Average deaths per match |
| `getOverallAssists()` | Total assists |
| `getAssistsPerMatch()` | Average assists per match |
| `getOverallLastHits()` | Total last hits |
| `getLastHitsPerMatch()` | Average last hits per match |
| `getOverallDenies()` | Total denies |
| `getDeniesPerMatch()` | Average denies per match |
| `getGoldPerMinute()` | Average GPM |
| `getXPPerMinute()` | Average XPM |
| `getNumberOfMatches()` | Number of matches included |

## Exceptions

`Dota2StatsAccessException` is a checked exception extending `Exception`. The implementation throws it for access and parsing failures, such as network access problems or unexpected API responses.
