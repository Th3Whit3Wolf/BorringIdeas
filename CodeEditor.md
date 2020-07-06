# The Best Code Editor



Here are somethings I think an editor needs to standout



* A rope data structure for text storage.
* A multiprocess architecture, with front-end and plug-ins each with their own process.
* Fully embracing async design.
* [CRDT](https://en.wikipedia.org/wiki/Conflict-free_replicated_data_type) as a mechanism for concurrent modification.
* Written in rust (take advantage of safety, performance, built-in testing, and cross compilation to many targets)
* A great syntax highlighter
* Startup Fast
* Beautiful UI



## Plugins

I think there should be three types of plugins

* core 
* non-core
* extensible



Core plugins should managed by the core teams, should just do, and once established should not need to be updated very frequently (with the syntax highlighting being an exception):



* Syntax Highlighting
* Auto Pair
* Language Server Client
* Search
* Folding
* Word Wrap
* Misc



Non-Core and extensible plugins should improve the ui, ux, ergnomics, or otherwise make the development experience better in some way.

Core & Non-Core plugins should be written in rust and communicate with the core via [tarpc](https://github.com/google/tarpc) while extensible plugins can be written in anything that with a flatbuffer implementation (as of write now is C, C++, C#, Dart, Go, Java, Javascript, Typescript, Lobster, PHP, Python, Rust, and Swift).



| Plugin     | RPC                                                          | Ships w/? | Written In                                                   |
| ---------- | ------------------------------------------------------------ | --------- | ------------------------------------------------------------ |
| Core       | [Tarpc](https://github.com/google/tarpc)                     | Yes       | Rust                                                         |
| Non-Core   | [Tarpc](https://github.com/google/tarpc)                     | Yes       | Rust                                                         |
| Extensible | [Flattbuffers](https://google.github.io/flatbuffers/flatbuffers_support.html) | No        | C, C++, C#, Dart, Go, Java, Javascript, Typescript, Lobster, PHP, Python, Rust, or Swift |



#### Why use FlatBuffers?

* Access to serialized data without parsing/unpacking
* forwards/backwards compatibility
* Memory efficiency and speed
* Flexible
* Tiny code footprint
* Strongly typed
* Convenient to use
* Cross platform code with no dependencies



### Syntax Highlighting

Discussed more [below](#The-Syntax-Highlighter)



### Auto Pairs

Automatically pair single quotes, double quotes, parenthesis, curly brackets, and square brackets. 

In languages where  if, do,def statements and functions are finished with and end, endif,fi,etc automatically add it after user presses enter after finishing the original statement.

Whenever the user presses enter while inside a parenthesis, curly brackets, or square brackets indent new line.



### Language Server Client

This will probably mostly just be using [LanguageClient neovim](https://github.com/autozimu/LanguageClient-neovim) as this almost exclusively does.



### Search

It makes the most send to either use [ripgrep](https://github.com/BurntSushi/ripgrep), this is what atom and vscode use. Alternatively we could also use the regrex library (what ripgreps uses) directly.



### Folding

Fold should be base off of syntax tree, maybe communicate with Syntax highlighter



### Word Wrap

**Incremental word wrap**

* Doesn't re-wrap entire paragraph
* Starts at line before edit
* Continues until re-sync with previous state
* Line breaks stored in another specialization of xi-rope tree
* Async



### Misc

* Minmap
* Multipane Splits and Tabs (Maybe be apart of the core-editor?)
* Builtin Terminal
* File Explorer
* Line Counter



### More Ideas for Non Core Plugins

* [SWC](https://github.com/swc-project/swc) integration - Super fast javascript / typescript compiler (20x faster than babel)
  * Also Spack - Similiar to webpack but brought to you by the swc project
* A Live server
* Rainbow brackets (Change color of  brackets pairs based on depth)
* Rainbow indentation (Change background color of  indents based on depth)
* Automatic Code Formatter
  * Should simply understand what formatters are available for a given language
  * Be configurable, different people have different preferences
* Automatic Code Linter
  * Should simply understand what linters are available for a given language
  * Be configurable, some language (Python) have many linters that don't play well together
* Code runner
  * Should be able to compile, run, and test program without leaving the editor
  * Should now when to use:
    * cargo vs rustc
    * rails vs ruby
    * make/meson vs compiler
* Web searcher
  * Idea is to let people search the internet without leaving their editor
    * Use case 1: Reading questions and answers from stackoverflow
    * Use case 2: Researching data structures and algorithms you're trying to implement
    * Use case 3: Look at similiar code to yours on github to see how other people solve problems
    * Use case X: There are a lot of reasons why a web developer would want this
  * Will lean heavily on [Servo](https://github.com/servo/servo) for this
* Web Development specific
  * Compiler integration for CSS and HTML preproccessors
  * Transpiler integration for dart and coffeescript
  * Code Minifier
* Automatically change background color for any hexadecimal color 
* VSC Integration (i.e. git, mercurial, pujal)
* Something to make it easier to programin for java
  * My understanding is tools like netbeans and eclipse offer features no one else does for java devs
* Github, Gitlab, Gitea, and Bitbucket Integrations
* Downloader for Language Servers, Linters, and formatters
* Debugger
* Vim Mode
* Live Preview Markdown Editor
* Export markdown and latex to pdf
* Image optimizer





## The Syntax Highlighter

The syntax highlighter should live in a different process, with asynchronous updates so typing is never slowed down.

Right now the two best syntax highlighters are:

* [tree-sitter](https://github.blog/2018-10-31-atoms-new-parsing-system/)
* [Lezer](https://marijnhaverbeke.nl/blog/lezer.html)



##### [Talks on Tree-sitter](https://tree-sitter.github.io/tree-sitter/#talks-on-tree-sitter)

- [Strange Loop 2018](https://www.thestrangeloop.com/2018/tree-sitter---a-new-parsing-system-for-programming-tools.html)
- [FOSDEM 2018](https://www.youtube.com/watch?v=0CGzC_iss-8)
- [GitHub Universe 2017](https://www.youtube.com/watch?v=a1rC79DHpmY)

##### [Underlying Research](https://tree-sitter.github.io/tree-sitter/#underlying-research)

The design of Tree-sitter was greatly influenced by the following research papers:

- [Practical Algorithms for Incremental Software Development Environments](https://www2.eecs.berkeley.edu/Pubs/TechRpts/1997/CSD-97-946.pdf)
- [Context Aware Scanning for Parsing Extensible Languages](http://www.umsec.umn.edu/publications/Context-Aware-Scanning-Parsing-Extensible)
- [Efficient and Flexible Incremental Parsing](http://ftp.cs.berkeley.edu/sggs/toplas-parsing.ps)
- [Incremental Analysis of Real Programming Languages](https://pdfs.semanticscholar.org/ca69/018c29cc415820ed207d7e1d391e2da1656f.pdf)
- [Error Detection and Recovery in LR Parsers](http://what-when-how.com/compiler-writing/bottom-up-parsing-compiler-writing-part-13)
- [Error Recovery for LR Parsers](http://www.dtic.mil/dtic/tr/fulltext/u2/a043470.pdf)

Ways they're similar

*  Ingeniously abuse [GLR parsing](https://en.wikipedia.org/wiki/GLR_parser), where the parser can try multiple interpretations simultaneously, to integrate automatic error-correction without a lot of extra complexity. 
* Error Correction - A GLR parser can split its parse stack and run both sides alongside each other for a while until it becomes clear which one works out. That's pretty much exactly what a search algorithm does—it tracks a number of branches that it still has to explore, and continues to explore them, possibly pruning unpromising branches with some heuristic, until it finds a solution. To be able to get good results, or at least *some* result, in messy situations like longer stretches of invalid input, each branch has a badness score associated with it, which is increased (linearly) each time a recovery action is taken, and decreased (asymptotically) every time it can consume a token normally. What we want to do is, after an error, try all kinds of possible recovery tricks, which recursively branch off a large amount of states. But then, after a bit of that, we should consolidate to one or, at most, a few parse states again, because parsing input in a whole bunch of different ways is expensive.

Ways they're different

* Lezer's gramars optimized for compactness, both in parser table size and syntax tree size. They need to be transfered over the web so size matters.



## Startup Fast

Something I always appreciated about vim and sublime vs vscode and atom is that they could start almost instantly. My vim config starts in about 35ms, sublime isn't quite that fast but its still pretty quick. By contrast atom takes several seconds, vscode less so but they also do a lot to create a perception of being ready before they actually are.

Something cool emacs can do is run in (server mode)the background at startup. So by the time the users opens it it opens at the speed it takes to draw a window. 

Ideally the best editor I think would open at the speed of sublime, (maybe vim if we could use some of vscode's tricks) and have the ability to run in server mode like emacs.



