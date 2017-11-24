# GIFView
GIFView is a library for showing GIFs in applications.

## Setup

In your project's build.gradle file:
```
allprojects {
    repositories {
        ...
        maven { 
            url "https://jitpack.io"
        }
        ...
    }
}
```
In your Application's or Module's build.gradle file:
```
dependencies {
    ...
    compile 'com.github.Gavras:GIFView:v1.1'
    ...
}
```
## XML Attributes:
 
 starting_on_init:
 A boolean that represents if the view starts the gif
 when its initialization finishes or not. Default is true.
 
 on_click_start_or_pause:
 If sets to true, every click toggles the state of the gif.
 If the gif is showing stops the gif, and if the gif is not showing starts it.
 If sets to false clicking the gif does nothing. Default is false.
 
 delay_in_millis:
 A positive integer that represents how many milliseconds
 should pass between every calculation of the next frame to be set. Default is 33.
 
 gif_src:
 A string that represents the gif's source.
 
 - If you want to get the gif from a url
 concatenate the string "url:" with the full url.
 
 - if you want to get the gif from the assets directory
 concatenate the string "asset:" with the full path of the gif
 within the assets directory. You can exclude the .gif extension.
 
 for example if you have a gif in the path "assets/ex_dir/ex_gif.gif"
 the string should be: "asset:ex_dir/ex_gif"

## Code Example

From XML:
```xml
<com.whygraphics.gifview.gif.GIFView xmlns:gif_view="http://schemas.android.com/apk/res-auto"
        android:id="@+id/main_activity_gif_vie"
        android:layout_width="200dp"
        android:layout_height="200dp"
        android:scaleType="center"
        gif_view:gif_src="url:http://pop.h-cdn.co/assets/16/33/480x264/gallery-1471381857-gif-season-2.gif" />
```

In the activity:
```java
GIFView mGifView = (GIFView) findViewById(R.id.main_activity_gif_vie);
        
mGifView.setOnSettingGifListener(new GIFView.OnSettingGifListener() {
            @Override
            public void onSuccess(GIFView view, Exception e) {
                Toast.makeText(MainActivity.this, "onSuccess()", Toast.LENGTH_SHORT).show();
            }

            @Override
            public void onFailure(GIFView view, Exception e) {

            }
});
```

Setting the gif programmatically:
```java
mGifView.setGifResource("asset:gif1");
```

## File Caching

GIFView is caching all GIF files it downloads when being provided with an URL to an image. If an
InputStream is used, no caching is performed.

The caching works as follows:

The GIFView initializes the GIFCache class with the URL provided by the caller. The GIFCache
class now checks for the existence of the sub-directory "GIFView" within the app's own
cache-directory. If that is not found, it will be created and the GIF-image will be downloaded
into it. If it does exist, the existence of the GIF-image is checked, and if found, the
cached-version will be provided. If the image is not found, it will be downloaded and then the
cached file will be used.

In order to clear the cached files programmatically, GIFCache offers the possibility to retrieve
the folder as a java.io.File object by calling the static method getCacheSubDir():

```java
File GIFCache.getCacheSubDir(Context context);
```
