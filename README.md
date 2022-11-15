# Example fabric library with custom cpp state implementation

## Description

Probably you will not need this template, since fabric is responsible for whole synchronous measurements under the hood. But in some cases, your native component would like to update its frames in synchronous [way](https://reactnative.dev/architecture/render-pipeline). Right now, codegen does not support generating a new state based on typescript implementation, hence custom state implementation must be added manually. Linking custom cpp can be tricky, so together with [@cortinico](https://github.com/cortinico) we prepared a showcase, so you can reuse this approach in your library.

More context you can find [here](https://github.com/reactwg/react-native-new-architecture/discussions/71#discussioncomment-3606598)

## How to generate shared cpp code

- run [codegen](https://reactnative.dev/docs/new-architecture-library-android#1-extend-or-implement-the-code-generated-native-interfaces) `./gradlew generateCodegenArtifactsFromSchema` in android folder
- copy everything under `build/generated/source/codegen/jni/react/renderer/components/yourlib` into cpp folder
- pass `interfaceOnly`
- implement cpp state

## How to link custom cpp state in RN 70?

### Android

Here you can see how to make it:
Instead of `AndroidMkPath` , please add `CMakePath` to react-native.config.js

### iOS

Replace `s.source_files = "ios/**/*.{h,m,mm}"` with `s.source_files = "ios/**/*.{h,m,mm}", "cpp/**/*.{h,cpp}"` inside `yourLib.podspec` file and change imports inside `.mm`.
