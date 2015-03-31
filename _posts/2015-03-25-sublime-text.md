---
layout: post
title: Sublime Text
---

## Resources

* [Perfect Workflow in Sublime Text 2](http://code.tutsplus.com/courses/perfect-workflow-in-sublime-text-2) is a video course with tutorials covering many aspects of Sublime Text 2 and 3.
* [Sublime Text 3 Documentation](http://www.sublimetext.com/docs/3/)
* [Sublime Text Unofficial Documentation](http://docs.sublimetext.info/en/latest/index.html)

## Configuration

`SublimeText/Data/Packages/User/Preferences.sublime-settings`
```json
{
    "color_scheme": "Packages/User/SublimeLinter/Monokai Bright (SL).tmTheme",
    "default_line_ending": "unix",
    "ensure_newline_at_eof_on_save": true,
    "font_size": 12,
    "ignored_packages":
    [
        "Vintage",
        "Markdown"
    ],
    "spell_check": true,
    "trim_trailing_white_space_on_save": true
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

### SublimeLinter

### Markdown Editing
