# Vim Guide for Safwan

Vim is a **modal editor**. The keys and keybindings work differently based on which mode you are, making it extremely powerful in various contexts.

By default, we are in `NORMAL` mode, which does not allow editing text, but you can navigate text buffers very easily by using Movement keys, or insert/replace at specific positions using cool keybindings.

Watch [Reference video](https://www.youtube.com/watch?v=RZ4p-saaQkc&t=2853s&pp=ygUKdmltIGNvdXJzZQ%3D%3D) by [Florian Dedov](https://github.com/NeuralNine) for further conceptual guidance.

## Modes of Interest

|Mode|Used for|How to enter it (from `NORMAL` mode)|
|:----|:--------|:------------------------------------|
|`NORMAL`|Navigating text buffers quickly **without** changing text (But can change at specific positions by entering `INSERT` mode with special keybindings - like for appending or changing inside/around something)|Its the default mode. Go here from any mode by pressing `Esc`
|`INSERT`|Used for editing text normally like regular editors. **NOTE** there are special keybindings too to enter or replace text at specific positions| <ul><li>`i` for regular insertion anywhere (**before** focused character)</li><li>`a` for appending **after** current character</li><li>`A` for appending to end of **line**</li><li>`I` for inserting at **beginning** of line</li><li>`o` for getting a new line **below** current line and then inserting.</li><li>`O` for getting a new line **above** current line and then inserting.</li><li>`c{motion}` for changing sth specific (`cw` for changing word, `ci(` for changing inside parenthesis)</li><li>`gi` for entering `INSERT` mode where you last exited `INSERT` mode (i.e. at the `^` mark!)</li></ul>|
|`REPLACE`|Similar to `INSERT`, but this **replaces** existing text instead of adding text| Press `R`|
|`VISUAL`|Select text using keyboard to delete, copy/yank, etc.|<ul><li>`v` for selecting by character</li><li>`V` for selecting by **line**</li><li>`<C-v>` for selecting **blocks** of text across lines.</li><li>`gv` for entering `VISUAL` mode in last selection.</li></ul>
|`COMMAND`|Used for typing vim script commands or common commands for navigation, setting options, or writing changes or quitting vim| Press `:` followed by the command, like `q` for quit, `w` for write, `wq` for write and quit, `q!` for quit without saving changes, etc.

## Motions (Nouns)
Motions define *where* the cursor moves to. Used to navigate, move around, or select text. Used in `NORMAL` or `VISUAL` mode.


Can be used independently (without verbs or modifiers), OR with verbs to do something to the motion.

### Basic Navigation
---
|Command|What it is used for|
|:-----:|-------------------|
|`<arrow keys>`|Move up, down, left, right (what noobs do)|
|`hjkl`|`h` moves left, `j` moves down, `k` moves up, `l` moves right (what real Vim users do)|
|`gj`/`gk`| Move down/up by *screen line* (seful when the line wraps to span multiple visual lines)

### Word Movement
---
> **NOTE:** Important distinction between word/WORD definitions:
> - **Word**: Group of alphanumeric characters separated by whitespaces **OR** special characters like `-` or `()`
> - **WORD**: Group of alphanumeric characters seprated by whitespaces **ONLY**

|Command|What it is used for|
|:-----:|-------------------|
|`w`|Move forward one word at the beginning|
|`W`|Move forward one WORD at the beginning|
|`b`|Move back one word at the beginning|
|`B`|Move back one WORD at the beginning|
|`e`|Move forward one word at the end|
|`E`|Move forward one WORD at the end|
|`ge`|Move back one word at the end|
|`gE`|Move back one WORD at the end|

### Line/Paragraph/Screen
---
|Command|What it is used for|
|:-----:|-------------------|
|`0`|Move to beginning of line|
|`^`|Move to first non-blank character in line|
|`$`|Move to end of line|
|`g_`|Move to last non-blank character in line|
|`gg`|Move to the beginning of the first line in the file|
|`G`|Move to the end of the last line in the file|
|`<line no>G`|Go to beginning of `line no` (e.g. `70G` goes to line 70)|
|`H`| Jump to top of visible screen|
|`M`| Jump to middle of visible screen|
|`L`| Jump to bottom of visible screen|


### Paragraph/Code Blocks
---
|Command|What it is used for|
|:-----:|-------------------|
|`%`|Jump to matching character (e.g. when in a `(`, this will jump to matching `)`)|
|`{`|Jump backward to previous empty line (**start of paragraph**)|
|`}`|Jump forward to next empty line (**end of paragraph**)|
|`[[`|Jump backward to the beginning of **previous** code section or function (e.g. opening `{` for a function)|
|`]]`|Jump forward to the beginning of **next** code section or function (e.g. opening `{` for a function)|
|`[]`|Jump backward to the end of **previous** code section or function (e.g. closing `}` for a function)|
|`][`|Jump forward to the end of **next** code section or function (e.g. closing `}` for a function)|
### Find/Till in **current line**
---
|Command|What it is used for|
|:-----:|-------------------|
|`t{character}`|Jumps **till** just before the **next** matching character in the current line. (e.g. `t*` jumps just before the next `*` in the line)|
|`f{character}`|Jumps **to** the **next** matching character in the current line. (e.g. `f*` jumps to the next `*` in the line)|
|`T{character}`|Jumps **till** just before the **previous** matching character in the current line. (e.g. `T*` jumps just before the previous `*` in the line)|
|`F{character}`|Jumps **to** the **previous** matching character in the current line. (e.g. `F*` jumps to the previous `*` in the line)|
|`,`| Find the **previous** `f/F/t/T` in that line|
|`;`| Find the **next** `f/F/t/T` in that line|

### Search
---
Finds matches in the text (using regex for `/` or `?` and whole words for `*` and `#`).

Can be used with verbs as well. For example, `d/error` deletes everything from cursor position till the **next** occurence of `error` (Forward search).
|Command|What it is used for|
|:-----:|-------------------|
|`/<regex>`|Searches for regex pattern **forward**|
|`?<regex>`|Searches for regex pattern **backward**|
|`n`|Goes to **next** match|
|`N`|Goes to **previous** match|
|`*`|Search word/token under cursor **forward**|
|`#`|Search word/tokenn under cursor **backward**|

### Marks
---
Used to leave waypoints/bookmark positions in text we frequently visit so that we can jump to those positions later on using a single keybind. Once a mark is set, it can be used with verbs as well since they are motions.

#### Basic Marks and motions
|Command|What it is used for|
|:-----:|-------------------|
|`m{char}`| Set mark on focused position **(NOT A MOTION! JUST A WAY TO SET A MARK!)**|
|`'{char}`|Jump to the **line** of mark|
|`` `{char} ``| Jump to **exact position** of mark|

#### Types of Marks
|Type|What it is used for|
|:-----:|-------------------|
|`a-z`| Buffer-local : only valid within the file we set them in|
|`A-Z`| Global: valid across files. Will open the file if it is closed|

#### Special built in marks
Refer to these the same way as regular marks: `'` for beginning of line with mark, `` ` `` for the exact position of mark.
|Type|What it is used for|
|:-----:|-------------------|
|`0-9`| Marks cursor position when each Vim **process** is quit (*NOT PER FILE OR ACROSS FILES,* ***JUST SESSIONS***). 0 is where last vim process was quit, 1 is when the second last one is quit, and so on.|
|`'` or `` ` ``| Marks cursor position before last jump|
|`"`| Marks cursor position where I exited this file (one per file)|
|`.`| Position of last change (any change, even in `NORMAL` mode through verbs like `d` outside `INSERT` mode)|
|`^`| Position where we last exit `INSERT` mode|
|`[`| Start of last change/yank (change is ANY change)|
|`]`| End of last change/yank (change is ANY change)|
|`<`| Start of last selection in `VISUAL` mode|
|`>`| End of last selection in `VISUAL` mode|

> **Difference between `[]` and `^.` for changes:** `^.` remembers only **ONE** position (the LAST positon) of change, whereas `[]` remembers the WHOLE range (start/end)

## Scrolling
|Command|What it is used for|
|:-----:|-------------------|
|`zz` | Center current selection|
|`zt`| Scroll current selection to top|
|`zb` | Scroll current selection to bottom|
|`<C-f>`| Full page down|
|`<C-b>`|Full page up|
|`<C-u>`|Half page up|
|`<c-b>`|Half page down|

**TODO: Add folding commands later when necessary after setting `foldmethod`**
## Verbs (a.k.a. actions)
Used to do something to the selected word (or motion), basically like grammar it **does** something to a noun (or a noun with a modifier or counts). Works in `NORMAL` or `VISUAL` modes when navigating or selecting text.

> **COMMON SHORTCUT:** Doubling an operator applies that action to the entire current line. For ex, `dd` means delete current line, `yy` means yank current line, and so on.

> **NOTE:** Motion can be any noun with modifier or counts, like `d3w` mean delete the next 3 words, or `dj` deletes current line **and below**, `>3j` indents current line and 3 lines below it, or `di(` means delete inside parentheses. Can also be special motions, like `d$` deletes till end of line. Motion can also be selected text in `VISUAL` Mode.
### Common Operations
---
|Command|What it is used for|
|:-----:|-------------------|
|`d{motion}`|Deletes something.| 
|`y{motion}`|Copy selected text or the motion.|
|`c{motion}`|Change selected text or the motion.|
|`p`| Paste **after** the cursor.|
|`P`|Paste **before** the cursor.|
|`dd`|Delete current line. (Special case of `d`)|
|`yy`|Copy current line. (Special case of `y`)|
|`cc`|Changes the current line (special case of `c`)|
|`D`|Deletes from cursor position to end of line (same as `d$`)|
|`Y`|Copies the **full** line (same as `yy`)|
|`C`|Changes from cursor position to end of line (same as `c$`)|
|`r`|Replace **one** character (the current one) and go back to `NORMAL` mode|
|`x`|Delete the focused character|
|`s`|Substitute the focused character|
|`.`|Repeat the last action|
### Indentation
---
> **NOTE**: Auto-indent (`=`) works best with languages using braces for code blocks, like C or Java. It doesn't work too well with languages like Python where code blocks themselves are indicated by indents.

|Command|What it is used for|
|:-----:|-------------------|
|`>{motion}`| Indent (shift right)|
|`<{motion}`|Unindent (shift left)|
|`={motion}`| Auto-indent (reformats according to filetype rules)|
|`>>`|Indent current line|
|`<<`|Unindent current line|
|`==`|Auto-indent current line|

### Undo/Redo
---
|Command|What it is used for|
|:-----:|-------------------|
|`u`|Undo (like a stack)|
|`<C-r>`|Redo (like a stack)|

## Counts
You can prefix any nouns (movements) or verbs (edits) or other commands in the `NORMAL` or `VISUAL` modes to repeat the task.
> Syntax: `{count}<noun/verb command>`

Example: `5j` moves 5 lines down, `3w` moves 3 words forward, `d6w` deletes 6 words, `3p` pastes what was yanked 3 times, `5dd` means delete 5 lines and so on

> **NOTE:** Combining counts with double oprerators (for lines) multiplies the line wise scope. Example: `5dd` deletes 5 lines, `6>>` indents 6 lines, and so on.

## Modifiers
**Modifiers** are keys used between an operator (verb) and a text object (noun) to alter the scope of the action.

For example, `dw`, where `w` is a regular motion without any modifiers, would delete from current position to end of the word, but `diw`, where `w` is a text object with the modifier `i` (inner), would delete the entire word wherever the cursor is within the word (verbose: delete (`d`) inner (`i`) word (`w`))

Modifiers of interest:
|Modifier|What it is used for|
|:-----:|-------------------|
|`i`| Inside the text object(s), excludes the delimiters defining the object|
|`a`| Around the text object(s), includes the delimiters defining the object|

> **NOTE:** Can **ONLY** be used with the specified text objects (nouns) below.

## Text Objects (Nouns)
Text objects define what container you're acting on, *regardless* of cursor position. 

The text object ***ALWAYS*** means the **WHOLE** container. For example, if the cursor is in the middle of the word, `w` as a motion (as in `dw`) means *from here till the end of word*, whereas `w` as a dext object (as in `diw`) means *the whole word* (regardless of where the cursor is).

These **CANNOT** be used standalone at all, always need i/a modifiers, and always come after a verb/operator. So the syntax for using text objects is always `<verb><modifier><text object>`

|Text Object|What it is used for|
|:-----:|-------------------|
|`w`|word (delimited by whitespace or other non-alphanumeric characters)|
|`W`|WORD (delimited by whitespace **only**)|
|`s`| Sentence (defined as a chunk of text ending with a punctuation mark (`., !, or ?`) followed by a space, a tab, or an end-of-line character.)|
|`p`|Paragraph (block of text separated by blank lines)|
|`(` or `)` or `b`|Parentheses block (inside/around `()`)|
|`[` or`]`| Brackets block (inside/around `[]`)|
|`{` or `}` or `B`| Braces block (inside/around `{}`)|
|`<` or `>`| Angle bracket block (inside/around `<>`)|
|`"`| Double quoted string (inside/around `""`)|
|`'`| Single quoted string (inside/around `''`)|
|`` ` ``| Backtick quoted string (inside/around `` ` ` ``)|
|`t`|HTML/XML tag|

## Complete VIM grammar structure for all commands in `NORMAL` mode
The complete picture is 
```
[count] + verb + [modifier] + [count] + noun
                 └── if modifier present → noun must be a text object
                 └── if no modifier → noun is a motion
```
Common examples: ***TODO***

## `COMMAND` Mode
All commands **MUST** be prefixed by `:` to enter `COMMAND` mode

The `COMMAND` mode operates on ***line ranges and pattern matching*** — you tell it explicitly which lines to act on and what pattern to look for, rather than relying on cursor position at all. (This is in contrast to the `NORMAL` or `VISUAL` mode's cursor position and motions model)

So the basic grammar syntax for this mode is:
```
:[range]command[arguments]
```
> **NOTE:** Not all commands accept ranges (like `w`, `q`).
### Basic navigation
Common commands I will encounter daily for making changes, quitting, etc. 
|Command|What it is used for|
|:-----:|-------------------|
|`!<cmd>`|Execute `<cmd>` in shell and then press `ENTER` to come back to vim|
|`w`| Write changes to file|
|`q`|Quit Vim (works only if no change are made, OR if all changes are saved.)
|`wq`| Composes the previous two to write all changes AND then quit (order important - you will write first **then** quit)|
|`q!`| Quit without saving any changes
|`<line number>`|Go to `<line number>` (e.g. `:6` goes to line 6)|
|`help <cmd>`|Opens the official doc entry for that command|

### Common options (also for scripting)
---
> **NOTE**: If you do them in `COMMAND` mode the changes are temporary (disappears after exiting). For permanent changes, change your editor's config file (`~/.vimrc` for vim and `~/.config/init.lua` or `~/.config/init.vim` for neovim ).

|Command in VimScript|What it is used for|
|:-----:|-------------------|
|`set number` OR `set nu`|Activates line number|
|`set relativenumber` OR `set rnu`|Activates relative line number (relative to the current line). By default it shows current line as line 0, but if you `:set number` as well, it shows current line number for the current line and relative lines for others.|
|`set mouse=a`|Activates mouse usage|
|`set tabstop=4`|Changes tab whitespace to 4 characters|
|`set shiftwidth=4`|Changes spacing of indentation to 4 characters|
|`colorscheme <some colorscheme>`|Changes colorscheme (examples are `slate`, `retrobox` and others, use `Tab` to go through the options)

> **NOTE:** The current options are written in VimScript, which are used in `.vimrc` and `init.vim` natively. Modern neovim configurations are written in Lua in `init.lua`, so uuse the corresponding syntax