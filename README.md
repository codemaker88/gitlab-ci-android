# gitlab-ci-android-ndk

- add apt-get install file
- add sdkmanager install ndk & cmake

docker hub : [codemaker88/gitlab-ci-android-ndk:1.0.0](https://hub.docker.com/r/codemaker88/gitlab-ci-android-ndk)

forked from [jangrewe/gitlab-ci-android](https://github.com/jangrewe/gitlab-ci-android)

# gitlab-ci-android
This Docker image contains the Android SDK and most common packages necessary for building Android apps in a CI tool like GitLab CI. Make sure your CI environment's caching works as expected, this greatly improves the build time, especially if you use multiple build jobs.

A `.gitlab-ci.yml` with caching of your project's dependencies would look like this:

```
image: jangrewe/gitlab-ci-android

stages:
- build

before_script:
- export GRADLE_USER_HOME=$(pwd)/.gradle
- chmod +x ./gradlew

cache:
  key: ${CI_PROJECT_ID}
  paths:
  - .gradle/

build:
  stage: build
  script:
  - ./gradlew assembleDebug
  artifacts:
    paths:
    - app/build/outputs/apk/app-debug.apk
```
