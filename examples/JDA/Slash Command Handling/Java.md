Start by making an interface which has both of the methods that we will need:
```java
public interface ISlashCommand {
    void execute(@NotNull SlashCommandInteractionEvent event);

    @NotNull
    CommandData getCommandData();
}
```
This will be the class that every command will implement and will be used later to register using the JDA instance.
Within our main class, we can create a `Map<String, ISlashCommand>` which listens to when a command is run using the key. (Example later).
For now, lets create a class which basically does nothing than send a message to the channel. We can do this by making a new class and implementing the interface.
```java
public class MessageCommand implements ISlashCommand {
    @Override
    @NotNull
    public CommandData getCommandData() {
        // additionally, options & sub commands may be added here
        return Commands.slash("message", "Sends a message to the channel this was executed in.");
    }

    @Override
    @NotNull
    public void execute(@NotNull SlashCommandInteractionEvent event) {
        event.reply("Hello").queue();
    }
}
```
Now, to handle & add the commands to the JDA instance, we can make a `Map<String, ISlashCommand>` in the main class:
```java
public class Main {
    private final Map<String, ISlashCommand> commands = new HashMap<>();

    public Main() {
        // start jda instance here, alternatively main(String[] args) works too.
        this.loadCommands();
    }

    private void loadCommands() {
        // here we need to add the command (with a name) to the map. So we can do:
        this.commands.put("message", new MessageCommand()); // additionally, if you need the main JDA instance you can get it from the event or pass it into the constructor of command class.

        // additionally, the commands also need to be registered on the JDA instance.    
        final CommandListUpdateAction commands = this.jda.updateCommands();
        this.commands.values().forEach(command -> commands.addCommands(command.getCommandData()));
        commands.queue();
    }
}
```
Lastly, we need a listener which listens to when a command is executed, we can do this inside a `ListenerAdapter` with another method in the main class:
```java
@Nullable
public ISlashCommand getCommand(@NotNull String key) {
    return this.commands.get(key);
}
```
Listener (you will need to pass an instance of your main class into the listener class, to make sure that you have the `getCommand` method inside there):
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