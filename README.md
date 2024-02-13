# Doc examples
A repository of code examples for various languages and libraries,
served by [Doxxy](https://github.com/freya022/Doxxy).

## Indexing examples
The [index file](index.json) must be edited to add code examples,
each element describes one example.

### File storage
* Standalone examples must be stored at: `examples/[Library]/[Name]/[Language].md`
* Multipart examples must be stored at: `examples/[Library]/[Name]/[Language]/[PartFileName].md`

## Contributing
Before making a PR, check that:
* The content is well formatted on Discord.
* Each part is under [the character limit](https://docs.jda.wiki/net/dv8tion/jda/api/entities/Message.html#MAX_CONTENT_LENGTH).

## Schema
Property names suffixed with `?` are optional, while types suffixed with `?` are nullable.

### Example object

| Name        | Type      | Description                                                                                                                                                                                                     | Choices               |
|-------------|:----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------|
| `name`      | String    | The name of the folder containing the files                                                                                                                                                                     |                       |
| `languages` | String[]  | Array of supported languages                                                                                                                                                                                    | Any, Java, Kotlin     |
| `library`   | String    | The target library                                                                                                                                                                                              | JDK, JDA, BotCommands |
| `title`     | String    | The title of the example                                                                                                                                                                                        |                       |
| `parts?`    | Part[]?   | The parts of this example, ignored if empty or has a single element                                                                                                                                             |                       |
| `targets?`  | String[]? | The targets of this example, can be empty, may be a simple class name, a class + method name, or a full signature<br/> A class + method name, such as `JDA#queue`, will apply to every overload of that method. |                       |

**Note for examples using the `Kotlin` language:** The code snippets can use JDA-KTX.

### Part object

| Name           | Type    | Description                                                            |
|----------------|---------|------------------------------------------------------------------------|
| `fileName`     | String  | The name of the file containing the example part                       |
| `label`        | String  | The select option's label                                              |
| `emoji?`       | String? | The select option's emoji, can be an unicode emoji or any custom emoji |
| `description?` | String? | The select option's description                                        |