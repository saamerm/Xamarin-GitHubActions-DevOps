# Xamarin-GitHubActions-DevOps
 This repo contains the result of my work combining GitHub Actions with Xamarin to Automatically Build iOS & Android apps

You can take a look at the article [here](https://levelup.gitconnected.com/using-github-actions-with-ios-and-android-xamarin-apps-693a93b48a61?source=friends_link&sk=cd81773f2e5a5931ae49c9362b4db795) that has more details. It will also give you a better understanding of what you see in the Actions folder.

Also, here's a short snippet of what to do [for GitLab](https://stackoverflow.com/questions/42757115/has-anyone-successfully-built-xamarin-forms-with-gitlab-ci/63233029#63233029)

## Where's the file published? 

Right now, the file is published as an "artifact" ZIP file https://github.com/actions/upload-artifact/issues/3 and can be found below your successful Action, as you can see here
<img width="871" alt="image" src="https://user-images.githubusercontent.com/8262287/116001770-38336f00-a5c4-11eb-8857-9121c3f5774e.png">


### Build you Android code & Publish the Signed APK from the build

If you want to build and publish the APK, simply copy this into your repository's .github/workflows/main.yml file.
Make sure to change Blank in all instances with your own Project/Solution name and change "com.tfp.blank" with the bundle identifier mentioned in your AndroidManifest file.

```
name: CI on Push and Pull Request
on: [push, pull_request]
jobs:
  Android:
    runs-on: macos-latest    
    steps:
    - uses: actions/checkout@v1      
    - name: Android
      run: |
        cd Blank
        nuget restore
        msbuild Blank.Android/Blank.Android.csproj /verbosity:normal /t:Rebuild /t:PackageForAndroid /t:SignAndroidPackage /p:Configuration=Debug 
    - uses: actions/upload-artifact@v2
      with:
        name: Android App
        path: Blank/Blank.Android/bin/Debug/com.tfp.blank-Signed.apk        
```

### Build you iOS code & Publish the simulator APP from the build

If you want to build and publish the simulator APP file, simply copy this into your repository's .github/workflows/main.yml file.
Make sure to change Blank in all instances with your own Project/Solution name.

```
name: CI on Push and Pull Request
on: [push, pull_request]
jobs:
  iOS:
    runs-on: macos-latest    
    steps:
    - name: Checkout repository
      uses: actions/checkout@v2        
    - name: iOS Simulator
      run: |
        cd Blank
        nuget restore
        msbuild Blank/Blank.iOS/Blank.iOS.csproj /verbosity:normal /t:Rebuild /p:Platform=iPhoneSimulator /p:Configuration=Debug        
    - uses: actions/upload-artifact@v2
      with:
        name: iOS Simulator App
        path: Blank/Blank.iOS/bin/iPhoneSimulator/Debug/Blank.iOS.app        
```
