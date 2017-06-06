# CSS and Styling

CSS styling should follow the [SMACSS convention](https://smacss.com) for structure, class naming, and general principles. This convention encourages componentization and re-use for development efficiency along with rules which promote speed and flexibility in browsers.

This page is meant as a high level introduction to the convention along with our own personal adaptations and deviations from the proposed standards. For more in-depth reading of the principles and motivations behind SMACSS, [see the official website](https://smacss.com).

## Class Naming and Prefixes

Class names should be short and semantically relevant. Contrary to other CSS conventions, we don't include context hints into the class name itself. Additionally, we don't use layout or module prefixes for scoping as some SMACSS guidelines promote. Rather we focus on readability and succinctness for generic elements and take advantage of our build tooling to [add automatic scoping](https://vue-loader.vuejs.org/en/features/scoped-css.html) when necessary.

A simple example of this is a `<button>` component, which in Bootstrap or other frameworks might be written as:

`<button class="btn btn-danger btn-sm btn-outlined">Danger</button>`

Can get even more verbose using a convention such as BEM:

`<button class="register-form__submit register-form__submit--primary btn btn-primary btn-sm btn-outlined">Submit</button>`

Instead, we focus on descriptive readability and allow our build system to scope the CSS if necessary on a per-component basis. By stacking the CSS class names the above can be simplified and made more readable to other developers:

`<button class="small danger outlined">Danger</button>`

Class names should generally be a single descriptive word that describes the state or appearance. If multiple words are needed, they should be written in kebab-case.

## Rule Organization

In general, there are 5 categories of rules:

1. **Base** - Defaults for top level tags (includes CSS resets through Normalize)
2. **Layout** - Major sections of the page (includes grid system built through Lost)
3. **Module** - Re-usable and modular components
4. **State** - Describe how things look under various forms of interaction (normal/hover, collapsed/expanded, active/inactive, etc.)
5. **Theme** - Color scheme and typography treatment across the entire site

### Base Rules

Base styles include setting heading sizes, default link styles, default font styles, and body backgrounds. There should be no need to use `!important` in a Base style.

We use Normalize.css for our CSS reset, which are the first rules defined in our Base. This is done to provide a consistent base across various browsers and versions.

Read more about [Base rules here](https://smacss.com/book/type-base).

### Layout Rules

Layout rules are intended to target the major layout components in the design. Things like a header, footer, sidebars, etc. typically fall into a layout rule. Their individual elements (for example a logo and tagline inside a header) would typically fall in a module.

For our purposes, layout rules are generally split between generic rules written in CSS and more specific rules written for stateful components that exist in the `.vue` file.

Read more about [Layout rules here](https://smacss.com/book/type-layout).

### Module Rules

Module rules are almost entirely reserved for pure components and will typically exist in a `.vue` file accompanying the HTML and Javascript. Generic styling can be shared using either a parent component or by declaring variables and functions in a theme rule and referencing it here.

Because of our build system introducing scoping on each module, rules like avoiding element selectors can typically be relaxed at this level. The exception to this would be when multiple low level components are meant to be stacked to represent a single user-facing component.

Read more about [Module rules here](https://smacss.com/book/type-module).

### State Rules

State rules augment or override previous styles under certain conditions. When possible these should be built to be standalone and keep modifications to a narrow scope. There are three forms of state rules:

- **Class names:** typically controlled through bindings on the element based on the state of the application or it's data. Classes should always be prefixed with `is-`.
- **Pseudo-classes:** typically representing user actions such as hover. Can be stacked or used standalone along with class names for children or sibling selectors.
- **Media queries:** breakpoints defined for various viewport sizes.

Similar to layout rules, state rules can exist in two locations: the global application and on each `.vue` component (stateful or pure). Generally, the actual breakpoints themselves can be declared as variables in the build process through PostCSS.

Read more about [State rules here](https://smacss.com/book/type-state).

### Theme Rules

Theme rules exist to declare colors schemes or layouts when multiple may exist in a project. By separating these rules from all the other components a design is more flexibly adapted when undergoing a re-design or in cases where multiple themes are needed.

For our use, theme rules will generally exist as SASS functions and variables rather than any CSS  that a browser will parse. These can be used across all rules to ensure that common colors, sizes and spacing rules are observed by all elements.

> Future versions of the Gallery may include some variation of a theme-switcher or the ability to side-load full custom themes depending on the account association. For this project, and similar ones, additional attention may be warranted on having a separate theme layer.

Read more about [Theme rules here](https://smacss.com/book/type-theme).

## Rule organization

To further encourage the separation of styling concerns that SMACSS proposes, rules from each group are generally placed in their own partial. For our projects which are built in Vue some styles will be placed in `.vue` components based on whether they are stateful (router level) or pure (re-usable generic) components:

```
app
├─┬ styles/          // Style rules applicable across multiple components
│ ├── _base.css
│ ├── _layout.css
│ ├── _state.css
│ ├── _theme.css     // Typically variables and functions, no CSS rules
│ └── index.css      // Used to import partials, no CSS rules
├─┬ routes/
│ ├── dashboard.vue  // Layout rules scoped only to this stateful component
└─┬ components/
  └── topbar.vue     // Module and state rules scoped to this pure component
```

## Further Reading

- [SMACSS convention](https://smacss.com) official website
- [Introduction to SMACSS](http://vanseodesign.com/css/smacss-introduction/)
- [CSS strategy square-off](https://www.viget.com/articles/css-squareoff)
- [Presentational and Container components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)
