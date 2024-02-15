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