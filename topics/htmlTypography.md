# Web Typography
[Topics](../README.md)

## Typography Elements

Some elements of typograhpy include:
- Font Family
- Relative Font Sizes (em)
- Indent Style
- Text Alignment
- Vertical Spacing
- Line Length

There are two distinct ways of adding web fonts to your website:
- locally hosted
-externally hosted

### Locally Hosted

1. Download a web font and add it to your project.
2. Embed the web font in your stylesheet.
3. Use the font elsewhwere in your stylesheet.

After downloading the WOFF file, you can embed it into your stylesheet with `@font-face`. These must be at the *top* of the stylesheet

```css
@font-face{
    font-famiy: 'Roboto';
    src: url('Roboto-Light-webfont.woff').form('woff');
}
```
The `font-family` property above defines how we will refer to it later on, so it can be anything. It doesn't need to relate to the official name but it is more intuitive if it does. It is also a good idea to keep it as *generic as possible*.

In order to *Use a web font* you can add the font-family name defined in `@font-face` to your specific element. Ex:

```css
body{
    font-family: 'Roboto', sans-serif; 
    /* other attributes */
}
```

## Font Families and Font Faces

Font Weights (range from 100 - 900):
- 100 Thin
- 200 Extra Light
- 300 Light
- 400 Regular
- 500 Medium
- 600 Semi Bold
- 700 Bold
- 800 Extra Bold
- 900 Black

Font Styles:
- Roman (upright)
- Italic
- Condensed
- Condensed Italic

