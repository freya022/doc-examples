Lastly, we need a listener which listens to when a command is executed, we can do this inside a `ListenerAdapter` with another method in the main class.

Listener (you will need to pass an instance of your main class into the listener class, to make sure that you have the `getCommand` method inside there):
```java
// Do not forget to register this listener.
public class SlashListener extends ListenerAdapter {
    private final Main application;

    public SlashListener(@NotNull Main application) {
        this.application = application;
    }

    @Override
    public void onSlashCommandInteraction(@NotNull SlashCommandInteractionEvent event) {
        final ISlashCommand command = this.main.getCommand(event.getName());
        if (command == null) return; // command was not registered in the loadCommands method
        command.execute(event); // handles the slash command
    }
}
```
**Tip:** If your command reply takes longer than 3 seconds, consider deferring the event and edit your reply using the hook inside the `execute` method.