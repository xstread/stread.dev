---
title: "Markdown Cheatsheet"
date: '2025-07-07T20:01:32+03:00'
categories: ["cheatsheets", "web-development"]
tags: ["markdown"]
---

# Markdown Cheatsheet

## Headers

```markdown
# H1
## H2
### H3
#### H4
##### H5
###### H6
```

## Emphasis

```markdown
*italic* or _italic_
**bold** or __bold__
**_bold and italic_**
~~strikethrough~~
```

## Lists

### Unordered

```markdown
- Item 1
- Item 2
  - Item 2a
  - Item 2b
```

### Ordered

```markdown
1. Item 1
2. Item 2
3. Item 3
   1. Item 3a
   2. Item 3b
```

## Links

```markdown
[Inline Link](https://www.example.com)
[Link with Title](https://www.example.com "Title")
```

## Images

```markdown
![Alt Text](url/to/image.jpg)
![Alt Text](url/to/image.jpg "Optional Title")
```

## Code

Inline code: `code`

Code blocks:
````markdown
```
function test() {
  console.log("Hello world!");
}
```
````

Syntax highlighting:
````markdown
```javascript
function test() {
  console.log("Hello world!");
}
```
````

## Blockquotes

```markdown
> This is a blockquote
> 
> > Nested blockquote
```

## Horizontal Rule

```markdown
---
***
___
```

## Tables

```markdown
| Header 1 | Header 2 | Header 3 |
|----------|----------|----------|
| Cell 1   | Cell 2   | Cell 3   |
| Cell 4   | Cell 5   | Cell 6   |
```

## Footnotes

```markdown
Here's a sentence with a footnote.[^1]

[^1]: This is the footnote.
```

## Task Lists

```markdown
- [x] Completed task
- [ ] Incomplete task
``` 