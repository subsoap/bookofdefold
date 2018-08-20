# Bundling Projects

When you need to test builds on devices, or your project is ready to release to the public, you will want to make platform specific build bundles of your project. Before you do, make sure you have the correct settings for each target platform setup in your game.project file. Defold will attempt to use builtin defaults where it can, but for some targets you will need to setup certain files such as certificates, provisioning profiles, and, in the case of iOS, launch screen images to properly run.

To make bundled builds go to Project -&gt; Bundle -&gt; and then pick the platform which you intend to make a build for.

For each platform, you’ll be shown a dialog box to confirm more information.

By checking “Release mode” your build will have less of the debug features enabled \(as of this writing, if you are using a Native Extension this release mode checkbox does not work, you must also use an appmanifest file to specify a true release mode build\). When publishing builds publicly this is generally an option you want enabled. By checking “Generate build report” a report.html file will be made which details all of the drive space usage of all of the resources of your project. Use this information to adjust compression of your assets so that you can reduce the final size of your bundled game binary.

It is possible to make bundled builds using command line tools. Check the later part of this chapter for information on this.

When you make games your game data is packed. For most users, your game assets including images and scripts won’t be accessible, but for power users it’s always possible for them to access these files no matter what engine or tool you use to make games. Keep this in mind, and don’t put any sensitive files into your game project. Assume that eventually anyone motivated enough will be able to get into it.

