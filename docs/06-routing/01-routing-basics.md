# Routing Basics

## Routes are declarative
Routing in Kunafa is declarative. This means that you define the routes similar to how you define views (inside `page` or in the `getView` component function). So let's see how we can create routes.

## Creating basic routes
To crreate a route for a view, call the `route` function. For example, lets create a 2 views with 2 different routes.

```kotlin
page {  
    route("/page-1") {  
        textView { text = "First page" }  
    }
    route("/page-2") {  
        textView { text = "Second page" }  
    }
}
```
Now if you run this and go to `/page-1` you will see the text "First page" and if you go to `/page-2` you will get "Second page".

### Exact routes
In the above example, let us add a `/` route. 
```kotlin
page {  
    route("/") {  
        textView { text = "Home" }  
    }
	route("/page-1") {  
        textView { text = "First page" }  
    }
    route("/page-2") {  
        textView { text = "Second page" }  
    }
}
```
Now similarly, when you navigate to `/`  you will see the text "Home". However, if you navigate to `/page-1` you will see **both** texts "Home" and "First page"! 
Why? Because routes by defaults are not exact (See nesting routes below). And thus, the URL `/page-1` matches both `/` and `/page-1`. To change this behavior, set `isExact = true` in the home route.

```kotlin
route("/", isExact = true) {  
    textView { text = "Home" }  
}
```
Now if you go to `/page-1`, only the "First page" text appears.

### Routing components
The `route` function expects a view to be returned it is lambda. If however you want to route a component, you cal call `routeComponent`.

```kotlin
page {
	routeComponent("/login") { LoginComponent }
}
```

### Nesting routes
Routes can be easily nested when declaring routes. For example:
```kotlin
page {  
    route("/admin-area") {  
        view {  
            textView { text = "Admin Area" }  
            route("/page-1") { textView { text = "First page" } }  
            route("/page-2") { textView { text = "Second page" } }  
        }    
    }
}
```

Now if you go to `/admin-area` you will see the text `Admin Area`. However, if you go to `/admin-area/page-1` you will see **both** texts `Admin Area` and `First page`.
Note that if you go to `/page-1` instead of `/admin-area/page-1`, you will get an empty page is it is not a registered route.

Also note that because `route` function expects a single view returned, all children (textView and the 2 routes) are wrapped in a `view` .

 Using nested routes, component can define their own routes and they will automatically be added to the routing tree where they are first mounted.  

## Navigating
### Links
The easiest way to navigate, is by creating `Links` 
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
The link above when clicked will change the page to the first page.
Links are simply an anchor element and thus can be styled as you would any other anchor element.

### Using `navigateTo()`
`Router.navigateTo()` is an imperative way to navigate between routes. As such, you can safely call it in callbacks or when an event happens in your application.

```kotlin
textView {  
    text = "Profile"
    onClick = {  
        Router.navigateTo("/profile")  
    }  
}
```

## Redirecting
### Using `redirect()`
Instead of using `navigateTo()` imperatively, you can define a "redirect route" using `redirect()`. This will add a route entry in the routing tree that redirect to a specific path. 
```kotlin
page {  
    route("/", isExact = true) {  
        view { redirect("/page-1") }  
    }    
    route("/page-1") {  
        textView { text = "First page" }  
    }
}
```
Here, whenever the `/` is loaded, it will always redirect to `/page-1`
#### `redirect()` vs `navigateTo()`
As mentioned above, `navigateTo()` is imperative (will only navigate to a path when it is called), whereas `redirect()` is declarative and will ass a route to the routing tree. Practically, this means that:
- When creating views, e.g. in `getView()`, use `redirectTo()`.
- You should **NOT** use `redirect()` in callbacks (e.g. `onClick`). Use `navigateTo()`.
- You should **NOT** either  `redirect()` in lifecycle functions like `onViewMounted` and `onViewCreated()`.

### Using `matchFirst`
`matchFirst` is a routing function that will stop looking for a match once a route is found. This is helpful in certain cases. For example, you can create a simple 404 page as follows:

```kotlin
page {  
    matchFirst {  
        route("/page-1") { textView { text = "First page" } }  
        route("/page-2") { textView { text = "Second page" } }  
        route("/") { textView { text = "404 Not found" } }  
    }
}
```

Now if you navigate to any page other than `/page-1` and `/page-2` you will get the text "404 Not found". Note that the order of declaring routes in important.

Another use case for `matchFirst` is combining it with `redirect()`
```kotlin
page {  
    matchFirst {  
        route("/page-1") { textView { text = "First page" } }  
        route("/page-2") { textView { text = "Second page" } }  
        redirect("/page-1")  
    }
}
```
Now when you navigate to `/`, you will be redirected to `/page-1`

