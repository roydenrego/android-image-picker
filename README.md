## ImagePicker

[![Android Arsenal](https://img.shields.io/badge/Android%20Arsenal-ImagePicker-brightgreen.svg?style=flat)](https://android-arsenal.com/details/1/4618)

A simple library to select images from the gallery and camera.

## Screenshot

<img src="https://raw.githubusercontent.com/esafirm/android-image-picker/master/art/ss.gif" height="460" width="284"/>

## Download [![](https://jitpack.io/v/roydenrego/android-image-picker.svg)](https://jitpack.io/#esafirm/android-image-picker)

Add this to your project's `build.gradle`

```groovy
allprojects {
    repositories {
        maven { url "https://jitpack.io" }
    }
}
```

And add this to your module's `build.gradle` 

```groovy
dependencies {
	implementation 'com.github.roydenrego:android-image-picker:x.y.z'
	// If you have a problem with Glide, please use the same Glide version or simply open an issue
	implementation 'com.github.bumptech.glide:glide:4.5.0'
}
```

change `x.y.z` to version in the [release page](https://github.com/roydenrego/android-image-picker/releases)

**Breaking changes**

If you're not using custom image loader and have Glide v3 in your classpath, please using version `1.8.0` below! 
Will improve this image loader compatibility issue in ImagePicker v2! 

## Usage

For full example, please refer to `sample`

### Start image picker activity

The simplest way to start 

```java
ImagePicker.create(this) // Activity or Fragment
	    .start();
``` 

Complete features of what you can do with ImagePicker

```java
ImagePicker.create(this)
	.returnMode(ReturnMode.ALL) // set whether pick and / or camera action should return immediate result or not.
	.folderMode(true) // folder mode (false by default)
	.toolbarFolderTitle("Folder") // folder selection title
	.toolbarImageTitle("Tap to select") // image selection title
	.toolbarArrowColor(Color.BLACK) // Toolbar 'up' arrow color
	.single() // single mode
	.multi() // multi mode (default mode)
	.limit(10) // max images can be selected (99 by default)
	.showCamera(true) // show camera or not (true by default)
	.imageDirectory("Camera") // directory name for captured image  ("Camera" folder by default)
	.origin(images) // original selected images, used in multi mode
	.exclude(images) // exclude anything that in image.getPath()
	.excludeFiles(files) // same as exclude but using ArrayList<File>
	.theme(R.style.CustomImagePickerTheme) // must inherit ef_BaseTheme. please refer to sample
	.enableLog(false) // disabling log
	.imageLoader(new GrayscaleImageLoder()) // custom image loader, must be serializeable
	.start(); // start image picker activity with request code
```                

If you want to call it outside `Activity` or `Fragment`, you can simply get the `Intent` from the builder

```java
ImagePicker.create(activity).getIntent(context)

```

### Receive result

```java
  @Override
    protected void onActivityResult(int requestCode, final int resultCode, Intent data) {
        if (ImagePicker.shouldHandle(requestCode, resultCode, data)) {
			// Get a list of picked images
			List<Image> images = ImagePicker.getImages(data)
            // or get a single image only
			Image image = ImagePicker.getFirstImageOrNull(data)
        }
        super.onActivityResult(requestCode, resultCode, data);
    }
```


### Camera Only

```java
ImagePicker.cameraOnly().start(activity) // Could be Activity, Fragment, Support Fragment 

// You could also get the Intent 
ImagePicker.cameraOnly().getIntent(context)
```

You also still can use the `DefaultCameraModule` but discouraged to do it. 


## Modification License

```
Copyright (c) 2016 Esa Firman

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```

## Original License

[Forked from esafirm/android-image-picker](https://github.com/esafirm/android-image-picker)

[The Original Image Picker](https://github.com/nguyenhoanglam/ImagePicker)

[You can find the original lincense here ](https://raw.githubusercontent.com/esafirm/ImagePicker/master/ORIGINAL_LICENSE) 


