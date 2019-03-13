# Sample Snapshot Test Framework - iOS only

### View-based testing

*View-based testing* means verifying that what the user sees is exactly
what we ( as developers ) want them to see. Thanks to this testing we
can guarantee that in different states or versions, our views are shown
as expected.

### Snapshot Test. How does it work?

The snapshot test takes a capture of a *UIView* or *CALayer* and uses
the *renderInContext* *method*which makes a capture of the view and
compares it with the reference image stored in our repository. The test
fails if both images do not match and deliver a third capture showing
the differences.

  

**Sample Project: Qantas iOS Mobile App:**

<https://stash.qcpaws.qantas.com.au/projects/AMS04-A868/repos/ios/browse>

### Configuration

The library was created by Facebook (FBSnapshotTestCase) and has now
been renamed to *iOSSnapshotTestCase* and is maintained by uber.

The first step, as they explain on their [Github
page](https://github.com/uber/ios-snapshot-test-case), is to add the
library to our Podfile.

Then we edit the scheme of our target to add the directory where our
reference captures will be saved. To do this we add an environment
variable with the key *FB\_REFERENCE\_IMAGE\_DIR.*

[![spanshot
testing](https://apiumhub.com/wp-content/uploads/2018/07/Picture1-3.png){.alignnone
.size-full .wp-image-60281 width="975"
height="450"}](https://apiumhub.com/wp-content/uploads/2018/07/Picture1-3.png)

 

Optionally we can also add the key *IMAGE\_DIFF\_DIR* to indicate the
directory where the differential captures that will be generated, will
be saved in case our tests fail.

 

### Implementation

To see the implementation we will test a simple *viewcontroller* that
will change the visual aspect depending on a state.

[![ios testing
implementation](https://apiumhub.com/wp-content/uploads/2018/07/Picture2.png){.alignnone
.size-full .wp-image-60286 width="284"
height="127"}](https://apiumhub.com/wp-content/uploads/2018/07/Picture2.png)

 The view of the two states:

[![snapshot testing
configuration](https://apiumhub.com/wp-content/uploads/2018/07/Screen-Shot-2018-07-15-at-16.53.50.png){.alignnone
.size-full .wp-image-60287 width="1072"
height="954"}](https://apiumhub.com/wp-content/uploads/2018/07/Screen-Shot-2018-07-15-at-16.53.50.png)

We configure our test class by making it a subclass
of *FBSnapshotTestCase* instead of *XCTestCase*.

We define our tests by instantiating the ViewController, assigning the
status and calling the *FBSnapshotVerifyView* method.

[![viewController
ios](https://apiumhub.com/wp-content/uploads/2018/07/Picture3.png){.alignnone
.size-full .wp-image-60288 width="875"
height="495"}](https://apiumhub.com/wp-content/uploads/2018/07/Picture3.png)

First of all, we must execute the tests with the *recordMode* activated
to save the reference images. For this we introduce inside the method of
setUp () recordMode = true.

[![recordmode
ios](https://apiumhub.com/wp-content/uploads/2018/07/Picture4.png){.alignnone
.size-full .wp-image-60289 width="305"
height="127"}](https://apiumhub.com/wp-content/uploads/2018/07/Picture4.png)

When executing the tests with recordMode activated, Fail will exit. It
is normal because you do not have another image yet with which to make
the comparison.

[![recordmode ios
test](https://apiumhub.com/wp-content/uploads/2018/07/Picture5.png){.alignnone
.size-full .wp-image-60290 width="1103"
height="45"}](https://apiumhub.com/wp-content/uploads/2018/07/Picture5.png)

Then we comment or eliminate the line of *recordMode* to launch the
tests again and see what happens.

From now on, if the visual aspect of the view changes in the wrong way,
our tests will notify us about this issue.

For example, if we inadvertently change the dimension of the icons, the
test will generate a differential image with the changes.

[![icon mobile app
ios](https://apiumhub.com/wp-content/uploads/2018/07/Picture6.png){.alignnone
.size-full .wp-image-60291 width="296"
height="527"}](https://apiumhub.com/wp-content/uploads/2018/07/Picture6.png)

I have increased the size of the icon for the 20px test, and the change
can be seen in the image.

 

### Run views in an isolated way

Thanks to the snapshot testing and to having the uncoupled views, we can
instantiate and execute a certain ViewController in the simulator. It is
very useful for accelerating the process of views creation and thus
reducing development time.

In our *didFinishLaunchingWithOptions* we check if we are running tests
and in that case, we assign the flat and empty *UIViewController* to
the *rootViewController*.

[![doing ios testing mobile
app](https://apiumhub.com/wp-content/uploads/2018/07/Picture7.png){.alignnone
.size-full .wp-image-60292 width="816"
height="251"}](https://apiumhub.com/wp-content/uploads/2018/07/Picture7.png)

In our test class, we use an *XCTWaiter* with a high timeout and assign
the controller to the *rootViewController* to execute.

[![rootViewController](https://apiumhub.com/wp-content/uploads/2018/07/Picture8.png){.alignnone
.size-full .wp-image-60293 width="736"
height="565"}](https://apiumhub.com/wp-content/uploads/2018/07/Picture8.png)

Finally, in the test we call the *debugViewController* method.

[![](https://apiumhub.com/wp-content/uploads/2018/07/Picture9.png){.alignnone
.size-full .wp-image-60294 width="975"
height="160"}](https://apiumhub.com/wp-content/uploads/2018/07/Picture9.png)

In this way, we can execute the typical view that is within a long flow
of screens of our app in a simple way.
