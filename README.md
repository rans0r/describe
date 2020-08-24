# Describe SCSS
Describe is a simple system based on SCSS placeholder selectors and mixins to allow for componentized core level building blocks, consistency throughout the project, easy to understand structured style management and automatically optimized CSS output. There are three primary goals for this coding structure: Scalable, Descriptive, DRY. 

## Project Settings Defined in a Self-Referential Map Structure
Instead of standard global variables, project variables are stored in an overwritable map. Settings are retrieved using a mixin that returns lists of name value pairs, values of which can reference other items in the project variables map to reduce variable duplication.

```scss
@include describe('project',(
	'breakpoints': (
		'default': (
			mobile: 767px,
			desktop: 768px
		),
		'smaller': (
			mobile: 400px,
			desktop: 401px
		),
		'large': (
			mobile: 999px,
			desktop: 1000px
		),
	),
	'color-pallet': (
		'transparent': 	transparent,
		'current':		currentColor,
		'black': 		'@colors.black',
		'white':		'@colors.white',
		'red':			'@colors.red-600',
		'gray': 		'@colors.gray-200',
		'green':		'@colors.green-600'
	),
));
```

## Descriptive Building Block Declarations
The @describe mixin handles building block declarations. Describe handles variables $it, $is and @content. If @content exists, new placeholder selectors are created for that CSS with modifiers for all breakpoint groupings described by the project. The $is variable holds a list of other building blocks to inherit from as part of this item. Example usage:

```scss
@include describe('padding-1'){
   padding: 1rem;
}
```

```scss
@include describe('button',(
   padding-1-mobile,
   padding-2-desktop,
   text-gray,
   font-bold,
   rounded,
   shadow,
   pointer
));
```

## Descriptive and Easily Organized Building Block Usage
The @extend mixin is used to list out, within standard SCSS selector structure, what building blocks to inherit from. Extend gathers all the building block placeholder selectors, based on breakpoint modifiers if used, and extends those for the item. Using this structure, a very robust building block system can be built easily with maximized code reuse and only the used building block styles ever written to the output CSS. Since placeholder selectors are widely used behind the scenes, instead of class names, a much more descriptive naming convention can be used; making code easier to understand without adding bloat to the output CSS or HTML. Example usage:

```scss
a[role="button"] {
	@include extend(
		button-red
	);
	&:hover {
		@include extend(bg-gray);
	}
	&:active {
		@include extend(bg-gray);
	}
}
```
