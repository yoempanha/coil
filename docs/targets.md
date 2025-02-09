# Targets

Targets receive the `Drawable` result of an `ImageRequest`. They often act as "view adapters" by taking the placeholder/error/success drawables and applying them to a `View` (e.g. `ImageViewTarget`).

Here's the easiest way to create a custom target:

```kotlin
val request = ImageRequest.Builder(context)
    .data("https://www.example.com/image.jpg")
    .target(
        onStart = { placeholder ->
            // Handle the placeholder drawable.
        },
        onSuccess = { result ->
            // Handle the successful result.
        },
        onError = { error ->
            // Handle the error drawable.
        }
    )
    .build()
imageLoader.enqueue(request)
```

There are 2 types of targets:

* [Target](../api/coil-base/coil-base/coil.target/-target/): The base target class. Prefer this if the image request isn't tied to a `View`.
* [ViewTarget](../api/coil-base/coil-base/coil.target/-view-target/): A target with an associated `View`. Prefer this if the request sets the placeholder/error/success Drawables on a `View`. Using `ViewTarget` also binds the request to the `View`'s lifecycle.
