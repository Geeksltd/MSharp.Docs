# Contributing guidelines

When contributing to this repository, please first discuss the change you wish to make via [issue](https://github.com/Geeksltd/MSharp.Docs/issues),
email, or any other method with the lead contributors of this repository before making a change. Also if there was any change that did not require out notice, feel free and make a PR.

## Pull Request Process

1. First make sure that you have read this document FULLY and you follow our writing styles.
2. Better to contact lead contributors about the changes
3. Include documentation information in [README.md](README.md) and [Docksify sidebar](_sidebar.md) if necessary
4. Fully write abut the changes you made and the reason if necessary in your commit/PR message.

Your PR will be reviewed by lead contributors and will be edited if necessary

## How you can help us

- Tip us good technical writing practices
- Fix or report any kind of typo or content mistakes
- Add new content and tutorial about M# (Make sure you contact us before making any new thing or a major change)

### Documentation source

Currently we are porting [old legacy M# documents](http://msharp.co.uk/Learn/Understanding-MSharp.html) to a [brand new](https://learn.msharp.co.uk/) and [open](https://github.com/Geeksltd/MSharp.Docs) documentation style.

Our next priorities are [issue](https://github.com/Geeksltd/MSharp.Docs/issues) and improvements and also **new M# features**.

> **Note:** Documentation about Olive framework (or in another words M# framework) are [HERE](https://geeksltd.github.io/Olive/).

## Writing guide

For having a good experience of technical authoring in this project you need to follow the instructions below. But these rules are not the best in the world; We are open to your contribution to update our writing styles as well. As you noticed we write out documentation in Markdown format into [this repository](https://github.com/Geeksltd/MSharp.Docs/). It's also available from [this website](https://learn.msharp.co.uk/).

### Markdown

You must use Markdown styling in this set of documentation. The most symbols and styles that you will be going to use are:

- Headings (With # )
- `Slices of code`
- Blocks of code

```csharp
// blocks of code here
```

- **Bold** and *Italic* emphasis.
- > Notes or quotes

You can find markdown cheat sheet [HERE](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

There are some rules about Markdown which you must consider. For example their extension should be `.md` and any block of code, heading and list should be surrounded by spaces; Or no space is allowed at the end of the sentence.

Here a list of Markdown roles are listed below:

- MD001 header-increment - Header levels should only increment by one level at a time
- MD002 first-header-h1 - First header should be a top level header
- MD003 header-style - Header style
- MD004 ul-style - Unordered list style
- MD005 list-indent - Inconsistent indentation for list items at the same level
- MD006 ul-start-left - Consider starting bulleted lists at the beginning of the line
- MD007 ul-indent - Unordered list indentation
- MD009 no-trailing-spaces - Trailing spaces
- MD010 no-hard-tabs - Hard tabs
- MD011 no-reversed-links - Reversed link syntax
- MD012 no-multiple-blanks - Multiple consecutive blank lines
- MD013 line-length - Line length
- MD014 commands-show-output - Dollar signs used before commands without showing output
- MD018 no-missing-space-atx - No space after hash on atx style header
- MD019 no-multiple-space-atx - Multiple spaces after hash on atx style header
- MD020 no-missing-space-closed-atx - No space inside hashes on closed atx style header
- MD021 no-multiple-space-closed-atx - Multiple spaces inside hashes on closed atx style header
- MD022 blanks-around-headers - Headers should be surrounded by blank lines
- MD023 header-start-left - Headers must start at the beginning of the line
- MD024 no-duplicate-header - Multiple headers with the same content
- MD025 single-h1 - Multiple top level headers in the same document
- MD026 no-trailing-punctuation - Trailing punctuation in header
- MD027 no-multiple-space-blockquote - Multiple spaces after blockquote symbol
- MD028 no-blanks-blockquote - Blank line inside blockquote
- MD029 ol-prefix - Ordered list item prefix
- MD030 list-marker-space - Spaces after list markers
- MD031 blanks-around-fences - Fenced code blocks should be surrounded by blank lines
- MD032 blanks-around-lists - Lists should be surrounded by blank lines
- MD033 no-inline-html - Inline HTML
- MD034 no-bare-urls - Bare URL used
- MD035 hr-style - Horizontal rule style
- MD036 no-emphasis-as-header - Emphasis used instead of a header
- MD037 no-space-in-emphasis - Spaces inside emphasis markers
- MD038 no-space-in-code - Spaces inside code span elements
- MD039 no-space-in-links - Spaces inside link text
- MD040 fenced-code-language - Fenced code blocks should have a language specified
- MD041 first-line-h1 - First line in file should be a top level header
- MD042 no-empty-links - No empty links
- MD043 required-headers - Required header structure
- MD044 proper-names - Proper names should have the correct capitalization
- MD045 no-alt-text - Images should have alternate text (alt text)

#### Docsify

We use a pretty tool named [Docsify](docsify.js.org) to turn our markdown files of our repository into a well rounded website.

#### Folders

Every topic needs to be stored in it's exact folder architecture. Look at [Tutorials](https://github.com/Geeksltd/MSharp.Docs/tree/master/Domain) or [Basics](https://github.com/Geeksltd/MSharp.Docs/tree/master/Tutorials) folder to get a birds eye about the architecture.

Also the folder [_media](https://github.com/Geeksltd/MSharp.Docs/tree/master/_media) is responsible to store the files which are related to [Docsify](####Docsify) or project information media.

#### Media and files

There are two ways of saving and displaying files:

1. Including media in the repository (Recommended for the media that is strictly about the topic and needs group contribution as the documentation develops)
2. Uploading to github user content (Recommended in most cases)

The good point about saving files in the repo is that it's maintainable by contributors and the dark side is that it can make the repo too heavy as time goes bye.
You can upload media into github user content by simply pasting the file in a text block of github (such as edit sections or issues) and then github with get you a link.

Strictly avoid putting binaries and large files.

#### Recommendation

I recommend you to use VSCode for editing markdowns. it helps you tio write better markdown with the ability of previewing Markdown side by side and also spell check.

install these plugins into VSCode:

- markdownlint
- code spell check
- markdown preview

### M# documents specific styles

In each **Tutorial** episode there is x main parts that you must cover:

- A name with this format : *M# Tutorial - Episode 18: Automated tasks*
- A short talk about the whole tutorial with this format:

In this tutorial you will learn:

    - Repeated buttons
    - Button markup template
    - Checkbox column for list modules
    - Display option for columns
    - Instance accessor for entity types
    - Automated tasks

- Requirements which must have pictures
- Implementation : Entities
- Implementation : Logic (If needed)
- Implementation: UI
    - Pages
        - Sub pages
    - Modules
        - Form modules
        - List modules
        - Adding to menu module
    - Final Step

### Technical writing good practices

The goal of all technical documents are to learn a user a particular things as easy as possible. So use easy but creative and lovely language. Keep it sort, stupidly simple but effective. Also improve your written English skills during your technical writing.

Nothing is worst than an info dump. In any tutorial that you are authoring, be careful of new comers and try to go further the tutorial step by step and clearly; From zero to hero.

Use the power of markdown and differentiate the words where there was any `Code();` or something really **Important** or something that must *differ* from the rest of sentence.

> **Note**: Also you can add notes to your document incase there was something to notice. Don't forget to see this document's raw MD file to see bunch of Markdown good practices 😁.

Use less jargon and super technical vocabulary. yes it's true in software industry jargons are everywhere, but the art is to express yourself as simple as possible.

Use less abbreviations but if you are using them at the first time write the complete form.

Bad practice:

> SOA is a style of software design where services are provided to the other components by application components, through a communication protocol over a network.

Good practice:

> A service-oriented architecture (SOA) is a style of software design where services are provided to the other components by application components, through a communication protocol over a network.

But be careful that don't extend abbreviations too much. Some of them are known enough (Like CPU) or some of then do not need to be extended (Like MySQL).

Mostly try to use *active* sentences rather than *passive*.

Meh practice:

> The offering price was established by the real estate vendor and the negotiation process was initiated by the real estate buyer.

Better practice:

> The real estate vendor set the offering price, and the real estate buyer started negotiating.

But sometimes you must use passive. Like the places that action itself is really important but we don't care about the actor at all.

Read your documentation load and try to improve it. Make sure that your documents meets our standards and there is nothing wrong in your content.

By the way, being positive is better than being negative–even in writing!

Meh practice:

> I did not think that the unbelievable would not occur.

Better practice:

> I thought the unbelievable would happen.
