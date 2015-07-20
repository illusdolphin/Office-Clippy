#  [![NPM version][npm-image]][npm-url] [![Build Status][travis-image]][travis-url] [![Dependency Status][daviddm-image]][daviddm-url]

> A tool to create office documents with JS


# Install

```sh
$ npm install --save office-clippy
```


# Usage

```js
var officeClippy = require('office-clippy');

officeClippy('Rainbow');
```
## Create blank Word Document
```
var file = docx.create();
```

## Create Paragraph
Every text block in OpenXML is organised in paragraphs. You can add more text to the paragraph by doing this:
```
var paragraph = docx.createParagraph();
```
```
var text = docx.createText("Lorem Ipsum Foo Bar");
var paragraph = docx.createParagraph();
paragraph.addText(text);
```
```
var paragraph = docx.createParagraph("Short hand notation for adding text.");
```
### Styles
Styles is a very important part of the look of a word document. At the moment, only headings and title is supported, but son the rest will be supported along with custom styles!

![Word 2013 Styles menu](http://content.gcflearnfree.org/topics/233/style_apply_choose.png "Word 2013 Styles menu")

#### Heading1 - Heading5
```
paragraph.heading1();
paragraph.heading2();
paragraph.heading3();
paragraph.heading4();
paragraph.heading5();
```

#### Title
```
paragraph.title();
```

### Text Alignment
To change the text alignment of a paragraph, for center, left, right or justified:
```
paragraph.center();
```

```
paragraph.left();
```

```
paragraph.right();
```

```
paragraph.justified();
```

#### Example
```
paragraph.heading1().center();
```
The above will create a `heading 1` which is `centered`.

### Thematic Break (Page Break)
To add a break in the page, simply add `.thematicBreak()` on a paragraph:

```
var paragraph = docx.createParagraph("Amazing Heading").heading1().thematicBreak();
```
The above example will create a heading with a page break directly under it.

## Text
Paragraphs need text objects. To create text:
```
var text = docx.createText("My awesome text here for my university dissertation");
```
Text objects have methods inside which changes the way the text is displayed.

### Typographical Emphasis
Soon, strikethrough, overlining, ALL-CAPS, lower case, camelCase, Title Case will be added. At the moment, the standard **bold**, *italics* and underline are avaliable. 

#### Bold
```
text.bold();
```

#### Italics
```
text.italics();
```

#### Underline
```
text.underline();
```

### Break
Sometimes you would want to put text underneath another line of text but inside the same paragraph.
```
text.break();
```

### Chaining
What if you want to create a paragraph which is ***bold*** and ***italic***?
```
paragraph.bold().italic();
```

## Bullet Points
To make a bullet point, simply make a paragraph into a bullet point:
```
var text = docx.createText("Bullet point");
var paragraph = docx.createParagraph(text).bullet();
```

## Tab Stops
If you do not know why tab stops are useful, then I recommend you do a bit of research. It enables side by side text which is nicely laid out without the need for tables, or constantly pressing space bar.

![Word 2013 Tabs](http://www.teachucomp.com/wp-content/uploads/blog-4-22-2015-UsingTabStopsInWord-1024x577.png "Word 2013 Tab Stops")

How it works is that, you create a `tabStop`, then add it to the paragraph. Then just add a `tab()` method call to a text object. Adding multiple `tabStops` will mean you would have to chain `tab()` until the desired `tabStop` is selected. Example is shown below.

### Left Tab Stop
```
var tabStop = docx.createLeftTabStop(2268);
paragraph.addTabStop();
```
2268 is the distance from the left side.

### Center Tab Stop
```
var tabStop = docx.createCenterTabStop(2268);
paragraph.addTabStop();
```
2268 is the distance from the left side.

### Right Tab Stop
```
var tabStop = docx.create\RightTabStop(2268);
paragraph.addTabStop();
```
2268 is the distance from the left side.

### Max Right Tab Stop
```
var tabStop = docx.createMaxRightTabStop();
paragraph.addTabStop();
```
This will create a tab stop on the very edge of the right hand side. Handy for right aligning and left aligning text on the same line.

### Example
```
var tabStop = docx.createMaxRightTabStop();
var paragraph = docx.createParagraph().addTabStop(tabStop);
var leftText = docx.createText("Hey everyone").bold();
var rightText = docx.createText("11th November 2015").tab();
paragraph.addText(leftText);
paragraph.addText(rightText);
```
The example above will create a left aligned text, and a right aligned text on the same line. The laymans approach to this problem would be to either use text boxes or tables. YUK!

```
var tabStop = docx.createMaxRightTabStop();
var tabStop2 = docx.createLeftTabStop(1000);
var paragraph = docx.createParagraph();
paragraph.addTabStop(tabStop);
paragraph.addTabStop(tabStop2);
var text = docx.createText("Second tab stop here I come!").tab().tab();
paragraph.addText(text);
```
The above shows the use of two tab stops, and how to select/use it.

# Examples
The following section:
```
var paragraph = docx.createParagraph("Hello World");
paragraph.addText("Lorem Ipsum foo bar");
paragraph.italics();
paragraph.bold();
```

Or:
```
var paragraph = docx.createParagraph("Hello World");
paragraph.addText("Lorem Ipsum foo bar");
paragraph.italics().bold();
```
Would produce:

***Hello World***

***Lorem Ipsum foo bar***

# License

MIT © [Dolan Miu](http://dolan.bio)


[npm-image]: https://badge.fury.io/js/office-clippy.svg
[npm-url]: https://npmjs.org/package/office-clippy
[travis-image]: https://travis-ci.org/dolanmiu/office-clippy.svg?branch=master
[travis-url]: https://travis-ci.org/dolanmiu/office-clippy
[daviddm-image]: https://david-dm.org/dolanmiu/office-clippy.svg?theme=shields.io
[daviddm-url]: https://david-dm.org/dolanmiu/office-clippy
