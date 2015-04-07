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

* `Ctrl+Shift+P` - Open Command Palette.
* ``Ctrl+` `` - Open Console.

### Edit

Line

* `Ctrl+Shift+K` - Delete Line.
* `Ctrl+Shift+D` - Duplicate Line.

### Selection

* `Ctrl+D` - Expand Selection to Word
* `Ctrl+L` - Expand Selection to Line

### Find

* `Ctrl+I` - Incremental Find
* `Ctrl+F3` - Quick Find
* `Alt+F3` - Quick Find All

### Bookmark

* `Ctrl+F2` - Toggle Bookmarks
* `Ctrl+Shift+F2` - Clear Bookmarks

### Navigation

* `Ctrl+P` - Goto Anything

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





