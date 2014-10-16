# Sassy Pygments

16-color syntax highlighting styles for Pygments and Rouge. Inspired by [Base16 project](https://github.com/chriskempson/base16-builder/).

Based on [this gist](https://gist.github.com/D-side/3054ce947676bd621ce6) (which quickly reveals itself to be a fork).

It's initially designed for use as a git submodule for [Jekyll](http://jekyllrb.com/) websites, just include it where you want it to be and you should be all set.

### Quick start

Copy the contents of this repository to a path accessible to Sass you are using. In Jekyll this is by default `_sass` and you may want a subfolder for this stuff. Let's assume it's `syntax`.

```sass
@import "syntax/begin" // Defines default colors
@import "syntax/end"  // Processes templates and outputs the result
```

This will load working defaults: a **dark Solarized theme**. But since you decided to use this thing, you might want something different, right?

```sass
@import "syntax/begin"
// This file contains defaults
// If you define them all, you don't need it

$syntaxfont: monospace
// You can change the font for your code, obviously

$sample: #042 // Because 42. Don't ask why.
$variation: 30deg
// Parameters for "mix" group of color schemes
// Required if they are used, otherwise not needed

@import "syntax/themes/mix/near"
// A color scheme that composes its 16 colors based
// on a sample and variation along the colorwheel

@import "syntax/inverse"
// Flip the first 8 colors of the theme (monotones)
// It effectively makes a dark base16 theme light
// and vice versa

// Finish up and build a theme
@import "syntax/end"
```

Comments make it bulkier than it actually is.  


```sass
@import "syntax/begin"
$syntaxfont: monospace
$sample: #042
$variation: 30deg
@import "syntax/themes/mix/near"
@import "syntax/inverse"
@import "syntax/end"
```

Not using a `mix`-type theme makes it even shorter:

```sass
@import "syntax/begin"
$syntaxfont: monospace
@import "syntax/themes/base16/ocean"
@import "syntax/inverse"
@import "syntax/end"
```

Once you are done, extend your code container (could be `pre`, or `.highlight` or whatever) with `%sassy-pygments`:

```sass
.highlight
  @extend %sassy-pygments
```

And it should be working!

### Theme definition

A theme is, basically, a Sass file with 16 variables exposed to the outside world. Variables' names are based on hexadecimal digits and look like: `$theme0X` where `X` is replaced by a hexadecimal digit, `0` to `F` (`A` to `F` are capitals, that's important).

As in `base16`, colors `$theme00` to `$theme07` are monotones: slight variations of a color ordered by brightness. Themes I keep here define colors with ascenting brightness, i. e. `$theme00` is the darkest, `$theme07` is the brightest. An `inverse` file, when imported, reverses that order if you need it.

Again, as in `base16`, the rest (`$theme08` to `$theme0F`) are accents. Most of the time (however, many themes fail to maintain that) they should all be legible on "edge" monotones, either bright and dark, such as 0-1 and 6-7 because keeping them legible with all the monotones is next to impossible. You could try though.

You are free to use the colors defined in a syntax theme elsewhere. You could, like me, build your entire design around it and bend the look and feel at will.

### `mix` themes

An experiment about generating color schemes. Inspired by Grayscale from `base16`, that defines a decent color scheme with shades of gray only. What if we don't have gray, but rather... cyan? Or violet? Or whatever else?

Importing one of them would require a `$sample` variable set to a color you want. The resulting scheme will inherit hue and saturation from it. Some schemes also require `$variation` of hue along the colorwheel, in degrees.
