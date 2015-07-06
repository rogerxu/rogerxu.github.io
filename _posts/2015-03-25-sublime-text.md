---
layout: post
title: Sublime Text
---

## Resources

* [Perfect Workflow in Sublime Text 2](http://code.tutsplus.com/courses/perfect-workflow-in-sublime-text-2) is a video course with tutorials covering many aspects of Sublime Text 2 and 3.
* [Sublime Text 3 Documentation](http://www.sublimetext.com/docs/3/)
* [Sublime Text Unofficial Documentation](http://docs.sublimetext.info/en/latest/index.html)

## Configuration

`/Packages/User/Preferences.sublime-settings`

```json
{
    "color_scheme": "Packages/User/SublimeLinter/Monokai Bright (SL).tmTheme",
    "default_encoding": "UTF-8",
    "default_line_ending": "unix",
    "draw_indent_guides": true,
    "draw_white_space": "all",
    "ensure_newline_at_eof_on_save": true,
    "font_size": 12,
    "highlight_line": false,
    "highlight_modified_tabs": true,
    "hot_exit": true,
    "ignored_packages":
    [
        "Vintage",
        "Markdown"
    ],
    "preview_on_click": true,
    "shift_tab_unindent": true,
    "show_encoding": true,
    "show_line_endings": true,
    "spell_check": true,
    "tab_size": 4,
    "translate_tabs_to_spaces": false,
    "trim_automatic_white_space": true,
    "trim_trailing_white_space_on_save": true,
    "use_tab_stops": true
}
```

## Usage

### General

* `Ctrl+Shift+P` - Open Command Palette
* ``Ctrl+` `` - Open Console
* `Ctrl+KB` - Toggle side bar

### Edit

Copy Paste

* `Ctrl+C` - Copy current line
* `Ctrl+X` - Cut current line
* `Ctrl+Shift+V` - Paste and indent correctly

Insert

* `Ctrl+Enter` - Insert line after
* `Ctrl+Shift+Enter` - Insert line before
* `Ctrl+Shift+D` - Duplicate line.

Delete

* `Ctrl+Shift+K` - Delete line
* `Ctrl+KK` - Delete from cursor to end of line
* `Ctrl+K+Backspace` - Delete from cursor to start of line


### Selection

* `Ctrl+D` - Expand Selection to Word
* `Ctrl+L` - Expand Selection to Line
* `Ctrl+M` - Expand Selection to matching bracket.
* `Ctrl+Shift+M` - Select all contents of the current brackets.
* `Right Mouse Button + Shift` or `Middle Mouse Button` - Column selection.

### Conversion

* `Ctrl+KU` - Upper case
* `Ctrl+KL` - Lower case

### Find

* `Ctrl+I` - Incremental Find
* `Ctrl+F3` - Quick Find
* `Alt+F3` - Quick Find All

### Bookmark

* `Ctrl+F2` - Toggle bookmarks
* `F2` - Next bookmark
* `Shift+F2` - Previous bookmark
* `Ctrl+Shift+F2` - Clear bookmarks

### Navigation

* `Ctrl+P` - Open file by name in the project
* `Ctrl+R` - Goto symbol in the file. (`Ctrl+P` with `@`)
* `Ctrl+;` - Goto word in current file. (`Ctrl+P` with `#`)
* `Ctrl+G` - Goto line in current file. (`Ctrl+P` with `:`)


## Project

`abc.sublime-project`

```json
{
    "folders":
    [
        {
            "name": "webapp",
            "path": "./src/main/webapp",
            "folder_exclude_patterns": ["target"],
            "file_include_patterns": ["*.*"]
        }
    ]
}

```

## Package Control

[Package Control - Installation](https://packagecontrol.io/installation)

### Emmet

### SublimeLinter

### MarkdownEditing

### AdvancedNewFile

### SideBarEnhancements

### SyncedSideBar

### Generic Config

### BracketHighlighter

### Find++

`/Packages/User/Default.sublime-keymap`

```json
[
    { "keys": ["f5"], "command": "fpp_find_in_current_file" },
    { "keys": ["f8"], "command": "fpp_find_in_current_folder" },
    { "keys": ["f10"], "command": "show_panel", "args": {"panel": "find_in_files", "where": "<project>"} },
    { "keys": ["ctrl+alt+f5"], "command": "fpp_show_results_panel" }
]
```

### SublimeCodeIntel

### SublimeBookmark

### Alignment

### DocBlockr

### JsFormat

### Random Everything





