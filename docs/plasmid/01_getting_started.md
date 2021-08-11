# Getting started

If you would like to get up and running quickly with a basic game setup, clone the [plasmid-starter](https://github.com/NucleoidMC/plasmid-starter) repository, run `init.py`, and then delete `.git`, `README.md`, and `init.py`. Alternatively, if you are looking for examples of existing implemented games, take a look through the [Nucleoid Organisation](https://github.com/NucleoidMC) repositories.

### Adding to Gradle
Assuming you [already have a Fabric workspace set up](https://fabricmc.net/wiki/tutorial:setup), the first step to setting up Plasmid will be adding it to your gradle buildscript. You will need to add the maven repository as well as the plasmid dependency. `PLASMID_VERSION` should be replaced with the latest version from [Maven](https://maven.nucleoid.xyz/xyz/nucleoid/plasmid).

```groovy
repositories {
  maven { url = 'https://maven.nucleoid.xyz/' }
}

dependencies {
  // ...
  modImplementation 'xyz.nucleoid:plasmid:PLASMID_VERSION'
}
```

### Creating a Basic Game
A `GameType` is the entry-point to creating a game with Plasmid: they provide a unique identifier for your game, as well as all the information needed for it to be able to call your code when the game starts.

Plasmid is designed to encourage data-driven games, and works with the concept of a _game config_. A game config is simply just a JSON file in a datapack that references your `GameType` and passes along any extra data that may be useful for configuring your game. This is especially useful because it allows the creation of different variations of the same game type, such as by using a different map or tweaking some game mechanics.

To register a `GameType`, you will need to call `GameType.register()` in your `ModInitializer` class. A call to register a `GameType` may look something like:
```java
GameType.register(
        new Identifier("plasmid_example", "example"),
        ExampleGame::open,
        ExampleGameConfig.CODEC
);
```

Let's break down what is going on here:  
- `new Identifier("plasmid_example", "example")`
   - declares the unique identifier that the game config JSONs will use to reference your game type
- `ExampleGame::open`
   - references a function that will be used to start your game when a player requests it
- `ExampleGameConfig.CODEC`
   - a `Codec` that will be used to load configuration from the game config JSON

This naturally will not compile yet: neither `ExampleGame` nor `ExampleGameConfig` exist!

#### Creating our config in code
Let's create our `ExampleGameConfig` class, which will hold a `String` field that will be used as a message to send to the player when they join.

```java
public class ExampleGameConfig {
    public final String greeting;

    public ExampleGameConfig(String greeting) {
        this.greeting = greeting;
    }
}
```

That's simple enough! But we're missing the `CODEC` field that we referenced earlier. What is that about?

A `Codec` is a very helpful tool implemented by Mojang's [DataFixerUpper](https://github.com/Mojang/DataFixerUpper) library that allows for convenient loading of a JSON file. A more detailed wonderful explanation of Codecs by Drullkus can be found [here](https://gist.github.com/Drullkus/1bca3f2d7f048b1fe03be97c28f87910), but for simple purposes, all you need to know is the pattern for putting them together.

Essentially, it goes like this:
```java
public static final Codec<ExampleGameConfig> CODEC = RecordCodecBuilder.create(instance -> {
    return instance.group(
            Codec.STRING.fieldOf("greeting").forGetter(config -> config.greeting)
    ).apply(instance, ExampleGameConfig::new);
});
```

Most things here you can ignore, but there are a few important things to note:
 - `Codec<ExampleGameConfig>`
    - The type of class that is being deserialized into is referenced as a generic on the `Codec`
 - `Codec.STRING.fieldOf(...).forGetter(...)`
    - This declares a field with a given name and type that will be read from the JSON. 
    - You will notice that `Codec.STRING` is itself a `Codec<String>`: a field can be created from any codec, where that codec will be used to deserialize the value of that field. This is very useful in allowing combinations of codecs to create complex structures!
    - The parameter to `.fieldOf()` specifies the name of the field that this value will be read from
    - `.forGetter()` specifies a lambda that is used to retrieve the value of a field. This is useful since codecs allow for both serialization and deserialization, and the getter is required to turn the object back into data.
 - `ExampleGameConfig::new`
    - This tells the codec how to create the object once it has deserialized all the fields. This requires a method reference to the constructor for the given object with all the fields **in order as they were specified!**.
    - For example, here we take in one `String` field, and the constructor we reference also takes a single `String` parameter.

The JSON that corresponds to this codec would look like:
```json
{
  "greeting": "Hello World!"
}
```

#### Creating a config
Now that we know what data our config should hold, we can create a game config for plasmid to load.

All game configs need to be located in a datapack (or within mod resources) at `data/<namespace>/games/<id>.json`. For the purpose of a mod, the `namespace` should just be your mod id, and the `id` can be any unique name that will later be used to reference your game config from inside Minecraft.

Plasmid requires only 2 JSON fields from the config, while the rest is loaded as per the config codec that you set up. These two fields are `type` and `name`, where the `type` refers to the `GameType` you created earlier in `namespace:path` format, and `name` defines a human-readable name to describe this game config. This does not need to be unique!

For our purposes, our game config at `data/plasmid_example/games/hello_world_example.json` will look like:
```json
{
  "type": "plasmid_example:example",
  "name": "Hello World Example",
  "greeting": "Hello, World!"
}
```

#### Writing the code to start our game
Now that we have set up a config and have told Plasmid how to read from it, we can finally write the code to actually start our game.

For the purpose of this example, let's create an `ExampleGame` class. We will use this class to hold the state of the game as well as our `ExampleGameConfig` that got loaded. For now though, we just need to create this `open` function that we referenced to the `GameType`.

This should look like:
```java
public class ExampleGame {
    public static GameOpenProcedure open(GameOpenContext<ExampleGameConfig> context) {
        // get our config that got loaded by Plasmid
        ExampleGameConfig config = context.getConfig();

        // create a very simple map with a stone block at (0; 64; 0)
        MapTemplate template = MapTemplate.createEmpty();
        template.setBlockState(new BlockPos(0, 64, 0), Blocks.STONE.getDefaultState());

        // create a chunk generator that will generate from this template that we just created
        TemplateChunkGenerator generator = new TemplateChunkGenerator(context.getServer(), template);

        // set up how the world that this minigame will take place in should be constructed
        BubbleWorldConfig worldConfig = new BubbleWorldConfig()
                .setGenerator(generator)
                .setDefaultGameMode(GameMode.ADVENTURE)
                .setSpawnAt(new Vec3d(0.0, 65.0, 0.0));

        return context.createOpenProcedure(worldConfig, logic -> {
            // to be implemented
        });
    }
}
```

There is a lot to digest here, but it's not too complex if we break it down. Our `open` will be called whenever a player starts this game. The function takes a `GameOpenContext`, which holds the data from our JSON config, and returns a `GameOpenProcedure`, which instructs Plasmid how it should continue to set up the game. It is worth nothing that this function is run asynchronously on the thread pool, so it is safe to run whatever slow code here before the game starts.

The `GameOpenProcedure` is created from the `GameContext` object, and takes in a `BubbleWorldConfig` as well as a lambda that accepts a `GameLogic` parameter. A bubble world is a concept within Plasmid that represents a fully isolated and temporary world. A bubble world is created at runtime when the game starts, and deleted when it finishes. When a player joins the game, their inventory will be cleared, and when they leave, it will be restored back to them.

The most important thing to be configured within the bubble world is the chunk generator: this tells the game how the world should generate. It would be possible to, for example, pass the overworld chunk generator here, but for our purpose, we're creating an empty world with a single stone block through the convenience `TemplateChunkGenerator`. The `TemplateChunkGenerator` takes a `MapTemplate`, which is just a very basic world that contains some blocks, and loads from that into the world itself.

Finally, we need to address what to do in the lambda with the `GameLogic` parameter. The code inside this lambda will run on the main thread, and is used to run the actual game setup code. This mainly involves registering event listeners, or setting global rules.

For example:
```java
return context.createOpenProcedure(worldConfig, logic -> {
    logic.setRule(GameRule.FALL_DAMAGE, RuleResult.DENY);
    logic.on(PlayerAddListener.EVENT, player -> {
        // a player has been added!
    });
});
```

This code will disable fall damage for all players, as well as registering a listener that will be called whenever a player is added to this game.

As of right now, though, the listener won't do anything when it is called. We want it to send a greeting to the player when they join.
```java
GameSpace gameSpace = logic.getSpace();

logic.setRule(GameRule.FALL_DAMAGE, RuleResult.DENY);
logic.on(PlayerAddListener.EVENT, player -> {
    Text message = new LiteralText(config.greeting);
    gameSpace.getPlayers().sendMessage(message);
});
```

We've added logic to send a message within the listener, but what is a `GameSpace`? A `GameSpace`, as the name implies, represents the space within which a game is occurring. For all our purposes, that space is just a dimension. The `GameSpace` is useful for us in that it keeps track of all the players within it, as well as the `ServerWorld` that the game is taking place within. Here, we access the `GameSpace` through `GameLogic.getSpace()`.

Working with players additionally goes through a new Plasmid API: a `PlayerSet`. A `PlayerSet` represents just a list of players, and it can be iterated over / queried, but it additionally provides utilities for performing bulk operations over many players. For example, sending a message! Here, we use `PlayerSet.sendMessage()` to send our greeting to every player within the game. 

Tada! 🎉 We have a working game! But before we test it, let's do some minor reorganization. With all these handlers and lambdas, our code inside `createOpenProcedure` is going to get quite lengthy very quickly! It would be nice if we can put all event listeners on our `ExampleGame` object instead.

Turns out, that works just fine, and we are left with our final `ExampleGame` setup:
```java
public final class ExampleGame {
    private final GameSpace gameSpace;
    private final ExampleGameConfig config;

    private ExampleGame(GameSpace gameSpace, ExampleGameConfig config) {
        this.gameSpace = gameSpace;
        this.config = config;
    }

    public static GameOpenProcedure open(GameOpenContext<ExampleGameConfig> context) {
        ExampleGameConfig config = context.getConfig();

        MapTemplate template = MapTemplate.createEmpty();
        template.setBlockState(new BlockPos(0, 64, 0), Blocks.STONE.getDefaultState());

        TemplateChunkGenerator generator = new TemplateChunkGenerator(context.getServer(), template);

        BubbleWorldConfig worldConfig = new BubbleWorldConfig()
                .setGenerator(generator)
                .setDefaultGameMode(GameMode.ADVENTURE)
                .setSpawnAt(new Vec3d(0.0, 65.0, 0.0));

        return context.createOpenProcedure(worldConfig, logic -> {
            GameSpace gameSpace = logic.getSpace();
            ExampleGame game = new ExampleGame(gameSpace, config);

            logic.setRule(GameRule.FALL_DAMAGE, RuleResult.DENY);
            logic.on(PlayerAddListener.EVENT, game::addPlayer);
        });
    }

    private void addPlayer(ServerPlayerEntity player) {
        Text message = new LiteralText(this.config.greeting);
        this.gameSpace.getPlayers().sendMessage(message);
    }
}
```

#### Testing the game!
Once everything compiles, we can finally launch up Minecraft. If our `GameType` is all correctly set up and game config JSON in place, once opening a world, we should be able to start our game by running: `/game open <id>`. (Remember, this is referencing the name of the JSON file and not the GameType!)

So in our case: `/game open plasmid_example:hello_world_example`
...and we should be joined into our void world with a stone block with a lovely greeting!

Now, any other player can join us too by running `/game join` or clicking the link that shows up in chat.

That's it! 🎉 