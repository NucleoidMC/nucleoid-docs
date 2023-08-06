# Implementing statistics

!!! warning
    The final statistics API is only available on Plasmid 0.5 for 1.17 and higher, as some things have changed since the initial implementation in Plasmid 0.4

Plasmid provides an API for allowing minigames to record statistics for their players, and can be implemented to allow leaderboards to be generated for games (soon&trade;).

## Before you begin
This guide assumes that you have a minigame already implemented and want to add support for tracking statistics. If you simply would like to create a minigame, see the [Getting Started guide](/plasmid/01_getting_started).

It also expects that you are on the latest version of Plasmid 0.5 with statistics support.

## Bundles of fun
(Well it might not seem fun, but its the first step for implementing statistics into your game.)

The first step for implementing statistics is getting your hands on a `GameStatisticBundle`, which is a class provided by plasmid that holds per-player and global statistics for your current game. You can do this quite easily within the constructor of your `GameActive` class like this:
```java
public class MyGameActive {
    /* other fields */
    public final GameStatisticBundle statistics;

    private MyGameActive(GameSpace gameSpace, /* other parameters */) {
        /* other initialization logic */

        // The value passed to getStatistics should usually be the ID of your minigame/mod
        this.statistics = gameSpace.getStatistics().bundle(MyGame.ID);
    }

    /* other game logic */
}
```

You also need to provide a translation for the name of your bundle, with the translation key in the form `statistic.<bundle>.<namespace>`. This `namespace` is whatever you passed into `gameSpace.getStatistics().bundle()`, so double check it matches.

## Getting some keys
Time to get implementi- Oh, we still need to do something else first :/

Once you have a `GameStatisticsBundle`, the next step is to actually increment some statistics, and this is where the specifics can become different between games, as every game is somewhat unique.

!!! note "What are StatisticKeys?"
    `StatisticKey`s are a type-safe identifier for a specific statistic, and internally store both an `Identifier`.

### Standard keys
Plasmid provides several built in `StatisticKey`s in a conveniently named `StatisticKeys` class. Here are some examples:

- `GAMES_PLAYED`
- `KILLS`
- `DAMAGE_DEALT`
- `QUICKEST_TIME`

### Custom keys
You can create your own `StatisticKey`s and store them in `public static final` fields in a dedicated class, usually named something like `MyGameStatistics`.
```java
public class MyGameStatistics {
    public static final StatisticKey<Integer> SOME_COOL_STAT =
        // or StatisticKey.doubleKey or StatisticKey.floatKey
        StatisticKey.intKey(new Identifier(MyGame.ID, "some_cool_stat"));
}
```

If you implement custom keys, you need to ensure you provide translations for their names, in the form `statistic.<id namespace>.<id path>`, where `id namespace` and `id path` are the namespace and path of the `Identifier` you passed as the first argument when creating the key.

!!! tip
    If you think other minigames could use a custom `StatisticKey` you implement, mention it in `#tools-and-libraries` [on Discord](https://nucleoid.xyz/discord) and it might get included in plasmid's `StatisticKeys` class.

## Incrementing statistics
Now for the actually interesting part.

!!! info "Global and per-player statistics"
    Per-player statistics are fairly self-explanatory; they're things like `KILLS` or `QUICKEST_TIME` that apply to a single player.
    Global statistics are a little different, as their values are not associated with a particular player, but with the entire game session.
    Global statistics can be used to store things like the number of teams in the game or the length of a course.

Incrementing the statistics uses a fluent API style like the following:
```java
// For a player
this.statistics.forPlayer(player).increment(StatisticKeys.DEATHS, 1);
// Or a global statistic
this.statistics.global().set(MyGameStatistics.TEAM_COUNT, 5);
```
`player` can be either a `UUID`, `PlayerRef` or `ServerPlayerEntity`.

The final step is to scatter these increments around your minigame and collect statistics for whatever seems interesting for players.

## Finished!
And then that's it, your minigame now has statistics support 🎉!

If you need a hand implementing or don't understand something, feel free to [join the Discord](https://nucleoid.xyz/discord/) and speak to me (@tom_the_geek) in `#minigame-dev`.

## Extra: debugging
If you want to double-check that your statistics are being counted correctly, you can add `-Dplasmid.debug_statistics=true` to your JVM arguments and plasmid will print out a JSON formatted version of all `GameStatisticBundle`s at the end of any game.
