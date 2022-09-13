# Basic Views

## Creating views
Kunafa provides a declarative Domain Specific Language DSL to create views. If you used any Kotlin UI library, Kunafa DSL should feel familiar. 

To create a view, you need to call the appropriate DSL function. For example, to create a view you will write the following. 
```kotlin

view {

}
```

All these DSL functions (except for `page`) are extension functions on the `View` class. Therefore, you need to have View as a receiver when you call DSL functions. For example, the following won't compile.

```kotlin

// This will NOT compile
fun main() {
	textView {
		text = "Hello, world"
	}
}
```

but this is fine.

```kotlin
fun main() {
	page {
		textView {
			text = "Hello, world"
		}
	}
} 
```

This required so views will be added to a parent. The alternative to that is to create a [detached view](03-working-with-views.md). 

## The View class
View is the simplest and basic UI element. All other views extend it. It is equivalent to an HTML `div` tag.

The `view` defines the common properties and functions such is `id` and `style`.

## Other views
Kunafa defines commonly used views such as `TextView`, `ImageView`, and `Button`. There are also [Layouts and Page](02-layouts-and-page.md). Other than that, you can find wrappers for most HTML tags. You can also wrap any arbitrary HTML or create your own view. Check [building custom view](04-building-custom-views.md) page for details.

## Views Properties
Some views define additional properties and functions in addition to the ones they inherit. For example, `TextView` have `text` property to get and set its text.
