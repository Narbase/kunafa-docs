---
slug: /
---
# Getting Started

## Kunafa Philosophy

The main goal of Kunafa is to create web development fun. It takes a pragmatic approach to abstracting the complexities of the underlying technologies. As such, it provides helper functions and classes so that developers can think in higher level of abstraction than working directly with HTML, CSS and JavaScript.

Kunafa tries to be a complete solutions for web developers in an unopinionated way.

### What Kunafa is NOT:
- Kunafa is not a wrapper around HTML and CSS.
- Kunafa is not a client side only library to create Single Page Applications

## Why use Kunafa
### Declarative views and type safe CSS

```kotlin
fun main() {
	page {  
	    verticalLayout {  
	        style {  
	            width = matchParent  
	            minWidth = 200.px  
	            height = matchParent  
	            padding = 32.px  
	            alignItems = Alignment.Center  
	        }  
	  
	        textView {  
	            text = "Kunafa Todo"  
	            style {  
	                fontSize = 32.px  
	                color = Color(100, 240, 100)  
	            }  
	        }        
	        button {  
	            id = "myButton"  
	            text = "Add to do"  
	            style {  
	                marginTop = 16.px  
	            }  
	        }   
		 }
	}
}

```

### Components
Wrap any view in a component class and override lifecycle methods
```kotlin
  
fun main() {  
    page {  
        mount(TodoPageComponent())  
    }  
}  
  
class TodoPageComponent() : Component() {  

	override fun onViewMounted(lifecycleOwner: LifecycleOwner) {  
	    ServerCaller.getList()  
	}
    
    override fun View?.getView() = verticalLayout {  
        style {  
            width = matchParent  
            minWidth = 200.px  
            height = matchParent  
            padding = 32.px  
            alignItems = Alignment.Center  
        }  
  
        textView {  
            text = "Kunafa Todo"  
            style {  
                fontSize = 32.px  
                color = Color(100, 240, 100)  
            }  
        }        
        button {  
            id = "myButton"  
            text = "Add to do"  
            style {  
                marginTop = 16.px  
            }  
        }    
	}
}
```

### Builtin routing
Use declarative routing similar to defining views.

```kotlin
page {  
    route("/", isExact = true) {  
        verticalLayout {  
            textView { text = "Home" }  
            link("/page-1") { text = "Go to first page" }  
        }    
	}    
	route("/page-1") {  
        textView { text = "First page" }  
    }
}
```

### Server-side Rendering
Use Kunafa on the server side to generate static HTML and CSS and then hydrate the views on the front end.


## Hello, World example 
It is easy to get started with Kunafa and start front-end web development with Kotlin. This guide will focus on client side rendering. We will discuss server side rendering later.

Here's a summary of the steps to get started:
* Create a Kotlin/js project.
* Add Kunafa dependencies.
* Write your first Hello World Application

### Create a Kotlin/js project
Setting a new Kotlin JS project is straightforward. Follow the official docs here to set up a project here [Set up a Kotlin/JS project](https://kotlinlang.org/docs/js-project-setup.html)

### Add Kunafa dependencies
To add Kunafa to your project, simply add it to your `build.gradle` (or `build.gradle.kts`) file. 

Add the following line and replace `<latest-version>` with the latest Kunafa version which you can [find here](https://mvnrepository.com/artifact/com.narbase.kunafa/core).

```groovy
implementation 'com.narbase.kunafa:core:<latest-version>'
````

And that's it. Now you can start playing with Kunafa.

### Write your first Hello World Application
After you sync your gradle project, create a new Kotlin file named `App.kt`. Then create the `main` function.
```kotlin
fun main() {

}
```
Kunafa provides a simple DSL to create UI components . The root component should always be `page`. The `page` component corresponds to a web page; thus, there should be only one `page` component.

Add a `page` component to your `main` function
```kotlin
import com.narbase.kunafa.core.components.page

fun main(args: Array<String>) {
    page {
    
    }
}
```

Next, add a `textView` with text of `Hello world!`. 
```kotlin
import com.narbase.kunafa.core.components.page
import com.narbase.kunafa.core.components.textView

fun main(args: Array<String>) {
    page {
        textView {
            text = "Hello world!"
        }
    }
}
```

Then run the project by running the `run` task in the terminal. 
```bash
./gradlew run
```

or you can run `./gradlew run -t` to take advantage of Gradle continuous build.

And we are done. Your browser should automatically open and you should see `Hello world!` on the page.

Next guide will go deeper into Kunafa to create interactive page.





