﻿![Coil](logo.svg)

An image loading library for Android backed by Kotlin Coroutines. Coil is:

- **Fast**: Coil performs a number of optimizations including memory and disk caching, downsampling the image in memory, automatically pausing/cancelling requests, and more.
- **Lightweight**: Coil adds ~2000 methods to your APK (for apps that already use OkHttp and Coroutines), which is comparable to Picasso and significantly less than Glide and Fresco.
- **Easy to use**: Coil's API leverages Kotlin's language features for simplicity and minimal boilerplate.
- **Modern**: Coil is Kotlin-first and uses modern libraries including Coroutines, OkHttp, Okio, and AndroidX Lifecycles.

Coil is an acronym for: **Co**routine **I**mage **L**oader.

Made with ❤️ at [Instacart](https://www.instacart.com). Translations: [한국어](README-ko.md), [中文](README-zh.md), [Türkçe](README-tr.md)

## Download

Coil is available on `mavenCentral()`.

```kotlin
implementation("io.coil-kt:coil:2.0.0-rc02")
```

## Quick Start

#### ImageViews

To load an image into an `ImageView`, use the `load` extension function:

```kotlin
// URL
imageView.load("https://www.example.com/image.jpg")

// File
imageView.load(File("/path/to/image.jpg"))

// And more...
```

Requests can be configured with an optional trailing lambda:

```kotlin
imageView.load("https://www.example.com/image.jpg") {
    crossfade(true)
    placeholder(R.drawable.image)
    transformations(CircleCropTransformation())
}
```

#### Jetpack Compose

Import the [Jetpack Compose](https://developer.android.com/jetpack/compose) extension library:

```kotlin
implementation("io.coil-kt:coil-compose:2.0.0-rc02")
```

To load an image, use the `AsyncImage` composable:

```kotlin
AsyncImage(
    model = "https://example.com/image.jpg",
    contentDescription = null
)
```

#### Image Loaders

Both `imageView.load` and `AsyncImage` use the singleton `ImageLoader` to execute image requests. The singleton `ImageLoader` can be accessed using a `Context` extension function:

```kotlin
val imageLoader = context.imageLoader
```

`ImageLoader`s are designed to be shareable and are most efficient when you create a single instance and share it throughout your app. That said, you can also create your own `ImageLoader` instance(s):

```kotlin
val imageLoader = ImageLoader(context)
```

If you do not want the singleton `ImageLoader`, depend on `io.coil-kt:coil-base` instead of `io.coil-kt:coil`.

#### Requests

To load an image into a custom target, `enqueue` an `ImageRequest`:

```kotlin
val request = ImageRequest.Builder(context)
    .data("https://www.example.com/image.jpg")
    .target { drawable ->
        // Handle the result.
    }
    .build()
val disposable = imageLoader.enqueue(request)
```

To load an image imperatively, `execute` an `ImageRequest`:

```kotlin
val request = ImageRequest.Builder(context)
    .data("https://www.example.com/image.jpg")
    .build()
val drawable = imageLoader.execute(request).drawable
```

Check out Coil's [full documentation here](https://coil-kt.github.io/coil/getting_started/).

## Requirements

- Min SDK 21+
- [Java 8+](https://coil-kt.github.io/coil/faq/#how-do-i-target-java-8)

## R8 / Proguard

Coil is fully compatible with R8 out of the box and doesn't require adding any extra rules.

If you use Proguard, you may need to add rules for [Coroutines](https://github.com/Kotlin/kotlinx.coroutines/blob/master/kotlinx-coroutines-core/jvm/resources/META-INF/proguard/coroutines.pro), [OkHttp](https://github.com/square/okhttp/blob/master/okhttp/src/jvmMain/resources/META-INF/proguard/okhttp3.pro) and [Okio](https://github.com/square/okio/blob/master/okio/src/jvmMain/resources/META-INF/proguard/okio.pro).

## License

    Copyright 2021 Coil Contributors

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       https://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
