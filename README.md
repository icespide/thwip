# thwip
A CSS style guide for enterprise web applications

## Naming conventions
When creating new class names, follow these guidelines:
* lowercase
* words separated by hyphens
* short and sensible
* specific to a component, not a screen
* name should not describe rule properties

**Good**
```css
.error-message {
    color: #ff0f1c;
}
```

**Bad**
```css
.fntff0flc {
    color: #ff0f1c;
}
```

## IDs vs Classes
You should pretty much avoid using IDs at all costs. ID based CSS cause specificty to become very brittle, and make conflicts very difficult to debug and refactor.

## Utility Classes
Rules that you find yourself re-using several times can be pulled out and rewritten as a utility class that can be shared and re-used by other developers. These utility classes should be small in scope and follow strict naming conventions with the prefix "u-".
```css
.u-center {
    margin: 0px auto;
}
 
.u-pull-left {
    float: left;
}
```

## States
Class names describing the state of a component should be prefixed with "is-". These classes can be added and removed with JavaScript. They should never be styled directly but only used with an adjoining component class name.

**Good**
```css
.nav-item { }
.nav-item.is-open { }
```

**Bad**
```css
.nav-item { }
 
.open { }
```

## JavaScript
Specific classes should be used explicitly for JavaScript selection. These classes should use the prefix "js-" and should under no circumstances be styled. They should only be referenced by JavaScript
```html
<div class="js-toggle"></div>
```

## Nesting
Nesting CSS should be limited to one level. Even then, it should be used sparingly. Convuluted nesting can lead to poor performance and it's just hard to read.

If you are writing component css, then you shouldn't be nesting to begin with. And since you are supposed to be favoring component based architecture to page specific architecture, nesting should not be something that comes up.

**Good**
```css
.main-nav {
	.nav-item {
		display: block;
	}

	.nav-item .sub-nav {
		display: block;
	}
}
```

**Bad**
```css
.main-nav {
	.nav-item {
		display: block;

		.sub-nav {
			display: block;
		}
	}
}
```

## !important
!important is a direct manifestation of specificity problems and should only be a last resort. For the most part, important should never be used and it's always bad. In situations where important seems like the only way to fix something, you should always instead consider refactoring the bit of CSS that is causing the specificity issue. Seriously you should feel really bad about checking in code with !important in it. If time does not permit a refactor, always leave a comment addressing the offending code with an explanation of why you felt it was necessary, and a TODO item recommending a refactor in the future.

The only time !important can be considered valid is if its used proactively in a project as a means to guarantee that a style will be applied rather than to fix a specificity problem. These types of uses should be reserved only for small utility type classes and more often than not reserved for the UI architecture team.

Consider the following markup
```html
<div class="main_section">
    <h2 class="section_header emphasis">...</h2>
</div>
```

**Good**
```css
.main_section .section_header {
    font-size: 20px;
}
 
.main_section .section_header.emphasis {
    font-size: 25px;
}
```

**Bad**
```css
.main_section .section_header {
    font-size: 20px;
}
 
.emphasis {
    font-size: 25px !important;
}
```

## Components
You should always try to abstract components so they can be reused. The console has lots of different screens that do many things but should retain a similar look and feel. The reuse of components helps to acheive this consistent look.

When writing new styles try not to think of it in terms of the specific screen you're building. You should instead try to write styles in a way that they can be reused in other parts of the application, because they probably can! A class name like `.smartgroups-tree-nav` has limited uses, where as a name like `.tree-nav` is more generic and could be reused in other screens.

Component styles should have their own individual less file. For example a tree navigation component would have a corresponding tree-nav.less file.

## Namespacing
When creating reusable CSS components, you should namespace your styles according to your component's name. You should never namespace according to a specific screen or page of the application (this discourages reusability).

**Good**
```css
.lg-picker,
.lg-picker-search,
.lg-picker-dropdown
```

**Bad**
```css
.lg-picker,
.settings-lg-picker,
.profiles-lg-picker
```

## Scoping to a specific page or screen
For the most part, pages should be using general component level styles in order to maintain consistency. In some very specific contexts, page level scoping can be useful to override certain generic styles. 

Take care not to over-use page level overrides, also be sure to limit your scoping to one single level of nesting.

```css
.profiles {
	.text-input {
		float:left;
	}
}
```

## Specificity
As a selector becomes more specific and complex, it's impact on rendering performance grows. Take this style for example:

```css
div.main-column div.grid table td span a:hover { color:blue; }
```

Browsers read selectors from right to left. In this example, everyone single <a> on the page would be individually inspected to determine if it resides any of the elements specified. This requires lots of DOM traversal, and can be quit slow on large documents. More information about how specificity affects performance [here](http://csswizardry.com/2011/09/writing-efficient-css-selectors/)

## Comments
Less style comments should be used because they'll get compiled out when optimized. Comments should be used to separate sensible groups of styles in a file. Try to stick to the following comment style:

**Good**
```less
// Modal // --------------------------------------------------

.modal {
	display:block;
}
```

**Bad**

```css
/* Modal
 **********************/

 .modal {
 	display:block;
}
```

## Formatting
Style declarations should start on a new line after the selector.

**Good**
```css
.nav-item {
	display:inline-block;
}
```

**Bad**
```css
.nav-item { display:inline-block; }
```

Within CSS rules, declarations should always appear on their own line. Do not place multiple declarations on the same line.

**Good**
```css
.nav-item {
	width:100%;
	height:50px;
	display:block;
}
```

**Bad**
```css
.nav-item {
	width:100%; height:50px; display:block;
}
```

If you have to use multiple selectors in a rule, place each selector on a new line. Do not place multiple selectors on the same line.

**Good**
```css
.nav-item,
.nav-link,
.nav-button {
	display:inline-block;
}
```

**Bad**
```css
.nav-item, .nav-link, .nav-button {
	display:inline-block;
}
```

## z-index scale
Z-index should never be hardcoded, instead use one of the variables from z-index.less. @z-index-1 - @z-index-9 are the available ranges, @z-index-9 should rarely be needed. This helps us prevent us from losing control of the z-index in our application

**Good**
```css
.modal {
	z-index: @z-index-5;
}
```

**Bad**
```css
.modal {
	z-index: 500;
}
```

## Font-size scale
Font sizes should also never be declared directly, this allows us to maintain consistancy and readability accross the application. Font sizes should always use variables from type.less.

```
ex:

@type-micro
@type-smallest
@type-smaller
@type-small
@type-base
@type-large
@type-larger
@type-largest
@type-jumbo
```

**Good**
```css
.nav-item {
	font-size: @type-base;
}
```

**Bad**
```css
.nav-item {
	font-size: 14px;
}
```

## Variables and Mixins

## Colors

## Branding

## Folder structure

## Where to put new styles

## Bundles