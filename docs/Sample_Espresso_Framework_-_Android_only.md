# Sample Espresso Framework - Android only

## **Overview**

Use Espresso to write concise, beautiful, and reliable Android UI tests.

The following code snippet shows an example of an Espresso test:

    @Testpublic void greeterSaysHello() {    onView(withId(R.id.name_field)).perform(typeText("Davo"));    onView(withId(R.id.greet_button)).perform(click());    onView(withText("Hello there!")).check(matches(isDisplayed()));}

The core API is small, predictable, and easy to learn and yet remains
open for customization. Espresso tests state expectations, interactions,
and assertions clearly without the distraction of boilerplate content,
custom infrastructure, or messy implementation details getting in the
way.

Espresso tests run optimally fast! It lets you leave your waits, syncs,
sleeps, and polls behind while it manipulates and asserts on the
application UI when it is at rest.

The Espresso API encourages test authors to think in terms of what a
user might do while interacting with the application - locating UI
elements and interacting with them. At the same time, the framework
prevents direct access to activities and views of the application
because holding on to these objects and operating on them off the UI
thread is a major source of test flakiness. Thus, you will not see
methods like `getView()` and `getCurrentActivity()` in the Espresso API.
You can still safely operate on views by implementing your own
subclasses of `ViewAction` and `ViewAssertion`.

## **Sample project - Qantas Mobile App Android project :**

<https://stash.qcpaws.qantas.com.au/projects/AMS04-A868/repos/android/browse>

As a part of source code Espresso tests are integrated with Android
code.

## **How to write your tests :**

### Set up your test environment

To avoid flakiness, we highly recommend that you turn off system
animations on the virtual or physical devices used for testing. On your
device, under **Settings &gt; Developer options**, disable the following
3 settings:

-   Window animation scale
-   Transition animation scale
-   Animator duration scale

### Add Espresso dependencies

To add Espresso dependencies to your project, complete the following
steps:

1.  Open your app’s `build.gradle` file. This is usually not the
    top-level `build.gradle` file but `app/build.gradle`.
2.  Add the following lines inside dependencies:

<!-- -->

    androidTestImplementation 'androidx.test.espresso:espresso-core:3.1.0'androidTestImplementation 'androidx.test:runner:1.1.0'androidTestImplementation 'androidx.test:rules:1.1.0'

[View the complete set of Gradle
dependencies](https://developer.android.com/studio/build/dependencies).

### **Set the instrumentation runner**

Add to the same `build.gradle` file the following line
in `android.defaultConfig`:

    testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"

### Example Gradle build file

    apply plugin: 'com.android.application'android {    compileSdkVersion 28    defaultConfig {        applicationId "com.my.awesome.app"        minSdkVersion 15        targetSdkVersion 28        versionCode 1        versionName "1.0"        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"    }}dependencies {    androidTestImplementation 'androidx.test:runner:1.1.0'    androidTestImplementation 'androidx.test.espresso:espresso-core:3.1.0'}

### Perform an action on a view

When you have found a suitable matcher for the target view, it is
possible to perform instances of `ViewAction` on it using the perform
method.

For example, to click on the view:

    onView(...).perform(click())

### Check view assertions

Assertions can be applied to the currently selected view with
the `check()` method. The most used assertion is
the `matches()` assertion. It uses a `ViewMatcher` object to assert the
state of the currently selected view.

For example, to check that a view has the text `"Hello!"`:

    onView(...).check(matches(withText("Hello!")))

### Add the first test

Android Studio creates tests by default
in `src/androidTest/java/com.example.package/`.

Example JUnit4 test using Rules:

  

    @RunWith(AndroidJUnit4::class)@LargeTestclass HelloWorldEspressoTest {    @get:Rule    val activityRule = ActivityTestRule(MainActivity::class.java)    @Test fun listGoesOverTheFold() {        onView(withText("Hello world!")).check(matches(isDisplayed()))    }}

### Run tests

You can run your tests in Android Studio or from the command line.

### In Android Studio

To create a test configuration in Android Studio, complete the following
steps:

1.  Open **Run &gt; Edit Configurations**.
2.  Add a new Android Tests configuration.
3.  Choose a module.
4.  Add a specific instrumentation
    runner: `androidx.test.runner.AndroidJUnitRunner`
5.  Run the newly created configuration.

### From the command line

Execute the following Gradle command:

    ./gradlew connectedAndroidTest

### Debugging

Espresso provides useful debugging information when a test fails:

### Logging

Espresso logs all view actions to logcat. For example:

    ViewInteraction: Performing 'single click' action on view with text: Espresso

### Analytics

In order to make sure we are on the right track with each new release,
the test runner collects analytics. More specifically, it uploads a hash
of the package name of the application under test for each invocation.
This allows us to measure both the count of unique packages using
Espresso as well as the volume of usage.

If you do not wish to upload this data, you can opt out by including
the `disableAnalytics` argument in your instrumentation command:

    adb shell am instrument -e disableAnalytics true

  
