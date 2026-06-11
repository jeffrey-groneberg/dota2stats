# Java API Usage

The public API is the `Dota2Stats` interface. Create a `Dota2StatsImpl` with your Valve API key, optionally with proxy settings.

```java
import de.inkvine.dota2stats.Dota2Stats;
import de.inkvine.dota2stats.impl.Dota2StatsImpl;

Dota2Stats stats = new Dota2StatsImpl("YOUR_API_KEY");
```

With an HTTP proxy:

```java
Dota2Stats stats = new Dota2StatsImpl("YOUR_API_KEY", "YOUR_PROXY_URL", 8080);
```

All wrapper methods that access external data can throw `Dota2StatsAccessException`.

## Search for a player

```java
import java.util.List;

import de.inkvine.dota2stats.Dota2Stats;
import de.inkvine.dota2stats.domain.playersearch.PlayerSearchResult;
import de.inkvine.dota2stats.exceptions.Dota2StatsAccessException;
import de.inkvine.dota2stats.impl.Dota2StatsImpl;

Dota2Stats stats = new Dota2StatsImpl("YOUR_API_KEY");

try {
    List<PlayerSearchResult> results = stats.searchByPlayerName("john doe");

    for (PlayerSearchResult result : results) {
        System.out.println(result);
    }
} catch (Dota2StatsAccessException e) {
    System.out.println(e.getMessage());
}
```

`PlayerSearchResult` exposes `getName()`, `getIconUrl()`, and `getAccountId()`.

## Get recent match history

```java
import java.util.List;

import de.inkvine.dota2stats.Dota2Stats;
import de.inkvine.dota2stats.domain.MatchOverview;
import de.inkvine.dota2stats.domain.matchhistory.MatchHistory;
import de.inkvine.dota2stats.exceptions.Dota2StatsAccessException;
import de.inkvine.dota2stats.impl.Dota2StatsImpl;

Dota2Stats stats = new Dota2StatsImpl("YOUR_API_KEY");

try {
    MatchHistory history = stats.getMostRecentMatchHistory();
    List<MatchOverview> matches = history.getMatchOverviews();

    for (MatchOverview match : matches) {
        System.out.println(match);
    }
} catch (Dota2StatsAccessException e) {
    System.out.println(e.getMessage());
}
```

## Filter match history

Use `MatchHistoryFilter` to add Valve query parameters. The builder methods return the same filter, so they can be chained.

```java
import de.inkvine.dota2stats.domain.GameMode;
import de.inkvine.dota2stats.domain.filter.MatchHistoryFilter;
import de.inkvine.dota2stats.domain.matchhistory.MatchHistory;

MatchHistory history = stats.getMatchHistory(
    new MatchHistoryFilter()
        .forAccountId(1234)
        .forGameMode(GameMode.All_Pick)
        .forMaximumNumberOfResults(25)
);
```

## Get match details

```java
import java.util.List;

import de.inkvine.dota2stats.domain.matchdetail.MatchDetail;
import de.inkvine.dota2stats.domain.matchdetail.MatchDetailPlayer;

MatchDetail detail = stats.getMatchDetails(12345);
List<MatchDetailPlayer> players = detail.getPlayers();

for (MatchDetailPlayer player : players) {
    System.out.println(player);
}
```

## Aggregate player stats

`getStats` collects match history and match details, then calculates totals and averages for a player.

```java
import de.inkvine.dota2stats.domain.filter.MatchHistoryFilter;
import de.inkvine.dota2stats.domain.playerstats.PlayerStats;

PlayerStats byRecentMatches = stats.getStats(123456, 300);

PlayerStats byDateFilter = stats.getStats(
    123456,
    new MatchHistoryFilter()
        .forDateMaximum(1349827200)
        .forDateMinimum(1349395200)
);

System.out.println(byRecentMatches);
System.out.println(byDateFilter);
```

!!! warning "Use aggregated stats carefully"
    The implementation fetches match details for every selected match using a fixed thread pool of 25 requests. The README explicitly warns that this can generate heavy network traffic and should not be used too often.
