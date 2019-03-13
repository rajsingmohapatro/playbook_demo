# Web Applications

### Web Automated Testing

In Web Application Testing, we are typically using a browser (the
client) to request a website from a web server by communicating with the
server over HTTP or HTTPS.

It is important that, as testers, when we are involved in Web Testing,
we should be familiar with the basics of HTTP to get a good understanding of how web applications work.

Most web applications work in an agile development model with frequent
releases, hence a need for frequent testing. In Web Testing, Test Automation can be of great benefit because it removes the burden of
repetitive work.

As well as verifying functionality, we can also use automated scripts to
generate test data that we need during Web Testing.

Another way automation can help in manual testing is tools can take
screenshots of the actual browser page or record the test duration. If
we need to visually check for a large number of pages, e.g. we want to know how the localised text renders on different webpages, we can use the tool to go through the pages and take screenshots and then quickly verify visually.

### Cross-browser Web Testing

As there are different number of browsers, we need to ensure our web
application works as expected on all of them (at least the major ones,
i.e. Google Chrome, Mozilla Firefox and Microsoft Internet Explorer),
not to forget Opera and Safari.

As with all testing, we need to know which browsers and their versions
the application supports and then plan the testing accordingly.

Testing everything on every browser can be very time consuming, hence we
can use automated tools to verify functionality on different browsers.

Moreover, there are online cross browser testing tools which make life
easier for testers to execute their tests on different browsers.

The number of browser-related issues are very few and mostly related to
very old versions of browsers or the CSS doesn’t render properly giving
layout issues.

Therefore it may not be necessary to run all test cases in all browsers
as it can be very time consuming (even when automated) for very little
gain, and chance of something not working in very low.

The best approach is to run all the test cases in one major browser, and
then select a handful of most important scenarios and run them on the
rest of the browsers.

### Analysing HTTP Traffic

Quite often there is a need to analyse the HTTP traffic from the browser to the downstream servers. By analysing the web traffic we can dig down to the details of each request and response.

In Web Testing, analysing HTTP traffic  is particularly useful when
testing third party tracking tags, such as Google Analytics tags or
omnivore tags on webpages.

Not only can we verify the tags hold correct values, we can actually
test that the requests are fired off to the appropriate third party
systems and that we get a valid response, usually 200 OK response code.

In order to be able to visualise and record HTTP traffic we have to use
an appropriate tool that acts as a proxy and can listen to the requests
and responses between the client, usually a browser, and the servers.

Here are some of the most popular tools we can use to analyse HTTP
traffic:

**Wireshark** if you want to see everything going on in the network.

**Fiddler** if you want to just monitor HTTP/s traffic.

**Live HTTP Headers** if you’re in Firefox and want a quick plugin just
to see the headers.

**FireBug/Chrome Dev tools** can get you that information too and
provides a nice interface when your working on a single page during
development. I’ve used it to monitor AJAX transactions.

**BrowserMob Proxy **is also a very nice tool that can hook with
Selenium WebDriver when running automated tests.

### Responsive Websites and Mobile Testing

More and more people are accessing websites from their mobile
phones than their desktop computers. This means that Web Testing is no
longer restricted to browsers on desktops. We now have to test web
applications on mobile platforms as well as desktops.

There are two types of web applications for mobile devices, ones which are purposely developed for mobile platforms, and ones which are
“responsive”, i.e. there is only one version of the web application
built for desktop and mobile devices but the application renders and is
displayed differently depending on the size of the device.

Both types require testing on mobile devices and/or simulators.

For more information on Web Testing on Mobiles read How to Test
Responsive Web Design

### Accessibility Automation Testing

Accessibility is one of those things we all wish we were better at. It
can lead to a bunch of questions like: how do we make our site better?
How do we test what we have done? Should we spend time each day going
through our site to check everything by hand? Or just hope that everyone
on our team has remembered to check their changes are accessible?

This is where automated accessibility tests can come in. We can set up
automated tests and have them run whenever someone makes a pull request,
and even alongside end-to-end tests, too.

Automated tests can’t cover everything however; only 20 to 50% of
accessibility issues can be detected automatically. For example, we
can’t yet automate the comparison of an `alt` attribute with an image’s
content, and there are some screen reader tests that need to be carried
out by hand too. To ensure our site is as accessible as possible, we
will still need to carry out manual tests

### Important elements for Web Testing

During Web Testing, as well as functional testing, we also need to check for and not limited to:

-   Javascript
-   CSS
-   Cookies
-   Accessibility
-   Dead-links
-   UX and Layout
-   HTML Validity
-   Security
-   Browser Refresh
-   Window Resizing
