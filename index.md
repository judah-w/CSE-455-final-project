# QuickDraw x Yolo

## Problem Summary

Our project does not necessarily solve a problem, however it is more of a fun/creative idea revolving around drawing/art. Similar to the Google Draw website found [here](https://quickdraw.withgoogle.com), our program/idea will, at its root, do the same thing. However, unlike Google Draw, our project will be able to  analyze multiple sketches within a single image. Currently the website looks for a single drawing. For example, if it wants a cat and I draw an apple in one corner and draw a cat in the middle, the AI doesn’t recognize that we’re drawing a cat no matter how well I draw it because it has noise from the corner image of an apple that it tries to consider as well. From here, we want to convert these images to an actual image of that sketch of relatively the same size in a new image. For example if we draw a tree and a cat sitting below the tree, the program would identify that there’s a tree and a cat in the image, then put labeled bounding boxes around them (saving pixel locations of the box) and then use machine learning to replace the image with an emoji of that label.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/judah-w/CSE-455-final-project/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
