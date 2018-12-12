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

- Box model
  - Height & width properties
  - Display property (layout of page and positioning of elements)
  - Properties worth to remember: CSS references
  - Psuedo classes and elements

## CSS Box Model
- Every element in css is interpreted as a "box" which consists of content, padding, border, margin.
- 2 diff types of elements: block-level and inline


## Understanding margin collapsing & removing default margins
- The body element also has a default margin, so set margin: 0 initially;
- Every h1 has agagin some default margin

Margin collpasing: if there're 2 elements -
  -> 2 block element arrange one below another, then margin b/w them is collapsed to
  one margin. The bigger margin wins!
  -> In general, use margin-top or margin-bottom to prevent the collpasing

### Shorthand properties:
- Combine multiple properties into one single property
Eg: border-width, border-style, border-color -> condensed to border: 2px solid orange
    margin-top, margin-right, margin-bottom, margin-left -> 
    condensed to margin: 5px(top) 10px(right) 5px(bottom) 10px(left) || 5px (top & bottom) 10px(left & right)


### Height & width properties
`width: 100%` takes entire width of the page. This is default behavior since section, div, h1 elements are block level 
elements

`height: 100%` refers to available height given by the parent container. Otherwise takes only the height of the content. 
So give abosulte height (px) to parent container first. Then relative height (%) will work in child container.

```
.main { height: 300px };
section { height: 100% }; //works!
```

Note: When adding a height, margins do not collapse anymore.


### Understanding box-sizing
All elements have default way of calculating width & height k/a `box-sizing: content-box`, which only calculates content area,
and padding, border, margin are excluded. Set it to `border-box` to prevent this behavior. Width & height now includes the padding
and border. This property is not used in css of body element, since div or section are block-level elements so
inheritance doesnt work and this property is not applied. So use universal selector (*). Its overriding inheritance and browser defaults now.

- `*` selects all elements whereas we rely on inheritance otherwise. If you have an element that overwrites border-box (e.g. the browser default sets a different border-box), inheritance will not do the job. Selecting the element directly (via * ) will however.



### Adding header
```
 <header class="main-header">
        <div>
            <a href="index.html">
                uHost
            </a>
        </div>
        <nav>
            <ul>
                <li>
                    <a href="packages/index.html">Packages</a>
                </li>
                <li>
                    <a href="packages/index.html">Customers</a>
                </li>
                <li>
                    <a href="packages/index.html">Start Hosting</a>
                </li>
            </ul>
        </nav>
    </header>
```

### Display property
- The display property allows to change the behavior of the element from block to inline or inline-block  
or to remove it from DOM. 

Note: display: none just removes the element from visible document flow, not from the DOM. You can still set it in
inspected html elements on browser.

Eg of inline elements: <a> anchor tags. They dont take the entire width.

- Inline bock elements behaves like inline elements by sitting next to each other, but they can be modified by 
setting margins, paddings like block level elements.

`display: none vs visibility: hidden`

`display: none;`  - this value removes the element to which you apply it from the document flow. 
This means that the element is not visible and it also doesn't "block its position". 
Other elements can (and will) take its place instead.

There is an alternative to that though.

If you only want to hide an element but you want to keep its place (i.e. other elements don't fill the empty spot), 
you can use `visibility: hidden;`

Here's a visual example:
```
.box-1 {
    display: none;
}
 
.box-2 {
    display: inline-block;
}
```
Will render:

`x  `

where `x`  has the class box-2 . The first element just isn't displayed. It's still part of the DOM though, 
you can still access it via JavaScript for example.

Here's an example for visibility: hidden :

```
.box-1 {
    visibility: hidden;
}
 
.box-2 {
    display: inline-block;
}
```
Will render:

`_x `

where `_`  simply is an empty spot and `x ` has the class box-2 .

The element is only invisible, it's not removed from the document flow and of course also not from the DOM.


`Block-level vs Inline Elements`

- Block-level elements are rendered as a block and hence take up all the available horizontal space.
You can set margin-top and margin-bottom and two block-level elements will render in two different lines.

Some examples are: `<div> , <section> , <article> , <nav>  but also <h1> , <h2>  etc and <p>`

- Inline elements on the other hand only take up the space they require to fit their content in. 
Hence two inline-elements will fit into the same line (as long as the combined content doesn't take up the 
entire space in which case a line break would be added).

They also use the box-model you learned about but margin-top  and margin-bottom have no effect on the element. 
padding-top  and padding-bottom  also have a different effect. They don't push the adjacent content away but they 
will do so with the element border.

Additionally, setting a width  or height on an inline element also has no effect. 
The width and height is auto to take as much space as required by the content.

Logically, this makes sense since you don't want your inline elements to destroy your multi-line text-layout. 
If you want to do so or need both block-level and inline behavior, you can set display: inline-block to merge behaviors.

Some example elements are: `<a> , <span> , <img> `


Note: 
- Use `calc() property` like this: width: calc(100% - 54px);
- `vertical-align: middle` to both elements to ensure that the elements are perfectly aligned to each other.
If you don't apply it to the div, select the div in the Developer Tools and open the "Computed" tab, you see that 
the default value for vertical-align is baseline. That's not what we want as the elements should be aligned at the same level
therefore we have to add vertical-align: middle to both elements.

## BEM - Block element modifier
It helps keeping your CSS class names clean and structured and avoid name collisions
Eg: .main-nav__items, .main-nav__item