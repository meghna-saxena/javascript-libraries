# What is CSS?
- Cascading style sheets
- Typically a web page is built by HTML which structures the page and shows content on the browser.
- CSS is optional, and allows to add styles to the HTML content. It add the visual effetcs.


# CSS History, Present & Future
- CSS was first introduced in 1996, referred as CSS version 1.0
- In 1998, CSS version 2.0 got released
- CSS 3.0 is still in development
- We'll never get version 4.0, since w/ version 3 the apporach towards CSS changed
- Rather than focussing on diff versions, CSS is split into modules which are organized by the
feature they cover
Eg: Modules on coloring text, modules focussing on shadows, modules focussing on animations

# Understanding the basics
- How to add CSS to html  
- Setting up CSS rules
- `Selectors, properties and values`
- Resolve conflicting styles

## Adding CSS
- 3 ways:

    - Inline styles by `style` attibute to any html element. Declare the styles.
      - Add more style, by spearating with semi-colon
      - This approach is not much recommended because in bigger pages, the code becomes unreadable

    - Internal css 
      - Inside <head> tag, add <style> tags and write CSS rules.
      - Selectors are additional piece of info that tells css to which element on DOM the style declaration
      is applied
      Eg: `<style>section { background: #000; }</style>`
      - This applies the same style to all the similar selectors

    - External css file
      - CSS rule consists of - selector, property and value
      - Add the file by `<link rel="stylesheet" href="style.css">`
      - Recommended way of adding styles
      - If same style sheet is used in muliple pages, browser can cache the stylesheet and doesnt need to 
      redownload again, but if style is added in head, the size of html page is increased and browser needs
      to re-download it for every page which can be slower


## Applying additional styles & importing google fonts
- sans-serif, serif and monospace are good fonts to be added as default in font-family
of the selector 
- Add google fonts, add the link to html file, inside the css file, add the css rule in the selector


## More about selectors

- *Elements* => set similar style for these elements. Eg: h1, section, p, div
- *Classes* => define a style which will be applied to `all elements that have same class`, 
and class is added to element by `class` attribute. In css file, class selector is denoted by
dot followed by class name. Eg: `.blog-post{...}`
- *Universal selectors* => style every element. Eg: `* { color: #eee; }`
- *IDs* => allows to select elements by id. Set style to `one specific element`. Denoted by `#id-name{...}`
- *Attributes selector* => set equal styles to all elements w/ attribute(s).
Eg: `<button disabled>Click</button>`
In css file, all buttons/elements with `disabled` attribute is selected by:
enclosing attribute name in square brackets => `[disabled] { color: red };`

Notes:
- ID selctors apart of adding style aslo add # at the end of url, and browser jumps down to the specific
element in the page.
- Can assign multiple classes w/ a space between the classes, eg: `class="section-title article-title"`
- Naming convention: HTML/CSS is case-insensitive, product-overview and product-Overview are interpreted equally 
therefore, use lower case with kebab-case to prevent style overriding


## Understanding the "cascading" style & specificity

The order of writing selctors matters in case of same selector, but if element is given a style,
eg: h1 tag, and then another h1 is given some class styles, the class override it, no matter in which order
its declared.

So `class selector has high specificity than element selector`
- Multiple rules affect the same element is the cascading part of css. *Cascading means multiple css rules 
can be applied to same element*. These rules can lead to conflicts though.

  - To resolve such conflicts css uses the concept k/a `specificity`
  - universal selector(*), <tag> and ::pseudo-element selectors has lowest priority
  - .class, ::pseudo-class and [attribute] selector has higher specificty
  - #ID selectors has more higher specificity
  - *Inline styles* are given the *highest priority*


## Understanding inheritance 

- Inheritance means an element also inherits some styles of the parent element.
- Add basic globl styles to the body element which is passed down to the child elements.
- However inheritance has very low specificity, it comes at the bottom, even below the browser default
webkit styles.
- Fonts are usually set at a global level to have consistency in page.

There are inherited and not-inherited properties in CSS:

https://developer.mozilla.org/en-US/docs/Web/CSS/inheritance#Inherited_properties

If you apply a inherited property to the body (like the font color), this will be applied automatically 
to all nested elements (if not overridden there).

But other properties like the margin are not inherited. So the margin definition of the body has 
no influence on the own margins of the other elements. If you want them all to have a margin:0, 
you would have to set it on each element separately - or use *.


## Adding combinators
- How to check if nested elements takes the same style as their parent element?
Set `font-family: inherit` which means to use inheritance style, increase the specificity of inheritance.

- Combinators allows to use multiple selectors to be more precise about what you want to select.
Eg: Add a combinator to h1 selector to narrow down which h1 tag is selected.
#product-overview h1 {...}
- It creates higher specificity. More rules, more specificity.

### 4 important types of combinators:
-> Adjacent sibling combinator
    Add a '+' between the selectors you want to combine. They can be more than 2
    Eg: div + p {...}
    h2 + p { color: red}; //style is applied to p element directly following the h2 element

      - Elements share the same parent
      - Second element comes immediately after first element

-> General sibling combinator
    Add a '~' between the selectors you want to combine. They can be more than 2
    Eg: div ~ p {...}
    h2 + p { color: red}; //style is applied all p element even if they dont directly 
    follow the h2 element

      - Elements share the same parent
      - Second element comes after first element (no need to directly come after)

-> Child combinator
    Add a '>' between the selectors you want to combine. They can be more than 2
    Eg: div > p {...}

    Any p element thats a `direct child` of div get the styles
      - Second element is direct child of first element

-> Descendent combinator
    Use whitespace between the selectors you want to combine. They can be more than 2
    Eg: div p {...}

    All p elements get the style if they are under div
      - Second element is descendent of first element
      - Most often used

  Notes:
  A combinator in the end also is part of a selector, so a "general sibling selector" simply 
  is a selector which includes a sibling combinator. The combinator itself is just the + , ~  etc 

  What's a "Rule" in CSS?
  - A combinator of selector ("what to style") and declaration ("how to style it")

  What is specificity about?
  Specificity is all about resolving conflicts that arise from multiple css rules which
  target the same element

  What is a combinator?
  Combinators (~, +, >, ) tie two selectors together (in a way defined by the combinator).

__________________________________________________________________________

  # Diving deeper in CSS
