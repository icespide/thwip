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
 
.u-pullLeft {
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

## Comments

## Variables and Mixins

## Formatting

## z-index scale
Z-index should never be hardcoded, instead use one of the variables from z-index.less. @z-index-1 - @z-index-9 are the available ranges, @z-index-9 should rarely be needed. This helps us prevent us from losing control of the z-index in our application

## Font-size scale

## Units

## Specificity

## Branding

## Folder structure

## Where to put new styles


## Bundles