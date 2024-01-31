# Doc examples

A repository of code examples for various languages and libraries, served by [Doxxy](https://github.com/freya022/Doxxy).

## How it works

The [index file](index.conf) must be edited to add code examples,
it essentially is an array with an element per message file.

Each message file must be stored at: `examples/[Library]/[Name]/[Language].md`

## Contributing
Before making a PR, check that your message is well formatted on Discord.
A bot will then validate the content of your PR.

## Schema

### Example object

| Name        | Type     | Description                                                                                                                                                                                                     | Choices               |
|-------------|:---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------|
| `name`      | String   | The name of the folder containing the files                                                                                                                                                                     |                       |
| `languages` | String[] | Array of supported languages                                                                                                                                                                                    | Any, Java, Kotlin     |
| `library`   | String   | The target library                                                                                                                                                                                              | JDK, JDA, BotCommands |
| `title`     | String   | The title of the example                                                                                                                                                                                        |                       |
| `targets`   | String[] | The targets of this example, can be empty, may be a simple class name, a class + method name, or a full signature<br/> A class + method name, such as `JDA#queue`, will apply to every overload of that method. |                       |

**Note for examples using the `Kotlin` language:** The code snippets can use JDA-KTX.