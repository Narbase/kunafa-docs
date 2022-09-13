# Working with Views

## Getting a reference to a view
All DSL functions return an instance of the view they create. Assign the return value of the function to get a reference of it.

```kotlin
val errorTextView = textView {
	
} 
errorTextView.text = "Unknown error"
```

## Editing views
Using the view reference, you can edit the properties of the view. 

### Accessing the HTML `element`
Each view has an `element` property that is a reference to the underlying JavaScript HTMLElement. This will allow you to edit any property of the element using the JavaScript API. For example
```kotlin

val layout = verticalLayout {
	textView { text = "Hello,"}
	textView { text = "World!"}
}
console.log("Layout height is ${layout.element.offsetHeight})
```

## Mounting views
Mounting a view means attaching to a parent in the [DOM](https://www.w3schools.com/js/js_htmldom.asp). This happens automatically when creating views using the DSL. 
A view can have only one parent. Therefore, if you mount a view in another parent, it will be detached from the first one. Here's an example.

```kotlin
verticalLayout {
	id = "firstParent"
	val label = textView {
		text = "Hello, World!"	
	}

	horizontalLayout {
		id = "secondParent"
		mount(label)
	}
}

```

In this example, `label` will be mounted inside the horizontal layout.
### The `parent` property
Every view has a nullable `parent: View?` property. When a view is mounted, this property is a reference to the view parent.

### Creating `detached` views
You can create a view that is not mounted by calling the DSL function on `detached`. You can then mount it when you need to.

```kotlin

val errorMessage = detached.textView { }

// later in the code

if (didErrorOccur) {
	errorMessage.text = "Error! Try again"
	parentView.mount(errorMessage)
}
```

By the way, `detached` is just [syntactic sugar](https://en.wikipedia.org/wiki/Syntactic_sugar) for `null` as you can achieve the same result by calling 
```kotlin
val errorMessage = null.textView { }
```
