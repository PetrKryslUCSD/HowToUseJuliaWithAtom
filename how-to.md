# How to use Atom with Julia

## Atom packages

Personally, I found these packages indispensable. Obviously, for programming with Julia, I install `uber-juno`. The others I find useful in general for working in Atom.

This is the list:
```
uber-juno
minimap
auto-indent (by griiin)
split-diff
simple-drag-drop-text
highlight-line
file-icons
project-manager
center-line
tabnine
```
And this is how it is really easily installed all in one go. In the terminal, type
```
apm install uber-juno minimap auto-indent simple-drag-drop-text highlight-line file-icons project-manager center-line tabnine
```
That should install all the packages requested.

Definitely grab the TabNine autocompleter! Worth its weight in gold (which would not be much, I realize, given that it is all bits; but you know what I mean).

## Configuration


### Configuration of the  keymap

In the file	`keymap.cson`, place the following configuration:
```
# support to-folder Dragon command

'atom-text-editor:not([mini])':
  'ctrl-shift-alt-C': 'editor:copy-path'

'atom-text-editor':
  'ctrl-shift-alt-I': 'editor:auto-indent'
  'ctrl-shift-alt-w': 'editor:select-word'
  'ctrl-space': 'autocomplete-plus:activate'

'body':
  'ctrl-shift-0': 'window:toggle-dev-tools'

'.platform-win32 .find-and-replace, .platform-linux .find-and-replace':
    'alt-shift-ctrl-r': 'find-and-replace:replace-next'

'.platform-linux atom-workspace, .platform-win32 atom-workspace':
    'alt-ctrl-shift-enter': 'platformio-ide-terminal:insert-selected-text'

```


### Snippets

Create a few snippets:
```
'.source.julia':
  'forloop':
    'prefix': 'forloop'
    'body': 'for ${1:i} in ${2:1:length(${3:a})}\n
	       ${0:${3:a}[${1:i}]}\n
     end $1'
  'comprehension':
     'prefix': 'comprehension'
     'body': '[${0:a[${1:idx}]} for ${1:idx} in ${2:collection}]'
  'counter of':
    'prefix': 'counterof'
    'body': 'cnt${1:something}'
  'number of':
    'prefix': 'numberof'
    'body': 'num${1:something}'
  'doc string':
    'prefix': 'thedocs'
    'body': '"""\n    ${1:bar(x[, y])}\n\n# Arguments\n${0:Compute}\n"""'
  'if else':
    'prefix': 'ifelse'
    'body': 'if ${1:condition}\n${2:whenconditionistrue}\nelse\n${2:whenconditionisfalse}\nend'
  'set up test module':
    'prefix': 'setuptestmodule'
    'body': 'module ${1:modulename}\n
using FinEtools\n
using Test\n
function test()\n
	${0:body}\n
end\n
end\n
using .${1:modulename}\n
${1:modulename}.test()\n'
```


### Configure visual styles

- styles.less:
```
/*
 * Your Stylesheet
 *
 * This stylesheet is loaded when Atom starts up and is reloaded automatically
 * when it is changed and saved.
 *
 * Add your own CSS or Less to fully customize Atom.
 * If you are unfamiliar with Less, you can read more about it here:
 * http://lesscss.org
 */

 // style the background and foreground colors on the atom-text-editor-element itself
 atom-text-editor {
   color: hsl(50, 40%, 80%);
   background-color: hsl(190, 10%, 12%);
 }

 // style UI elements inside atom-text-editor
 atom-text-editor .cursor {
   border-color: red;
 }

 atom-text-editor {
 	.selection .region {
 		background-color: rgba(0,80,120,0.9);
 	}
 }
```

### How to start Atom so that we get a sane command line

Start Atom within a Git bash. Create a batch file (for instance `atom.bat`) with the following contents:
```
start "" "%PROGRAMFILES%\Git\bin\sh.exe" --login -i -c "exec atom"
```
As an alternative, start Atom from the Git Bash by typing `atom`.

## Troubleshooting

When  Atom would not start

When the editor wouldn't run, run this
```
atom --clear-window-state
```
in the command line.
