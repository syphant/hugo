+++
title = "Hugo Markdown Guide"
date = "2024-01-14"
+++

This article offers a detailed overview of what can be used in Hugo content files.

<!--more-->

## Headings

The following HTML `<h1>`—`<h6>` elements represent six levels of section headings. `<h1>` is the highest section level while `<h6>` is the lowest.

# H1

## H2

### H3

#### H4

##### H5

###### H6

## Paragraph

Xerum, quo qui aut unt expliquam qui dolut labo. Aque venitatiusda cum, voluptionse latur sitiae dolessi aut parist aut dollo enim qui voluptate ma dolestendit peritin re plis aut quas inctum laceat est volestemque commosa as cus endigna tectur, offic to cor sequas etum rerum idem sintibus eiur? Quianimin porecus evelectur, cum que nis nust voloribus ratem aut omnimi, sitatur? Quiatem. Nam, omnis sum am facea corem alique molestrunt et eos evelece arcillit ut aut eos eos nus, sin conecerem erum fuga. Ri oditatquam, ad quibus unda veliamenimin cusam et facea ipsamus es exerum sitate dolores editium rerore eost, temped molorro ratiae volorro te reribus dolorer sperchicium faceata tiustia prat.

Itatur? Quiatae cullecum rem ent aut odis in re eossequodi nonsequ idebis ne sapicia is sinveli squiatum, core et que aut hariosam ex eat.

## Links

