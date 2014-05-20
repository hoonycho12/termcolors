# TermColors

> Import and export between multiple terminal colour scheme formats

Many templates are sourced from the
[Base16-Builder](https://github.com/chriskempson/base16-builder).

Colors are handled using
[tinytinycolor](https://www.npmjs.org/package/tinytinycolor).

## Installation

```
npm install --save termcolors
```

## Usage

```javascript
var fs = require('fs');
var termcolors = require('termcolors');

var xresources = fs.readFileSync('~/.Xresources', 'utf8');
var colors = termcolors.xresources.import(xresources);

var iterm = termcolors.iterm.export(colors);
fs.writeFile('~/config.itermcolors', iterm);
```

## Supported Formats

Only some formats support importing.

**Gnome**

- `gnome`
- Export

**Guake**

- `guake`
- Export

**iTerm2**

- `iterm`
- Import
- Export

**Konsole**

- `konsole`
- Export

**MinTTY**

- `mintty`
- Export

**Putty**

- `putty`
- Export

**Terminator**

- `terminator`
- Export

**Termite**

- `termite`
- Import
- Export

**XFCE4 Terminal**

- `xfce`
- Export

**Xresources**

- `xresources`
- Import
- Export

## DIY Export

Templates use [doT.js](http://olado.github.io/doT/index.html).

Check the `templates` folder for some examples.

**Usage:**

`termcolors.create.export(template, [transformer])`

- template (string)
- [transformer] (function)

The transformer is an optional function that is passed the colors input into
the template and can transform them for use in the template.

This is useful so that you don't have to use the tinycolor 

**Example Without Converter:**

```javascript
var template = 'body { background {{=c.background.toHexString()}}; }'

var cssTemplate = termcolors.create.export(template);
```

**Example With Converter:**

```javascript
var template = 'body { background: {{=c.background}}; }'

var toHex = function (colors) {
    return {
        background: colors.background.toHexString();
    }
};

var cssTemplate = termcolors.create.export(template, toHex);
```


**Example With LoDash.paLoDash.mapValues Converter:**

```javascript
var _ = require('lodash');
var template = 'body { backgdround: {{=c.background}}; }'

var toHex = _.partialRight(_.mapValues, function (color) {
    return color.toHexString();
});

var cssTemplate = termcolors.create.export(template, toHex);
```
