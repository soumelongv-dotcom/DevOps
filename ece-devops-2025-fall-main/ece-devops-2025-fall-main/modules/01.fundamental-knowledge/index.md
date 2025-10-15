---
duration: 1-3 hours
---

# Fundamental knowledge

## Common tools

### Software installation

Install the following software on your computer:

- [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- [Node.js](https://nodejs.org/en/download/)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- [Docker](https://docs.docker.com/get-docker/)

### Terminal

- Most useful developer tool
- Any number of customizations
- On Windows: Linux Bash Shell, Powershell, Git Bash (don't use default CMD!)
- On macOS / Linux: native Terminal

### Bash

Learn Bash base commands:

- [Bash base commands](https://www.educative.io/blog/bash-shell-command-cheat-sheet)
- [GameShell: a "game" to teach the Unix shell](https://github.com/phyver/GameShell)

### Vi(m)

- Bash text editor
- Use `:` to enter command mode
  - `w` to write file
  - `q` to quit
  - `q!` to quit without saving
  - `x` to write & quit
- Use `/` to search for text
- Use `i` to enter edit mode and `ESC` to exit it
- `vimtutor` is the best tutorial to learn

### Password manager

- Using a password manager is mandatory
- [Buttercup](https://buttercup.pw/)
- [Bitwarden](https://bitwarden.com/)
- [KeePass](https://keepass.info/)
- [pass](https://www.passwordstore.org/)

## Networking

### Client VS Server

- Two parts of a distributed computing model:
  - Client requests the info and displays it
  - Server processes the request and services the result
- We will do server work + a bit of client-side

### The IP protocol

- Send data from one computer to another over a network (ex: client/server)
- Use of IPV4 addresses (ex: 172.16.254.1), IPV6 also available but not much used
- Data packaged in IP packets with 2 sections
  - Header: IP version, addresses, TTL, ...
  - Data: the packet's content

### The HTTP protocol

- Application protocol for transmitting hypermedia documents (HTML)
- Two types of messages: *requests- & *responses*
- HTTP message split between *headers- & *body*
- HTTP response always contains
  - the *protocol- (HTTP/1.1)
  - a *status code- (200, 404, ...)
  - a *status text- (page not found)

### API and REST API

- Application Programming Interface (API)
- In web: REST API
  - Expose a set of HTTP routes
  - Use HTTP verbs (GET / POST / PUT / DELETE)
  - Client connects to communicate
  - Usually communicating in JSON
  
REST API example: https://petstore.swagger.io/
  
### SSL/TLS & HTTPS

(Secure Sockets Layer / Transport Layer Security)
- Establish an encrypted link over a network
- Exchange of public & private keys to secure the exchange
  - Server sends SSL certificate + public key
  - Client checks the certificate & answers with an encrypted session key
  - Client & server exchange messages encrypted with the keys to authenticate
- SSL certificate has been certified by a renowned authority
- HTTPS: HTTP secured with SSL/TLS

### SSH - Secure shell

- Cryptographic network protocol to operate network services securely over an unsecured network
- Exchange of public & private keys to secure the exchange
  - Client has the private key
  - Server needs to have the associated public key
  - Client & server exchange messages encrypted with the keys to authenticate

### The SFTP protocol

- Send files over SSH
- ex: deploy a website to a server
- SFTP apps: FileZilla, Cyberduck, WinSCP, ...

## Progamming tools

### Databases

- RDBMS (basis for SQL): MySQL, PostgreSQL, Hive, Oracle
- NoSQL:
  - Filesystems: posix and object storage
  - Documents store: MongoDB, ElasticSearch
  - Key/value and sorted key/value stores: Redis, LevelDB
  - Column families: HBase, Cassandra
  - Graph DBs: JanusGraph (ex-TitanDB), Neo4J

### Editors, IDE

As a developer, the terminal being your partner and the editor is your best friend: 

- [Vim](https://www.vim.org/) (Linux, macOS, Windows)   
  Free, one of the most powerful, many will say the most powerful, single file or project-oriented.
- [Atom](https://atom.io/) (Linux, macOS, Windows)   
  Free project-oriented, minimalist, and productive UI (my day to day favorite editor), slow and memory hungry
- [VS Code](https://code.visualstudio.com/) (Linux, macOS, Windows)   
  Free most popular editor, most active community, and plugins development
- [Sublime Text](https://www.sublimetext.com/) (Linux, macOS, Windows)   
  Free, very fast, single file or project-oriented
- [BBedit](https://www.barebones.com/products/bbedit/) (macOS)   
  Free version very powerful, very fast
- [Notepad++](https://notepad-plus-plus.org/) Windows)   
  Free, almost a Windows standard, powerful and fast
- [WebStorm](https://www.jetbrains.com/webstorm/) (Linux, macOS, Windows)
  Licensed, 30 days trial
- ...

### Gravatar

- Globally Recognized   
  Gravatar (Globally Recognized Avatar) provides a universal avatar service that links user avatars to their email addresses, making them visible across participating sites.
- Ease of Use   
  Users can create a Gravatar account and upload an avatar once, which will automatically appear on all sites that support Gravatar, enhancing consistency and recognition.
- Widely Supported   
  Many popular websites and applications, including WordPress, GitHub, and Stack Overflow, integrate with Gravatar to display user avatars.
- Personal Branding   
  Gravatar helps in personal branding by ensuring that your chosen image appears alongside your content across the web, providing a cohesive and professional online presence.

## Common Knowledge

### Programmation paradigms

- Declarative   
  The program describes its desired results without explicitly listing commands or steps.
- Imperative   
  The control flow is an explicit sequence of commands.
- Functional   
  The computation proceeds by function calls, no global state
- Object-oriented   
  Everything is an object, functions are methods and are executed with the object's context
- Event-driven   
  The control flow is triggered and determined by async actions
- Fluent API   
  Chaining method calls in a readable, fluid manner.
- Pure function   
  A function that, given the same inputs, always produces the same output and has no side effects, not altering any state or data outside its scope.

### Communities

- HackerNews
  - Most qualified community
  - Large technological scope coverage
- StackOverflow
  - Huge data source
  - Reactive community
  - Any subject
  - Lots of answered questions (> 1M !)
  - Don’t forget the source code!
- Dev.to, Medium
  - Blog publications

## Languages

### Markdown

- Simple Syntax   
  Markdown uses easy-to-read, plain text formatting syntax that can be quickly learned and applied.
- Versatility   
  It can be used to create formatted text for web pages, documents, notes, and more.
- Compatibility   
  Markdown files can be converted to various formats such as HTML, PDF, and Word.
- Lightweight   
  As a plain text format, Markdown is lightweight and doesn't require special software to read or write.
- Widespread Use   
  Popular platforms like GitHub, Reddit, and Stack Overflow support Markdown, making it a valuable skill.
- Improves Workflow   
  It enhances productivity by allowing writers and developers to focus on content without worrying about complex formatting.

### JSON format

- JSON is a subset of JavaScript, JavaScript is built upon JSON
- Data format

Valid JavaScript:

```js
const user = {
  firstname: 'Lucky',
  lastname: `Luke`,
  "password": "secret",
  age: 42,
  mood: 0.9,
  languages: ['en', ['fr_FR', 'fr_CA'] , , ],
  level: null,
  friends: undefined,
};
```

Valid JSON:

```json
{
  "firstname": "Lucky",
  "lastname": "Luke",
  "password": "secret",
  "age": 42,
  "mood": 0.9,
  "languages": ["en", ["fr_FR", "fr_CA"]],
  "level": null
}
```

### YAML format

- Human-readable data-serialization format
- Indentations are important!
- *"Yet Another Markup Language"*
- A JSON extention, JSON is YAML, YAML is not JSON

The same as above JSON, but YAML:

```yml
firstname: Lucky
lastname: Luke
password: secret
age: 42
mood: 0.9
languages:
  - en
  - - fr_FR
    - fr_CA
level:
```

---

*The content of this document, including all text, images, and associated materials, is the exclusive property of Adaltas and is protected by applicable copyright laws. Unauthorized distribution, reproduction, or sharing of this content, in whole or in part, is strictly prohibited without the express written consent of the author(s). Any violation of this restriction may result in legal action and the imposition of penalties as prescribed by law.*
