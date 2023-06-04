# ao3-bootstrap-workskin

This is an AO3 (An Archive of Our Own) workskin using a modified version of [Bootstrap's 3.4.1 CSS grid system](https://getbootstrap.com/docs/3.4/css/#grid). This work skin provides a 12-column layout for AO3 works with complex typographical needs, as well as some alignment tools and basic text transformations. Reviewing the Bootstrap documentation will give a good sense of what this code does, but there are some deviations to keep in mind.

## Getting Started 
You are welcome to clone this repo, but the simplest way to apply this work skin is to simply copy the contents of the *modified-bootstrap.css* file into the CSS box when creating a new work skin. For creating a new work skin, [AO3 has a tutorial available on its site](https://archiveofourown.org/admin_posts/1370).

Once you have your work skin installed and selected, you'll want to format it for columns using AO3's **HTML** editor. This work skin cannot be used in Rich Text mode.

## Applying Classes
This work skin is *class-based*, which means that all styles will be applied via CSS class. Classes are applied to HTML elements via the **class** keyword. For instance, a work skin with the following classes

```CSS
.text-center {
  text-align: center;
 }
 .text-sm {
  font-size: 0.75rem;
 }
 ```
 Would be applied to HTML thus:
 
 ```HTML
<p class="text-center text-sm">This is your content</p>
```
The above text would be center-aligned and the text would be smaller. You can apply a (theoretically) infinite number of classes to a given HTML element by including a space between each class name. For further explanation, see [MDN's guide on CSS classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Class_selectors).

## Using the Grid
Because of the quirks of how AO3 processes text, using this grid work skin differs somewhat from the standard boostrap framework. The basic structure of your page should look something like this:
```HTML
<div class="container"> <!-- The entire body of your work should be wrapped in a <div> with a class of "container" -->
  <div class="row"> <!-- Rows should posses column elements that add up to 12 or less -->
    <p class="col-6">A column that takes up half of the horizontal space</p> <!-- Every column should be within a <p> tag, not a <div> -->
    <p class="col-offset-4 col-2">A column that takes up the rightmost 1/6 of horizontal space on the same line</p>
  </div>
</div>
```
Please keep the following in mind:
- A `<div>` with a class of `container` should wrap the entirety of your chapter
- The `row` class should only be applied to a `<div>` tag
- Conversely, all `col` classes should be applied to `<p>` tags only. Because of the way AO3 auto-formats HTML, you'll get odd spacing if you try to use columns with anything other than the `<p>` tag.
- Each `row` class should have an amount of columns adding up to 12 or less. For instance, in the above example, there's a `<p class="col-6">`, so a `<p>` that spans 6 columns, and then a `<p class="col-offset-4 col-2">`, a `<p>` that is offset by 4 (so 4 columns of empty space) and then content that spans 2 colums. So 6 + 4 + 2 = 12. If you have more than 12 columns in a row, the contents will wrap to the next line and may behave erratically.

### Limitations
Unlike the original Bootstrap, this work skin does not support mobile devices, because AO3 does not support media queries in its work skins. This means that if you have a lot of text in very narrow columns, it may be difficult to read on mobile devices.

If you are having trouble with AO3 not respecting intra-line spacing, you can toggle to the Rich Text editor and use the space bar, or HTML-encode your spaces by replacing them with the `&nbsp;` character. For instance, if you wanted to preserve the 5 spaces between "Hello" and "World" below:

```
Hello     World!
```
You would replace those spaces with 5 `&nbsp;` characters:
```
Hello&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;World!
```
You can usually find + replace spaces using your word processor by replacing a single " " character with the `&nbsp;` tag rather than doing it manually. You can also [read more about other intra-line spacing options here](https://www.freecodecamp.org/news/html-space-how-to-add-a-non-breaking-space-with-the-nbsp-character-entity/).

## Using the Text Utilities
This work skin has several basic class utilities that deal with alignment, capitalization, font size, and font color.

### Alignment
The alignment utilities make use of the CSS [text-align](https://developer.mozilla.org/en-US/docs/Web/CSS/text-align) property. These utilities will likely only work properly when applies to `<p>` tags with text inside.

- `text-left` will align text to the left. This is AO3's default.
- `text-right` will align text to the right.
- `text-center` will align text in the center.
- `text-justify` will justify text.

### Capitalization
The capitalization utilities make use of the CSS [text-transform](https://developer.mozilla.org/en-US/docs/Web/CSS/text-transform) property.

- `text-uppercase` will make all text uppercase, regardless of how it was typed in.
- `text-lowercase` will make all text lowercase, regardless of how it was typed in.
- `text-capitalize` will capitalize the first letter of every word. If a word is already capitalized, it will not make the rest of the word lowercase. It also will capitalize words not typically capitalized in title case, such as "the" and "or."

### Font Size
The font size utilities make use of the CSS [font-size](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size) property. All font sizes are specified in `rem`, where 1`rem` is equal to the browser's default font size. If you modify these font sizes, it's recommended to stil with a relative calculation for accessibility, instead of `px`, which don't scale as nicely.

- `text-xs` is an extra-small font. This font may be functionally useless.
- `text-sm` is a small font.
- `text-md` is a medium font. This should be the same size as the default AO3 font.
- `text-lg` is a slightly larger font.
- `text-xl` is the largest font.

These utilities are for use with body text. If you want a large header, it's recommended that you use HTML section heading tags such as `<h1>`, `<h2>`, `<h3>`, &c. ([section header reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements)).

### Font Color
The font color utilities make use of the CSS [color](https://developer.mozilla.org/en-US/docs/Web/CSS/color) property. Right now there are only two font colors available: 

- `text-red`, which is hex code `#C82E23`
- `text-blue`, which is hex code `#6FA8DC`

Text colors are easy to add. You'll just want to add a rule to your work skin like so:

```CSS
.text-[color-name] {
  color: [color-code];
}
```
Where `[color-name]` is whatever you want to name the color and `[color-code]` is a web. I personally like the [W3Schools HTML Color Picker](https://www.w3schools.com/colors/colors_picker.asp). For the different ways you can specify color, [MDN has a useful piece here](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_colors/Applying_color#how_to_describe_a_color).

Please note that CSS rules (that's the `.text-red` bit) cannot contain spaces!

## Block-level & Inline Elements
Most of the tags we've discussed, such as `<p>` and `<div>`, are what we call "block-level elements, which means they always take up a block of vertical space. It's easiest to think of them as paragraphs. However, you may want to apply any of the above text utilities (except alignment) to a line of text or a single word. In that case, you'll want to use an inline element. If you're at all familiar with HTML, you might've encountered the inline elements `<i>` or `<em>` for italics, or `<b>` or `<strong>` for bold. You can add classes to those tags. So, for instance, if you want your italicised text to also be red, you could do something like:

```HTML
<p>I really <em class="text-red">want to emphasize this</em>!</p>
```
However, if you don't want text to be bold or italics, just say small and blue, you'll want to use the `<span>` tag.
```HTML
<p>I want <span class="text-blue text-sm">this text to be a little quieter</span>.</p>
```
`<span>` doesn't apply any additional styles, so it's perfect for text you just want to modify with the classes in the work skin. Also, if my explanation of block and inline elements didn't make total sense, feel free to check out [W3Schools' much better explanation](https://www.w3schools.com/html/html_blocks.asp) if that didn't make sense.

## Conclusion
If you're going to be making extensive use of this system, I suggest downloading a free code editor like [Notepad++](https://notepad-plus-plus.org/downloads/) or [Visual Studio Code](https://code.visualstudio.com/), as an editor will help you keep track of your HTML tags and add contextual highlighting to your classes. Of course, do what's easiest for you.

Feel free to modify this skin however you see fit, and if you find any bugs feel free to reach out to me or shoot a PR my way.
