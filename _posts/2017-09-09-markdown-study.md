---
layout: post
title: markdown study
description: "markdown study"
modified: 2017-09-09
tags: [markdown]
categories: [etc]
---

# Markdown title

`# Markdown title`

## Heading

`## Heading`

**Bold text**

`**Bold text**`

Plain text
`Plain text`


- List item1
- List item1

```markdown
- List item1
- List item1
````


> dsdsdfsdfsdfsdfsdf
>
> sdfsdfsdfsdfsdfsdf

```markdown
> dsdsdfsdfsdfsdfsdf
>
> sdfsdfsdfsdfsdfsdf
```

sdfsdfs
sdfs
```
> sdsd
```

### table

table | head | item 
|---|---|---|
content1|content2|content3

```markdown
table | head | item 
---|---|---
content1|content2|content3
```

# Hello Markdown

## Examples 

### Text

It's very easu to make some word **bold** and
other words *italic* woth Markdown. you can even 
[link to Google!](http://google.com)

```markdown
It's very easu to make some word **bold** and
other words *italic* woth Markdown. you can even 
[link to Google!](http://google.com)
```

### Lists

**sometimes you want numbered lists:**

1. One
2. Two
3. Three

**sometomes you wnat buller points:**

* Start aline with a srar
* profit!

**Alternatively,**

- Dashes work just as well
- and if you have sub points, put two spaces before the dash or star:

	- Like this 
    - And this
    
```markdown
**sometimes you want numbered lists:**

1. One
2. Two
3. Three

**sometomes you wnat buller points:**

* Start aline with a srar
* profit!

**Alternatively,**

- Dashes work just as well
- and if you have sub points, put two spaces before the dash or star:

    - Like this 
    - And this
```

### Images

**If you wnat to embed images, this is how you do it:**

![image of Yakocat](https://octodex.github.com/images/yaktocat.png)

```markdown
**If you wnat to embed images, this is how you do it:**

![image of Yakocat](https://octodex.github.com/images/yaktocat.png)
```

### Headers & Quotes

# Structured documents

sometimes it's useful to have different levels of headings to structure your documens. Start lines with a `#` to create headings. Multiple `##` in a row denot smaller heading sizes.

### This is a third-tier heading

you can use one `#` all the way up tp `#####` six for different heading sizes.

If you'd like to quote someone, use the >
character bofore the line:

> Cofee. the finest organic suspension ever devised... I beat the Borf with it.
> -Caprain Janeway


# Code

There are manu dofferent ways to style code woth GotHub's markdown. Ig you have inline code blocks, wrap them in backticks: `var example = true`. if you've got a linger block of code, you can indent with four spaces:

```
if (isAwesome){
	return true
}

```

GitHub also surppors somethinf called code fenconf, whoch allows for multiple lines wirhour indenrarion:

```
if (isAwesome){
	return true
}
```

And if you'd like to use sytax ifhlighrinf, include the language:

```javascript

if (isAwesome){
	return true
}
```

```javascript

  if (isAwesome){
      return true
  }
```


### Extras

GitHub supports many extras in Markdown that help you reference and link to people. If you can prefix their name with an @symbol: hey @kneath - lone your sweater!

but I have to admit, tasks lists are my favorite:

- [x] This is a complete item
- [ ] This is an incomplete item

When you include a task list in the first c,,enr of an Issue, you list of issues. It works in Pull Rquests, too!

And, of course emoji! 
:sparkles: :camel: :boom: :smile: :cry: :cat: :heart: :memo:


# Syntax guide

Here’s an overview of Markdown syntax that you can use anywhere on GitHub.com or in your own text files.

## Headers

```
# This is an <h1> tag
## This is an <h2> tag
###### This is an <h6> tag
```

## Emphasis

*This text will be italic*
_This will also be italic_

**This text will be bold**
__This will also be bold__

_You **can** com**bine** them_

```markdown
*This text will be italic*
_This will also be italic_

**This text will be bold**
__This will also be bold__

_You **can** com**bine** them_
```

## Lists

### Undordered

* Items1
* Items2

	* Item 2a
	* Item 2b


### Ordered

1. Item 1
3. Item 2
1. Item 3
   1.Items 3a
   1.Items 3b

1. Fist list item in first line.
	- First nested list item
	- second nested list item
	
```markdown
1. Item 1
3. Item 2
1. Item 3
   1.Items 3a
   1.Items 3b

1. Fist list item in first line.
	- First nested list item
	- second nested list item
```
## Images

![GitHub Logo](///Users/janggunhee/Documents/md-file/images/logo.png)
Format URL: ![GitHub Logo](https://assets-cdn.github.com/images/modules/open_graph/github-mark.png)

```markdown
![GitHub Logo](///Users/janggunhee/Documents/md-file/images/logo.png)
Format URL: ![GitHub Logo](https://assets-cdn.github.com/images/modules/open_graph/github-mark.png)

```


## Links

https://www.meetup.com/ko-KR/ -automatic!

[Meet Up](https://www.meetup.com/ko-KR/)

[Meet UP](https://secure.meetupstatic.com/s/img/286374644891845767035/logo/meetup-logo-script-1200x630.png)

![Meet Up](https://secure.meetupstatic.com/s/img/286374644891845767035/logo/meetup-logo-script-1200x630.png)

```markdown
[Meet Up](https://www.meetup.com/ko-KR/)

[Meet UP](https://secure.meetupstatic.com/s/img/286374644891845767035/logo/meetup-logo-script-1200x630.png)

![Meet Up](https://secure.meetupstatic.com/s/img/286374644891845767035/logo/meetup-logo-script-1200x630.png)
```
## Blockquotes 

As Kanye West said:

> we;re living the future so
>> the present is our past.
>>> The end
>>>> fuck off !!



## Inline code 

I think you should use an 
`<addr>` element here instead




# GitHub.com uses its own version of the Mardown

**GitHub.com uses its own version of the Markdown syntax that provides an additional set of useful features, many of which make it easier to work with content on GitHub.com.**

**Note that some features of GitHub Flavored Markdown are only available in the descriptions and comments of Issues and Pull Requests. These include @mentions as well as references to SHA-1 hashes, Issues, and Pull Requests. Task Lists are also available in Gist comments and in Gist Markdown files.**


## Syntax highlighting

**Here's an example of how you can use syntax highlightinf with** [GitHub Flavored Mardown](https://help.github.com/articles/basic-writing-and-formatting-syntax/):

```javascropt
function fancyAlert(arg) {
	if(arg) {
    	$.facebox({div:'#foo'})
    }
 }
```
```markdown
    ```javascropt
    function fancyAlert(arg) {
        if(arg) {
            $.facebox({div:'#foo'})
        }
     }
    ```
```

**You can also simply indent your code by four spaces:**


```
    function fancyAlert(arg) {
      if(arg) {
        $.facebox({div:'#foo'})
      }
    }
```
    
**Here’s an example of Python code without syntax highlighting:**


```python
def foo():
	if not bar:
    	return True
```
```markdown
    ```python
    def foo():
        if not bar:
            return True
    ```
```

## Task Lists

- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported
- [x] list syntax required (any unordered or ordered list supported)
- [x] this is a complete item
- [ ] this is an incomplete item

```markdown
- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported
- [x] list syntax required (any unordered or ordered list supported)
- [x] this is a complete item
- [ ] this is an incomplete item
```


## Tables 

**You can dreate tables by assembling alist of words and dividing them with hyphen`-`(for the first row), and then separatinf each column with a pip`|`:

```
First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column

```
Would become:

First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column

## SHA references 

**Any reference to a commit’s [SHA-1 hash](https://en.wikipedia.org/wiki/SHA-1) will be automatically converted into a link to that commit on GitHub.**


16c999e8c71134401a78d4d46435517b2271d6ac
mojombo@16c999e8c71134401a78d4d46435517b2271d6ac
mojombo/github-flavored-markdown@16c999e8c71134401a78d4d46435517b2271d6ac

## Issue references within a repository

**Any number that refers to an Issue or Pull Request will be automatically converted into a link.**

```
#1	
'mojombo#1
mojombo/github-flavored-markdown#1
```

## Username @mentions

Typing an `@ `symbol, followed by a username, will notify that person to come and view the comment. This is called an “@mention”, because you’re mentioning the individual. You can also @mention teams within an organization.

## Automatic linling for URLs

Any URL (like `http://www.github.com/`) will be automatically converted into a clickable link.

[git hub: (http://www.github.com/)](http://www.github.com/)

[http://www.github.com/](http://www.github.com/)

```markdown
[git hub: (http://www.github.com/)](http://www.github.com/)

[http://www.github.com/](http://www.github.com/)
```


## Strikethrough

Any word wrapped with two tildes (like `~~this~~`) will appear crossed out.

~~sdsfsd~~

~~ㄴㅇㄴㄹㅇㅎㄴㅎㄴㅇㅎㄴㅇㅎ~~

```markdown
~~sdsfsd~~

~~ㄴㅇㄴㄹㅇㅎㄴㅎㄴㅇㅎㄴㅇㅎ~~
```

## Emoji

GitHub supports emoji! 

:sparkles: :camel: :boom:

```markdown
:sparkles: :camel: :boom:
```