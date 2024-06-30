Now that your command is done, we can create the class that will:
* Hold the slash command objects
* Update the slash commands on Discord once JDA loads any guild
* Listen for slash command events and execute the right command

```java
public class SlashCommandManager extends ListenerAdapter {
    private final Map<String, ISlashCommand> commands = new HashMap<>();
    private boolean updated = false;

    // Adds multiple commands to the map
    public void addCommands(ISlashCommand... slashCommands) {
        for (ISlashCommand slashCommand : slashCommands) {
            CommandData commandData = slashCommand.getCommandData();
            // Associate the command's name to the slash command object
            commands.put(commandData.getName(), slashCommand);
        }
    }

    // Listens for a GuildReadyEvent and then updates the global commands
    // This will run multiple times, so we need to make sure it only runs once
    @Override
    public void onGuildReady(@NotNull GuildReadyEvent event) {
        if (this.updated) return; // Return if already updated
        this.updated = true;

        // Add the commands on the global scope
        event.getJDA().updateCommands()
                .addCommands(commands.values().stream().map(ISlashCommand::getCommandData).toList())
                .queue();
    }

    @Override
    public void onSlashCommandInteraction(@NotNull SlashCommandInteractionEvent event) {
        // Get our slash command by name
        ISlashCommand slashCommand = commands.get(event.getName());
        if (slashCommand == null) {
            event.reply("This command was not found")
                    .setEphemeral(true)
                    .queue();
            return;
        }
        
        // The slash command exists with such name, execute it
        slashCommand.execute(event);
    }
}
```
