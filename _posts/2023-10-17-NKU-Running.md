---
title: NKU Running
commentable: true
Edit: 2023-10-17
mathjax: true
mermaid: true
tags: nku-running
categories: Markdown
description: This is about Nankai University's 104th Anniversary Running Event, hosted by **NKRunning Club** and **NKU SMS**.
---

# Careful!

<figure class="half">
    <img src="https://ssskz.github.io/about/Run_1.jpg"/>
    <img src="https://ssskz.github.io/about/Run_2.jpg"/>
</figure>

# Highlights

*This is italic.* **This is Bold**. * If asterisk is surrounded by spaces, it is not parsed. *

_This is also italic._ __This is also Bold__. _ If underscore is surrounded by spaces, it is not parsed. _

~~This is strike through~~. 

There is no underline in markdown. You can use html tags <u>like this to underline.</u>

`This is a code block`. 

[This is an external link](https://bit.ly). "https://" is important. This is an internal [link](#this-is-a-h2). Internal links are all lowercase with space replaced by hyphens "-". 

You can mix them like [*this*](https://bit.ly), [`this`](https://bit.ly), **[this](https://bit.ly)**, but not like `[this](https://bit.ly)`.

# Blocks

> This is a quote block
>
> > This is a quote block in side another

```python
 import numpy as np
 print("""This is a python code fence""")
```

```fortran
 "This is a fortran code fence"
 implicit none
```

```
 This is a simple code fence. You can use it to display text. The fonts are mono spaced.
```

You can mix them as well, like 

> ```
>  This
> ```

# Other Elements

This is horizontal line

------

# Lists

- This is unordered list
  - sub item
    - subsub item
      - subsubsub item
        - subsubsubsub ...

------

- List can have multiple lines

  like this.

------

1. This ordered list
   1. sub item
2. This is as well
3. It can keep going

------

1. You can avoid numbers like this
   1. sub item
1. It keeps going
1. Blah Blah


# Tables

| This column is left aligned | This column is centered | This column is right aligned |
| :-------------------------- | :---------------------: | ---------------------------: |
| 1                           |            4            |                            7 |
| 2                           |            5            |                            8 |
| 3                           |            6            |                            9 |

| You can use `![caption](link)` in tables.                    | You can use Math in tables. | You can use `<img src="" width="">` in tables.               |
| ------------------------------------------------------------ | --------------------------- | ------------------------------------------------------------ |
| ![caption](https://raw.githubusercontent.com/yk-liu/yk-liu.github.io/master/_posts/2018-11-01-Introduction-to-Homology/assets/triangles.png) | $1+1=2$                     | <img src="https://raw.githubusercontent.com/yk-liu/yk-liu.github.io/master/_posts/2018-11-01-Introduction-to-Homology/assets/triangles.png" width="30%"> |

# Foot Notes

This is a note[^1]. Footnotes can have captions like[^this]. You can reference to the same note multiple times like[^this]. Foot notes can have many other options like[^this-one]. Or just like [^that]. This is a [reference style link][linkid] to a page. And [this][linkid] is also a link. As is [this][] and [that].

# Titles

# This is  h1

## This is  h2

### This is  h3

#### This is  h4

# Foot Notes

The Foot notes are like this

[^1]: https://ssskz.github.io
[^this]: https://ssskz.github.io
[^this-one]: 

```
> Blockquotes can be in a footnote.
```

```
    as well as code blocks
```

[^that]: or, naturally, simple paragraphs.

[linkid]: https://ssskz.github.io	"Optional Title"
