You should avoid using `upsertCommand` as it only adds one command, which will quickly add up on the number of requests your bot does, and also does not let you delete commands easily.

Instead, you should use `updateCommands` as:
- It adds all the commands at once
- It removes the commands that are not present in the list
- Commands that are not created/modified/removed do not count toward the 200/day rate limit

You essentially tell Discord "these are the commands I support" and it adds/modifies/removes commands as necessary.

**Tip:** If your commands are the same everywhere, always add them using `JDA`, at startup using an event listener:
```kotlin
class CommandUpdater(jda: JDA, commands: List<CommandData>) {
    init {
        jda.listener<GuildReadyEvent> { event ->
            cancel() // Unregisters this listener, meaning this can only run once

            event.jda.updateCommands()
                .addCommands(commands)
                .await()
        }
    }
}
```