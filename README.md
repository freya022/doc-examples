# Doc examples

A repository of code examples for various languages and libraries, served by [Doxxy](https://github.com/freya022/Doxxy).

## How it works

The [index file](index.conf) must be edited to add code examples,
it essentially is an array with an element per message file.

Each message file must be stored at: `examples/[Library]/[Language]/[File]`

## Contributing
Before making a PR, check that your message is well formatted on Discord.
A bot will then validate the content of your PR.

## Schema

### Example object

| Name        | Type     | Description                                                                                         | Choices               |
|-------------|:---------|-----------------------------------------------------------------------------------------------------|-----------------------|
| `file`      | String   | The file name of the message content                                                                |                       |
| `languages` | String[] | Array of supported languages                                                                        | Java, Kotlin          |
| `library`   | String   | The target library                                                                                  | JDK, JDA, BotCommands |
| `title`     | String   | The title of the example                                                                            |                       |
| `targets`   | String[] | The targets of this example, may be a simple class name, a class + method name, or a full signature |                       |

**Note:** A class + method name, such as `JDA#queue`, will apply to every overload of that method.