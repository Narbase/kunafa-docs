# Advanced topics

# RouteMeta
When creating a route using the `route{}` or the `routeComponent{}`, you can access a RouteMeta objects that allows you to access route parameters and override certain behavior. 

## Route Parameters
Once a view or component is loaded, you can access an observer that holds a map of the URL parameters. 

```kotlin
page {  
	val productDetailsComponent = ProductDetailsComponent()
	
    routeComponent("/products/:id") { meta ->
	    meta.params.observe {  
		    val id = it?.get("id") ?: return@observe  
		    productDetailsComponent.getProductDetails(id)  
		}
        productDetailsComponent 
    }
}
```


## Overriding navigation events using `onRouteWillChange`
This function is called before the route changes. If the return value is false, then route will not change.

For example, if you want to prevent navigating away when changes are not saved in a bill (dirty), then you can use something like this.

```kotlin
routeComponent("/bill") { meta -> 

    meta.onRouteWillChange = { !billComponent.isDirty }  
    billComponent  
}
```


## Clearing route tree with `invalidateCache`
Routing in Kunafa is declarative. When routes are first crated, Kunafa constructs a route tree. If you want to clear the tree (for example when logging out), you can call `invalidateCache`
