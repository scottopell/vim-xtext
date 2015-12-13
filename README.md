# Vim Xtext
Generates a vim plugin from a given xtext language giving
- validation
- code completion
- code formatting
- (basic) syntax highlighting

## Usage:
Edit the mwe2 file for your language to include a segment like this:
```xtend
fragment = GenerateVim {
  absolutePath = '/Users/scott/vim_xtext/'
  override = true
}
```
and then add the `GenerateVim.xtend` file from this repo alongside your mwe2
generator file.


You can find the vim plugin at the path you specified above and from here you
can either copy it into your `.vim` folder or you can put it in your `code`
folder (or any arbitrary location) and then link to it with a package manager
(recommended.)

For instructions on adding a local vim plugin, see your plugin manager's
documentation (vundle, plug, pathogen etc.)

For Plug you'd do something like this:
```vim
Plug '~/code/FOA/vim-statemachine'
```

## What it does

### Validation
This generates you a vim plugin that will setup a `compiler` allowing you access
to `:make` and quickfix (`:help quickfix`). In addition, if you have syntastic
installed then it will also show you errors inline as you edit your file
(activated on file save.)

### Completion
This gives you the capability to get intellisense style suggestions at any point
with the standard omnifunc completion (`:help complete`).

Activate it at any point by hitting `ctrl-x ctrl-o` (ctrl + x followed quickly by
ctrl-o) and you'll get a list of suggestions to choose from.

### Formatting
This sets both the `indentprg` and `formatprg` to a code formatter, so you can use
either the `=` key or the code formatting (\<motion\>q) hotkeys.


## Output
Here is an example output of the directory tree it will generate:

```
      1 .
      2 ├── autoload
      3 │   └── MyDsl.vim
      4 ├── compiler
      5 │   └── MyDsl.vim
      6 ├── ftdetect
      7 │   └── ftaccess.vim
      8 ├── ftplugin
      9 │   └── MyDsl.vim
     10 ├── syntax
     11 │   └── MyDsl.vim
     12 ├── syntax_checkers
     13 │   └── MyDsl
     14 │       └── MyDsl.vim
     15 ├── completer.rb
     16 ├── formatter.rb
     17 └── validator.rb
     18
     19 7 directories, 9 files
```

## Dependencies
Currently this has a dependency on ruby and a modern version of vim (7.x should
be fine, tested on 7.4.x)

It also requires the xtext web integration server to be running.

`./gradlew jettyRun`

## TODO
There is a syntax highlighting file generated, but its not complete.
More investigation needs to be done in how to link the vim syntax groups with
the current xtext language's syntax groups.
