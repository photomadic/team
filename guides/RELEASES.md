Release Process
==


#### iOS

All iOS releases are done using an Enterprise developer account which means that
we don't push directly to the App Store. However, the release process is very
similar and is managed through Xcode:

1. Open the project in Xcode
2. Make sure that the bundle version string and number have been bumped for this
   release. Both should follow Semver guidelines with the bundle version string
   representing a major/minor version number and the bundle version representing
   the patch number.
3. In the menu go to **Product > Archive**
4. Once finished, the Organizer window should open automatically with the new
   build already selected. On the right side of this window select **Export...**
5. Select **Save for Enterprise Deployment**
6. The next screen will prompt you to select the development team for code
   signing. Verify that **Photomadic, LLC** is selected on this screen.
7. Select **Export one app for all compatible devices**
8. The next screen will confirm the settings with a preview of the build. Make
   sure to *disable* the option **Rebuild from bitcode** which is automatically
   selected by default.
9. Fill in all fields of the Distribution Manifest Information screen. The
   exact URL will depend on the app being deployed but can be pulled from either
   Google or Amazon storage consoles. Click **Export**

Xcode will export both an `.ipa` and `.plist` file to the directory you specify.
Both of these files should be uploaded to their respective buckets in order to
finalize the release.
