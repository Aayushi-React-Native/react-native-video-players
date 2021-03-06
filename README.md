# react-native-video-players

## Getting started

`$ npm install react-native-video-players --save`

### Mostly automatic installation

`$ react-native link react-native-video-players`

<p align="left">

 <img  width="150" height="300" src="https://github.com/codiant-technology/react-native-video-players/blob/main/assets/IMG_03.png">
  <img  width="150" height="300" src="https://github.com/codiant-technology/react-native-video-players/blob/main/assets/IMG_04.png">
   <img  width="150" height="300" src="https://github.com/codiant-technology/react-native-video-players/blob/main/assets/IMG_01.PNG">
   <br/>
   <img  width="430" height="200" src="https://github.com/codiant-technology/react-native-video-players/blob/main/assets/IMG_02.png">
  </p>
  
## Usage
```javascript
import VideoPlayers from 'react-native-video-players';
onst styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center'
  }
})

const url = ['https://your-url.com/video.mp4']

class VideoExample extends React.Component {

  render() {
    return (
      <View style={styles.container}>
       <VideoPlayers
        source={{
          uri: url,
        }}
        title={'Video title'}
        favorite={favorite}
        paused={paused}
        
        resizeMode={'contain'}
        playInBackground={true}
        playWhenInactive={true}
        
        isSettingShow={true}
        
        controlTimeout={2000}
      />
      </View>
    )
  }
}

AppRegistry.registerComponent('VideoExample', () => VideoExample)

```
##  A customisable React Native video player for Android and IOS



## Features

* Fullscreen support for Android and iOS!
* Works with react-navigation
* Optional action button for custom use
* Add your own logo and/or placeholder
* support Potrait and Landscape mode
* background video/audio play  supports
* music-controls on notification bar  when app is not active

## Install

```shell
npm i  react-native-video-player --save
npm i react-native-keep-awake --save
npm i react-native-music-control --save
npm i react-native-orientation --save
npm i react-native-svg --save
npm i react-native-video --save
```

##  Add the android.permission.FOREGROUND_SERVICE permission to your AndroidManifest.xml


<uses-permission android:name="android.permission.FOREGROUND_SERVICE" />


Then follow the instructions for your platform to link react-native-video into your project:

### iOS installation
<details>
  <summary>iOS details</summary>

#### Standard Method

**React Native 0.60 and above**

Run `npx pod-install`. Linking is not required in React Native 0.60 and above.

**React Native 0.59 and below**

Run `react-native link react-native-video` to link the react-native-video library.

#### Using CocoaPods (required to enable caching)

