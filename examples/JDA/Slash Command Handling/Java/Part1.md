Using an interface and a class which manages multiple commands is a simple yet effective way to make your commands.
The goal is to have a single class which receives the command events, and then run the right class automatically.

### The command interface
Each command will be its own file and will implement an interface, such as:
```java
public interface ISlashCommand {
    // Runs the slash command, only called if the command name matches 
    void execute(@NotNull SlashCommandInteractionEvent event);

    // Returns the object describing the slash command
    @NotNull
    CommandData getCommandData();
}
```

### Creating a command
For now, let's create a command which sends a message to the channel.
```java
public class MessageCommand implements ISlashCommand {
    @NotNull
    @Override
    public CommandData getCommandData() {
        // Options & subcommands may be added here
        // See #addOptions and #addSubcommands
        return Commands.slash("message", "Sends a message to the channel this was executed in.");
    }

    @NotNull
    @Override
    public void execute(@NotNull SlashCommandInteractionEvent event) {
        event.reply("Hello").queue();
    }
}
```
**Tip:** If your command reply takes longer than 3 seconds, consider deferring the event and edit your reply using the hook.