This is a [internal link](/posts/emoji-support) to another page. [This one](https://www.gohugo.io) points to a external page nad will be open in a new tag.

## Blockquotes

The blockquote element represents content that is quoted from another source, optionally with a citation which must be within a `footer` or `cite` element, and optionally with in-line changes such as annotations and abbreviations.

#### Blockquote without attribution

> Tiam, ad mint andaepu dandae nostion secatur sequo quae.
> **Note** that you can use _Markdown syntax_ within a blockquote.

#### Blockquote with attribution

> Don't communicate by sharing memory, share memory by communicating.<br>
> — <cite>Rob Pike[^1]</cite>

## Tables

Tables aren't part of the core Markdown spec, but Hugo supports them out-of-the-box.

| Name  | Age |
| ----- | --- |
| Bob   | 27  |
| Alice | 23  |

#### Inline Markdown within tables

| Italics   | Bold     | Code   |
| --------- | -------- | ------ |
| _italics_ | **bold** | `code` |

## Code Blocks

#### Code block with backticks

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8" />
        <title>Example HTML5 Document</title>
    </head>
    <body>
        <p>Test</p>
    </body>
</html>
```

#### Code block indented with four spaces

    <!doctype html>
    <html lang="en">
    <head>
      <meta charset="utf-8">
      <title>Example HTML5 Document</title>
    </head>
    <body>
      <p>Test</p>
    </body>
    </html>

#### Code block with Hugo's internal highlight shortcode

{{< highlight html >}}

<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Example HTML5 Document</title>
</head>
<body>
  <p>Test</p>
</body>
</html>
{{< /highlight >}}

## List Types

#### Ordered List

1. First item
2. Second item
3. Third item

#### Unordered List

-   List item
-   Another item
-   And another item

#### Nested list

-   Fruit
    -   Apple
    -   Orange
    -   Banana
-   Dairy
    -   Milk
    -   Cheese

#### Foot Notes

Check it[^2] at the end[^3] of this article[^4].

## Other Elements — abbr, sub, sup, kbd, mark

<abbr title="Graphics Interchange Format">GIF</abbr> is a bitmap image format.

H<sub>2</sub>O

X<sup>n</sup> + Y<sup>n</sup> = Z<sup>n</sup>

Press <kbd><kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>Delete</kbd></kbd> to end the session.

Most <mark>salamanders</mark> are nocturnal, and hunt for insects, worms, and other small creatures.

[^1]: The above quote is excerpted from Rob Pike's [talk](https://www.youtube.com/watch?v=PAAkCSZUG1c) during Gopherfest, November 18, 2015.
[^2]: A footnote.
[^3]: Another one.
[^4]: Cool, right?

# Math Typesetting

Mathematical notation in a Hugo project can be enabled by using third party JavaScript libraries.

In this example we will be using [KaTeX](https://katex.org/)

-   Create a partial under `/layouts/partials/math.html`
-   Within this partial reference the [Auto-render Extension](https://katex.org/docs/autorender.html) or host these scripts locally.
-   Include the partial in your templates like so:

```bash
{{ if or .Params.math .Site.Params.math }}
{{ partial "math.html" . }}
{{ end }}
```

-   To enable KaTex globally set the parameter `math` to `true` in a project's configuration
-   To enable KaTex on a per page basis include the parameter `math: true` in content files

**Note:** Use the online reference of [Supported TeX Functions](https://katex.org/docs/supported.html)

{{< math.inline >}}
{{ if or .Page.Params.math .Site.Params.math }}

<!-- KaTeX -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.css" integrity="sha384-zB1R0rpPzHqg7Kpt0Aljp8JPLqbXI3bhnPWROx27a9N0Ll6ZP/+DiW/UqRcLbRjq" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/katex.min.js" integrity="sha384-y23I5Q6l+B6vatafAwxRu/0oK/79VlbSz7Q9aiSZUvyWYIYsd+qj+o24G5ZU2zJz" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.11.1/dist/contrib/auto-render.min.js" integrity="sha384-kWPLUVMOks5AQFrykwIup5lo0m3iMkkHrD0uJ4H5cjeGihAutqP0yW0J6dpFiVkI" crossorigin="anonymous" onload="renderMathInElement(document.body);"></script>
{{ end }}
{{</ math.inline >}}

### Examples

{{< math.inline >}}

<p>
Inline math: \(\varphi = \dfrac{1+\sqrt5}{2}= 1.6180339887…\)
</p>
{{</ math.inline >}}

Block math:

$$
 \varphi = 1+\frac{1} {1+\frac{1} {1+\frac{1} {1+\cdots} } }
$$

# Emoji Support

Emoji can be enabled in a Hugo project in a number of ways.

The [`emojify`](https://gohugo.io/functions/emojify/) function can be called directly in templates or [Inline Shortcodes](https://gohugo.io/templates/shortcode-templates/#inline-shortcodes).

To enable emoji globally, set `enableEmoji` to `true` in your site's [configuration](https://gohugo.io/getting-started/configuration/) and then you can type emoji shorthand codes directly in content files; e.g.

<p><span class="nowrap"><span class="emojify">🙈</span> <code>:see_no_evil:</code></span>  <span class="nowrap"><span class="emojify">🙉</span> <code>:hear_no_evil:</code></span>  <span class="nowrap"><span class="emojify">🙊</span> <code>:speak_no_evil:</code></span></p>
<br>

The [Emoji cheat sheet](http://www.emoji-cheat-sheet.com/) is a useful reference for emoji shorthand codes.

**N.B.** The above steps enable Unicode Standard emoji characters and sequences in Hugo, however the rendering of these glyphs depends on the browser and the platform. To style the emoji you can either use a third party emoji font or a font stack; e.g.

{{< highlight html >}}
.emoji {
font-family: Apple Color Emoji, Segoe UI Emoji, NotoColorEmoji, Segoe UI Symbol, Android Emoji, EmojiSymbols;
}
{{< /highlight >}}

{{< css.inline >}}

<style>
.emojify {
	font-family: Apple Color Emoji, Segoe UI Emoji, NotoColorEmoji, Segoe UI Symbol, Android Emoji, EmojiSymbols;
	font-size: 2rem;
	vertical-align: middle;
}
@media screen and (max-width:650px) {
  .nowrap {
    display: block;
    margin: 25px 0;
  }
}
</style>

{{< /css.inline >}}

# HTML and CSS-Only Tabs

## Shortcodes

The following content:

```markdown
{{</* tabgroup */>}}
{{</* tab name="Hello" */>}}
Hello World!
{{</* /tab */>}}

{{</* tab name="Goodbye" */>}}
Goodbye Everybody!
{{</* /tab */>}}
{{</* /tabgroup */>}}
```

Will generate:

{{< tabgroup >}}
{{< tab name="Hello" >}}
Hello World!
{{< /tab >}}

{{< tab name="Goodbye" >}}
Goodbye Everybody!
{{< /tab >}}
{{< /tabgroup >}}

## Right alighment

You can also align the tabs to the right:

```markdown
{{</* tabgroup align="right" */>}}
{{</* tab name="Hello" */>}}
Hello World!
{{</* /tab */>}}

{{</* tab name="Goodbye" */>}}
Goodbye Everybody!
{{</* /tab */>}}
{{</* /tabgroup */>}}
```

Giving you this look:

{{< tabgroup align="right" >}}
{{< tab name="Hello" >}}
Hello World!
{{< /tab >}}

{{< tab name="Goodbye" >}}
Goodbye Everybody!
{{< /tab >}}
{{< /tabgroup >}}

## Markdown content

Any valid markdown can be used inside the tab:

````markdown
{{</* tabgroup align="right" style="code" */>}}
{{</* tab name="Ruby" */>}}

```ruby
puts 'Hello'
```

{{</* /tab */>}}
{{</* tab name="Python" */>}}

```python
print('Hello')
```

{{</* /tab */>}}
{{</* tab name="JavaScript" */>}}

```js
console.log("Hello");
```

{{</* /tab */>}}
{{</* /tabgroup */>}}
````

And you get this lovely content:

{{< tabgroup align="right" style="code" >}}
{{< tab name="Ruby" >}}

```ruby
puts 'Hello'
```

{{< /tab >}}
{{< tab name="Python" >}}

```python
print('Hello')
```

{{< /tab >}}
{{< tab name="JavaScript" >}}

```js
console.log("Hello");
```

{{< /tab >}}
{{< /tabgroup >}}

In this case `style="code"` makes it look a little nicer for scenarios where
your content is purely a code block.

# Mermaid Support

If you want to use [Mermaid-JS](https://mermaid-js.github.io/mermaid/#/) on your website.
Provide `mermaid` as [Shortcode](https://gohugo.io/content-management/shortcodes/#readout) in your markdown file.

{{<mermaid>}}
flowchart LR

    A --> B

    B --> C

    C --> D

    D --> B

{{</mermaid>}}

{{<mermaid>}}
sequenceDiagram
participant Alice
participant Bob
Alice->>Bob: Hi Bob
Bob->>Alice: Hi Alice
{{</mermaid>}}

Find more example on [Mermaid-JS](https://mermaid-js.github.io/mermaid/#/) website.

# Rich Content

Hugo ships with several [Built-in Shortcodes](https://gohugo.io/content-management/shortcodes/#use-hugos-built-in-shortcodes) for rich content, along with a [Privacy Config](https://gohugo.io/about/hugo-and-gdpr/) and a set of Simple Shortcodes that enable static and no-JS versions of various social media embeds.

## YouTube Privacy Enhanced Shortcode

{{< youtube ZJthWmvUzzc >}}

<br>

---

## Twitter Shortcode

{{< tweet user="SanDiegoZoo" id="1453110110599868418" >}}

<br>

---

## Vimeo Simple Shortcode

{{< vimeo_simple 48912912 >}}

# More Rich Content

Hugo provides some custom shortcodes.

## Notice Shortcodes

{{< notice note >}}
One note here.
{{< /notice >}}

{{< notice tip >}}
I'm giving a tip about something.
{{< /notice >}}

{{< notice example >}}
This is an example.
{{< /notice >}}

{{< notice question >}}
Is this a question?
{{< /notice >}}

{{< notice info >}}
Notice that this box contain information.
{{< /notice >}}

{{< notice warning >}}
This is the last warning!
{{< /notice >}}

{{< notice error >}}
There is an error in your code.
{{< /notice >}}

# Placeholder Text

Lorem est tota propiore conpellat pectoribus de pectora summo. <!--more-->Redit teque digerit hominumque toris verebor lumina non cervice subde tollit usus habet Arctonque, furores quas nec ferunt. Quoque montibus nunc caluere tempus inhospita parcite confusaque translucet patri vestro qui optatis lumine cognoscere flos nubis! Fronde ipsamque patulos Dryopen deorum.

1. Exierant elisi ambit vivere dedere
2. Duce pollice
3. Eris modo
4. Spargitque ferrea quos palude

Rursus nulli murmur; hastile inridet ut ab gravi sententia! Nomine potitus silentia flumen, sustinet placuit petis in dilapsa erat sunt. Atria tractus malis.

1. Comas hunc haec pietate fetum procerum dixit
2. Post torum vates letum Tiresia
3. Flumen querellas
4. Arcanaque montibus omnes
5. Quidem et

# Vagus elidunt

<svg class="canon" xmlns="http://www.w3.org/2000/svg" overflow="visible" viewBox="0 0 496 373" height="373" width="496"><g fill="none"><path stroke="#000" stroke-width=".75" d="M.599 372.348L495.263 1.206M.312.633l494.95 370.853M.312 372.633L247.643.92M248.502.92l246.76 370.566M330.828 123.869V1.134M330.396 1.134L165.104 124.515"></path><path stroke="#ED1C24" stroke-width=".75" d="M275.73 41.616h166.224v249.05H275.73zM54.478 41.616h166.225v249.052H54.478z"></path><path stroke="#000" stroke-width=".75" d="M.479.375h495v372h-495zM247.979.875v372"></path><ellipse cx="498.729" cy="177.625" rx=".75" ry="1.25"></ellipse><ellipse cx="247.229" cy="377.375" rx=".75" ry="1.25"></ellipse></g></svg>

[The Van de Graaf Canon](https://en.wikipedia.org/wiki/Canons_of_page_construction#Van_de_Graaf_canon)

## Mane refeci capiebant unda mulcebat

Victa caducifer, malo vulnere contra dicere aurato, ludit regale, voca! Retorsit colit est profanae esse virescere furit nec; iaculi matertera et visa est, viribus. Divesque creatis, tecta novat collumque vulnus est, parvas. **Faces illo pepulere** tempus adest. Tendit flamma, ab opes virum sustinet, sidus sequendo urbis.

Iubar proles corpore raptos vero auctor imperium; sed et huic: manus caeli Lelegas tu lux. Verbis obstitit intus oblectamina fixis linguisque ausus sperare Echionides cornuaque tenent clausit possit. Omnia putatur. Praeteritae refert ausus; ferebant e primus lora nutat, vici quae mea ipse. Et iter nil spectatae vulnus haerentia iuste et exercebat, sui et.

Eurytus Hector, materna ipsumque ut Politen, nec, nate, ignari, vernum cohaesit sequitur. Vel **mitis temploque** vocatus, inque alis, _oculos nomen_ non silvis corpore coniunx ne displicet illa. Crescunt non unus, vidit visa quantum inmiti flumina mortis facto sic: undique a alios vincula sunt iactata abdita! Suspenderat ego fuit tendit: luna, ante urbem Propoetides **parte**.

{{< css.inline >}}

<style>
.canon { background: white; width: 100%; height: auto; }
</style>

{{< /css.inline >}}