Setup your Podfile like it is described in the [react-native documentation](https://facebook.github.io/react-native/docs/integration-with-existing-apps#configuring-cocoapods-dependencies). 

Depending on your requirements you have to choose between the two possible subpodspecs:

Video only:

```diff
  pod 'Folly', :podspec => '../node_modules/react-native/third-party-podspecs/Folly.podspec'
+  `pod 'react-native-video', :path => '../node_modules/react-native-video/react-native-video.podspec'`
end
```

Video with caching ([more info](docs/caching.md)):

```diff
  pod 'Folly', :podspec => '../node_modules/react-native/third-party-podspecs/Folly.podspec'
+  `pod 'react-native-video/VideoCaching', :path => '../node_modules/react-native-video/react-native-video.podspec'`
end
```

</details>



### Android installation
<details>
  <summary>Android details</summary>
 
Linking is not required in React Native 0.60 and above.
If your project is using React Native < 0.60, run `react-native link react-native-video` to link the react-native-video library.

Or if you have trouble, make the following additions to the given files manually:

#### **android/settings.gradle**

The newer ExoPlayer library will work for most people.

```gradle
include ':react-native-video'
project(':react-native-video').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-video/android-exoplayer')
```

If you need to use the old Android MediaPlayer based player, use the following instead:

```gradle
include ':react-native-video'
project(':react-native-video').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-video/android')
```

#### **android/app/build.gradle**

From version >= 5.0.0, you have to apply these changes:

```diff
dependencies {
   ...
    compile project(':react-native-video')
+   implementation "androidx.appcompat:appcompat:1.0.0"
-   implementation "com.android.support:appcompat-v7:${rootProject.ext.supportLibVersion}"

}
```

#### **android/gradle.properties**

Migrating to AndroidX (needs version >= 5.0.0):

```gradle.properties
android.useAndroidX=true
android.enableJetifier=true
```

#### **MainApplication.java**

On top, where imports are:

```java
import com.brentvatne.react.ReactVideoPackage;
```

Add the `ReactVideoPackage` class to your list of exported packages.

```java
@Override
protected List<ReactPackage> getPackages() {
    return Arrays.asList(
            new MainReactPackage(),
            new ReactVideoPackage()
    );
}
```
</details>


## Notes 

### iOS installation
<details>

<summary>iOS details</summary>

To get audio/video in IOS when app is in background


From x-code  in capabilities add background modes and enable audio mode.


Also  add  following entries to get orientation in landscape :-


Add this lines into appDelegate.m file.
```
#import "Orientation.h"

- (UIInterfaceOrientationMask)application:(UIApplication )application supportedInterfaceOrientationsForWindow:(UIWindow )window {
  return [Orientation getOrientation];
}
```

</details>


## Props

Prop                  | Type     | Required | Default                   | Description
--------------------- | -------- | -------- | ------------------------- | -----------
url                   | string, number | Yes |                          | A URL string (or number for local) is required.
autoPlay              | bool     | No       | false                     | Autoplays the video as soon as it's loaded
loop                  | bool     | No       | false                     | Allows the video to continuously loop
title                 | string   | No       | ''                        | Adds a title of your video at the top of the player
placeholder           | string   | No       | undefined                 | Adds an image placeholder while it's loading and stopped at the beginning
theme                 | string   | No       | 'white'                   | Adds an optional theme colour to the players controls
hideFullScreenControl | bool     | No       | false                     | This hides the full screen control
style                 | number, object | No | {}                        | Apply styles directly to the Video player (ignored in fullscreen mode)
resizeMode            | string   | No       | 'contain'                 | Fills the whole screen at aspect ratio. contain, cover etc
rotateToFullScreen    | bool     | No       | false                     | Tapping the fullscreen button will rotate the screen. Also rotating the screen will automatically switch to fullscreen mode
fullScreenOnly        | bool     | No       | false                     | This will play only in fullscreen mode
isRepeat              | bool     | No      | false                     | This is to active repeat play of a single video.
playInBackground      | bool     | No       | false                     | Audio continues to play when app enters background.
playWhenInactive      | bool     | No       | false                     | [iOS] Video continues to play when control or notification center are shown.
onMorePress           | function | No       | undefined                 | Adds an action button at the top right of the player. Use this callback function for your own use. e.g share link
onFullScreen          | function | No       | (value) => {}             | Returns the fullscreen status whenever it toggles. Useful for situations like react navigation.
lockPortraitOnFsExit  | bool     | No       | false                     | Keep Portrait mode locked after Exiting from Fullscreen mode
onLoad                | function | No       | (data) => {}              | Returns data once video is loaded
onProgress            | function | No       | (progress) => {}          | Returns progress data
onEnd                 | function | No       | () => {}                  | Invoked when video finishes playing  
onError               | function | No       | (error) => {}             | Returns an error message argument
onPlay                | function | No       | (playing) => {}           | Returns a boolean during playback
error                 | boolean, object | No | true                     | Pass in an object to Alert. See https://facebook.github.io/react-native/docs/alert.html
theme                 | object   | No       | all white                 | Pass in an object to theme. (See example below to see the full list of available settings)
controlDuration             | number   | No       | 3                 | Set the visibility time of the pause button and the progress bar after the video was started
