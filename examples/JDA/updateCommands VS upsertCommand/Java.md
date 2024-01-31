You should avoid using `upsertCommand` as it only adds one command, which will quickly add up on the number of requests your bot does, and also does not let you delete commands easily.

Instead, you should use `updateCommands` as:
- It adds all the commands at once
- It removes the commands that are not present in the list
- Commands that are not created/modified/removed do not count toward the 200/day rate limit

You essentially tell Discord "these are the commands I support" and it adds/modifies/removes commands as necessary.

**Tip:** If your commands are the same everywhere, always add them using `JDA`, at startup using an event listener:
```java
// Don't forget to register this listener in your JDABuilder
public class CommandUpdater extends ListenerAdapter {
    private final List<CommandData> commands;
    private boolean updated = false;
    
    public CommandUpdater(@NotNull List<CommandData> commands) {
        this.commands = commands;
    }
    
    @Override
    public void onGuildReady(@NotNull GuildReadyEvent event) {
        if (updated) return; // Return if already updated
        updated = true;
        
        event.getJDA().updateCommands()
                .addCommands(commands)
                .queue();
    }
}
```