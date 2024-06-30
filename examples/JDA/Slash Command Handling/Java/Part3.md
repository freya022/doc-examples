Finally, we can use our slash command manager, and add our first slash command:
```java
public class Bot {
    private final JDA jda;

    private Bot() {
        // Let's create our commands
        final MessageCommand messageCommand = new MessageCommand();

        // Then register them
        final SlashCommandManager slashCommandManager = new SlashCommandManager();
        slashCommandManager.addCommands(
                messageCommand
                // Can also add more
        );

        // Finally, create our JDA instance
        this.jda = JDABuilder.createLight(token)
                // Further configuration
                // Add our slash command manager
                .addEventListeners(slashCommandManager)
                .build();
    }

    // You should not have to get a JDA instance often,
    // as they are given in every event.
    @NotNull
    public JDA getJDA() {
        return this.jda;
    }

    public static void main(String[] args) {
        new Bot();
    }
}
```
