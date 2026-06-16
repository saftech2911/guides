# Vim Cheatsheet for Safwan

Vim is a **modal editor**. The keys and keyboards work differently based on which mode you are, making it extremely powerful in various contexts.

By default, we are in `NORMAL` mode, which does not allow editing text, but you can navigate text buffers very easily by using Movement keys, or insert/replace at specific positions using cool keybindings.

Modes of interest are:

|Mode|Used for|How to enter it (from `NORMAL` mode)|
|:----|:--------|:------------------------------------|
|`NORMAL`|Navigating text buffers quickly **without** changing text (But can change at specific positions by entering `INSERT` mode with special keybindings - like for appending or changing inside/around something)|Its the default mode. Go here from any mode by pressing `Esc`
|`INSERT`|Used for editing text normally like regular editors. **NOTE** there are special keybindings too to enter or replace text at specific positions| <ul><li>`i` for regular insertion anywhere (**before** focused character)</li><li>`a` for appending **after** current character</li><li>`A` for appending to end of **line**</li><li>`I` for inserting at **beginning** of line</li><li>`o` for getting a new line **below** current line and then inserting.</li><li>`O` for getting a new line **above** current line and then inserting.</li><li>`c{motion}` for changing sth specific (`cw` for changing word, `ci(` for changing inside parenthesis)</li></ul>|
|`REPLACE`|Similar to `INSERT`, but this **replaces** existing text instead of adding text| Press `R`|
|`VISUAL`|Select text using keyboard to delete, copy/yank, etc.|<ul><li>`v` for selecting by character</li><li>`V` for selecting by **line**</li><li>`<C-v>` for selecting **blocks** of text across lines.</ul>
|`COMMAND`|Used for typing vim script commands or common commands for navigation, setting options, or writing changes or quitting vim| Press `:` followed by the command, like `q` for quit, `w` for write, `wq` for write and quit, `q!` for quit without saving changes, etc.

## Nouns (a.k.a. Movements)
Used to navigate, move around, or select text. Used in `NORMAL` or `VISUAL` mode

### Basic Navigation
---
|Command|What it is used for|
|:-----:|-------------------|
|`<arrow keys>`|Move up, down, left, right (what noobs do)|
|`hjkl`|`h` moves left, `j` moves down, `k` moves up, `l` moves right (what real Vim users do)

### Word Movement
---
|Command|What it is used for|
|:-----:|-------------------|
|`w`|Move forward one word at the beginning|
|`b`|Move back one word at the beginning|
|`e`|Move by words but at the end of the word|

### Special Motions (can be used for verbs accepting motions too)
---
|Command|What it is used for|
|:-----:|-------------------|
|`0`|Move to beginning of line|
|`^`|Move to first non-blank character in line|
|`$`|Move to end of line|
|`gg`|Move to the beginning of the first line in the file|
|`G`|Move to the end of the last line in the file|
|`{`|Jump backward to previous empty line (**start of paragraph**)|
|`}`|Jump forward to next empty line (**end of paragraph**)|


## Verbs (a.k.a. actions)
Used to do something to the selected word (or motion), basically like grammar it **does** something to a noun (or a noun with a modifier or counts). Works in `NORMAL` or `VISUAL` modes when navigating or selecting text.

> **COMMON SHORTCUT:** Doubling an operator applies that action to the entire current line. For ex, `dd` means delete current line, `yy` means yank current line, and so on.

> **NOTE:** Motion can be any noun with modifier or counts, like `d3w` mean delete the next 3 words, or `di(` means delete inside parentheses. Can also be special motions, like `d$` deletes till end of line. Motion can also be selected text in `VISUAL` Mode.
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

## `COMMAND` Mode
All commands **MUST** be prefixed by `:` to enter `COMMAND` mode
### Basic navigation
Common commands I will encounter daily for making changes, quitting, etc. 
|Command|What it is used for|
|:-----:|-------------------|
|`!<cmd>`|Execute `<cmd>` in shell and then press `ENTER` to come back to vim|
|`w`| Write changes to file|
|`q`|Quit Vim (works only if no change are made, OR if all changes are saved.)
|`wq`| Composes the previous two to write all changes AND then quit (order important - you will write first **then** quit)|
|`q!`| Quit without saving any changes
|`<line number>`|Go to `<line number>` (e.g. `:6` goes to the **end** of line 6)|

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
|`colorscheme <some colorscheme>`|Changes colorscheme (examples are `slate` and others, use `Tab` to go through the options)

> **NOTE:** The current options are written in VimScript, which are used in `.vimrc` and `init.vim` natively. Modern neovim configurations are written in Lua in `init.lua`, so uuse the corresponding syntax