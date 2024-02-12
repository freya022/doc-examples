# Slash Command Interface
```java
public interface ISlashCommand {
    void execute(SlashCommandInteractionEvent event);

    CommandData getCommandData();
}
```
This will be the class that every command will implement.

# Example Command
```java
public class MessageCommand implements ISlashCommand {
    @Override
    public CommandData getCommandData() {
        // additionally, options & sub commands may be added here
        return Commands.slash("message", "Sends a message to the channel this was executed in.");
    }

    @Override
    public void execute(SlashCommandInteractionEvent event) {
        event.reply("Hello").queue();
    }
}
```
# Main Class Example
```java
public class Main {
    private final Map<String, ISlashCommand> commands = new HashMap<>();

    public Main() {
        // start jda instance here before this method
        this.loadCommands();
    }

    private void loadCommands() {
        // register custom commands
        this.commands.put("message", new MessageCommand());
  
        // register the commands
        final CommandListUpdateAction commands = this.jda.updateCommands();
        this.commands.values().forEach(command -> commands.addCommands(commanfd.getCommandData()));
        commands.queue();
    }
}
```
Add another method in your main class:
```java
@Nullable
public ISlashCommand getCommand(@NotNull String key) {
    return this.commands.get(key);
}
```
# Command Listener
```java
// Do not forget to register this listener.
@Override
public void onSlashCommandInteraction(@NotNull SlashCommandInteractionEvent event) {
    final ISlashCommand command = this.main.getCommand(event.getName());
    if (command == null) return; // command was not registered in the loadCommands method
    command.execute(event); // handles the slash command
}
```
**Tip:** If your command reply takes longer than 3 seconds, consider deferring the event and edit your reply using the hook.