---
slug: /
---
# Getting Started

## Welcome to Kunafa! 
It is easy to get started with Kunafa and start front-end web development with Kotlin. This guide will focus on client side rendering. We will discuss server side rendering later.

Here's a summary of the steps to get started:
* Create a Kotlin/js project.
* Add Kunafa dependencies.
* Write your first Hello World Application

## Create a Kotlin/js project
Setting a new Kotlin JS project is straightforward. Follow the official docs here to set up a project here [Set up a Kotlin/JS project](https://kotlinlang.org/docs/js-project-setup.html)

## Add Kunafa dependencies
To add Kunafa to your project, simply add it to your `build.gradle` (or `build.gradle.kts`) file. 

Add the following line and replace `<latest-version>` with the latest Kunafa version which you can [find here](https://mvnrepository.com/artifact/com.narbase.kunafa/core).

```groovy
implementation 'com.narbase.kunafa:core:<latest-version>'
````

And that's it. Now you can start playing with Kunafa.

## Write your first Hello World Application
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





