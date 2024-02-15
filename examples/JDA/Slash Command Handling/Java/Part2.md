```java
public class Main {
    private final Map<String, ISlashCommand> commands = new HashMap<>();

    public Main() {
        // start jda instance here, alternatively main(String[] args) works too.
        // command registration
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

    // if your main class extends ListenerAdapter then you can just access the map directly. Otherwise you will need this method to access it in a different class. 
    @Nullable
    public ISlashCommand getCommand(@NotNull String key) {
        return this.commands.get(key);
    }
```
}
```