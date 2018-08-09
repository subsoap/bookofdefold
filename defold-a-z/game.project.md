---
description: Description of all features related to the game.project master project file.
---

# game.project

**Note: this is old text still and needs to be updated for latest features.**

The game.project file is the main project file of your project. In it, you enter various important configuration files. You can modify the file directly with a text editor or use the built in Project Editor. If you modify this file directly with a text editor it will not be populated with default values, and you will need to add it all by hand. There are only a few values which can be modified for this file which are not exposed in the Project Editor. The Project Editor does show default values - if a value has not been changed from its default value then Defold will not bother to save that value in the game.project file - once you do change a value even if you change it back to its default it will then begin to be included in the game.project file and be visible in the text if edited directly. When editing files in the Project Editor you must change the input away from the last input you edited to be able to save the most recent changes.

If you edit your game.project file to include additional properties they will be accessible depending on where you place them. You can access these values via sys.get\_config\(\). For example, print\(sys.get\_config\(“project.title”\)\). You can create most any custom group, with most any custom contents. Do note that your game.project file is accessible as plain text so you should not put anything sensitive into it, only useful config information. It would be possible for users to modify your game.project to, for example, bootstrap into a collection you never intended to be the bootstrap. If you wish to you can fix this by having a global value check that is only set when your primary Collection is the actual bootstrap.

You may want to add your Publisher and AppName as custom values, and then use these values when saving your player save data instead of hard coding it deeper into your source. To add custom values, you must edit the game.project file in plain text mode \(Open As -&gt; Text\).

If you press the icon to the left of text boxes it will revert the values of the fields to default values. Oddly these default values are not the same as the values within the blank project.

project - General project settings. title: The title of your app. Displayed in the titlebar area for desktop builds. When doing iOS and Android builds this is the label used below your app’s icon - when making builds you can quickly modify this, or if you use a custom plist and manifest update the label there. CFBundleDisplayName for iOS/plist, for Android look for the first android:label and customize the value of that - both will by default be what you have set project.title to when you bundle your apps, but because these labels need to be shorter for mobile builds you may want to pick a shorter name vs desktop builds where it can be longer. If you don’t shorten this label for mobile builds it will simply be truncated, sometimes with a … where it has been cut off. version: As you release builds publicly, you can increase this version number. Inside of your game, you can grab this value so that you can display it to your users, or use it for comparison, such as checking client version with latest version available to download. Use: sys.get\_config\(“project.version”\)

write\_log: If true \(1\) then the Defold game engine will write logs as the app is ran. These logs can be useful for debugging purposes. A “log.txt” file is created in the root directory of the app. For iOS, you can access logs from iTunes -&gt; Apps -&gt; Files Sharing. For Android, look in the external storage. Use one of the many good Android apps, such as AirDroid, which allows you to remotely access the file system. On Android too, while running the development engine, you can find logs at the following location: /mnt/sdcard/Android/data/com.defold.dmengine/files/log.txt

compress\_archive: If true \(1\) then archives will be compressed when bundling. Android archives will always be compressed due to the way the platform works. You will generally want this on.

dependencies: This is a comma separated list of Defold hosted library dependency URLs. If you wish to use this feature then the library data must be hosted on the Defold servers as a project, and you must have permission to access it. If you create a library, you can find its proper URL to link to on the online Defold dashboard page for each project. An alternative to this feature is to use git submodules directly, but this takes more to setup.

custom\_resources: \(not exposed in Project Editor but should be\): Comma separated list of resources you wish to include in your project. You can list folders or specific files. Note that you should not include the leading slash when specifying folders. Including custom resources is necessary when you wish to arbitrarily run Lua files which you do not know the names of before compiling your project, such as RPG related scripted events.

display - Resolution and display settings. Currently Defold does not have any graphics throttling in place, and relies entirely on your system’s vsync. Sometimes when your graphics card drivers are updated or out of date things can go wrong. If your game runs too quickly on your desktop you may need to go into your graphics card settings and force vsync on.

width, height: The width and height of your project. You may use these values if you use custom rendering scripts.

high\_dpi: If true \(1\) then support for high-dpi screens will be enabled on Windows and Mac. If your computer has a high-dpi screen you will want to enable this option. samples: A whole number value greater than 0 will enabled super sampling for your project. Your project will be drawn at 2 \* x size, and then scaled down. This feature can greatly impact performance. It is meant to remove or smooth jagged edges. Don’t turn this feature on unless your target hardware can handle it as you currently cannot toggle it at runtime. In general, leave it off \(0\).

fullscreen: If true \(1\) enables fullscreen for desktop targets. Currently there is a bug with desktop fullscreen in that the native screen size is not used, and instead a default smaller size is used, leading to bad quality image. There also currently no ability to toggle fullscreen as runtime, or change resolution. Hopefully this improves in the future. update\_frequency: How often your game goes through its update loops. Valid values are 60, 30, 20, 15, 12, 10, 6, 5, 4, 3, 2, 1

variable\_dt: This, if set to true \(1\), allows the update frequency to be at a variable rate, and instead of maintaining a constant delta time passed to update loops as an argument, it allows updates as often as possible. Depending on your project you may want this checked or unchecked. Generally it is better to have a fixed rate if your game is using physics simulations \(if dt becomes inconsistent then your simulation results can vary where if the dt was consistent then the results would be the same every time\) but otherwise it's generally better to have variable delta timing on, and to not rely on a fixed delta time in your scripts.

display\_profiles: Defines the location of your .display\_profiles file for your project, which contains the various sizes of screen size layouts in whatever proportions you wish to support. If you edit the location directly you must include the c at the end for the eventual compiled version.

dynamic\_orientation: If set to true \(1\) then when you change your device’s orientation the project will automatically select the best fitting layout for that size and orientation. Note that the iOS development engine does not respect this setting value and always supports dynamic orientation; however, the release build does respect this value.

physics - Settings. type: Your project can either use 2D or 3D physics. Capsule Shapes are only functional with 3D physics enabled; however, with 3D physics enabled there are other considerations you must make for your project too. You can also compose capsule like shapes \(good for certain platforms\) out of 2 circles and a rectangle.

gravity\_y: y-axis gravity. Default value is -10, which moves physics objects, which are modified by gravity, to move downward. debug: If true \(1\) then physics objects will have their geometry drawn. Otherwise physics objects \(spheres, rectangles, capsules, and so on\) are invisible. Turn this on to better visualize and debug your game’s physics.

debug\_alpha: This value can be from 0-1. Making the value closer to 1 makes it more visible, closer to 0 more invisible.

world\_count: The maximum allowed number of physics worlds. If you have physics simulations happening inside of a collection loaded via a collection proxy then that is an independent world. You should carefully load and unload your collections so that you do not have more physics worlds active at once than you really need. Default max is 4, but this is more of a buffer for loading/unloading and you should try to use as few as possible at once.

gravity\_x: x-axis world gravity.

gravity\_z: z-axis world gravity.

scale: Value can be from 0.01 to 1. Defines scale of physics worlds relative to game world. Adjust this value to fix the scaling for your project.

debug\_scale: If you have debug enabled then, depending on your setup, you will be able to visibly see unit objects such as triads \(the x,y,z origin arrows\) and normals \(a ray which is perpendicular to another line\). This value defines the scale of these units.

max\_collisions: Max concurrent collisions that will be reported.

max\_contacts: Max concurrent contact points that will be reported.

contact\_impulse\_limit: If set to a value higher than 0 then any contact impulses which are lower than the value will be ignored.

bootstrap - initial settings passed to Defold’s game engine. main\_collection: The main starting point for your project. Note that when editing this value in the Project Editor it will automatically append a c at the end so as to point to the compiled version of the collection file. For example, /main/main.collectionc - you must point to the compiled version too if you edit directly. The same is true for other files which are linked to in the same way.

render: The render file to use - not the render script \(which is defined in the render file\). You can define multiple types of behaviors in your render script so only one is necessary.

graphics - Settings. default\_texture\_min\_filter: Default filter to use when min \(minification\) filtering. Set to either linear or nearest \(good for pixel art games\).

default\_texture\_mag\_filter: Default filter to use when mag \(magnification\) filtering. Set to either linear or nearest. These two min/mag are used when rendering images in the running game engine. If you are making a pixel art game then you will need to edit some other areas where there is filtering, such as with fonts, so that they use linear filtering as not all respect these default values.

max\_debug\_vertices: When drawing visual debug information, for physics and other objects, this setting determines the maximum allowed.

texture\_profiles: Define the location of your .texture\_profiles file. This does not point to a c / compiled version. Your .texture\_profiles file determines how different folders of image files are processed for different platforms when you bundle your game. Keep in mind that the default .texture\_profiles does not use the WebP format as support for it was only recently added. It’s a very good idea to use this format in your own projects as it will greatly reduce your bundled file size.

sound - Settings. gain: The default gain in linear scale generally from 1 to 0. Read the chapter on sounds for more information.

max\_sound\_data: The maximum number of unique sound files allowed.

max\_sound\_buffers: Maximum number of unique sounds loaded at once. Buffers hold sound data.

max\_sound\_sources: Maximum number of concurrently playing sounds.

max\_sound\_instances: The maximum number of sound components allowed active at once.

resources - Loading and resource management settings for HTML5 builds. http\_cache: If true \(1\) then resources will be cached locally \(saved\) and reloaded from cache instead of from the server when needed. Add a ?version=number or some kind of tag to force refresh with this option enabled.

uri: Defines where to find the game.project config file.

max\_resources: The maximum number of unique resources allowed to be loaded at a time. Fonts, for example, count as two resources. input - Settings.

repeat\_delay: How long in seconds before treating an input, which is pressed, as a repeating, held down input.

repeat\_interval: Once an input is treated as a repeated input, how often it counts as an event. Lower to have faster intervals. If you do not want a delay between events then don't use action.repeated which this is for.

gamepads: File references to a .gamepadsc file. The .gamepad files includes information on various .gamepad models and how you wish to support them. game\_binding: File reference to your .input\_binding file’s compiled version .input\_bindingc.

sprite - Settings. max\_count: Maximum number of sprite components allowed at once.

subpixels: While false \(0\), sprites are forced to be aligned to pixels. While true \(1\), sprites are no longer forced to align with pixels. This option is checked by default, and so the default behavior is to not snap align sprites to the pixel grid.

collection - Settings. max\_instances: Maximum number of instances of objects / components allowed at once.

collection\_proxy - Settings. max\_count: Maximum number of collection proxies allowed at once while the engine is running.

collectionfactory - Settings. max\_count: Maximum number of collection factories allowed at once.

factory - Game Object Factory Settings. max\_count: Maximum number of factories allowed at once.

ios - Settings. appicon\*: Various sizes of pre-made icons sizes which iOS will use when showing your app’s icon in different screens / devices. You can use or buy [https://iconverticons.com/online/](https://iconverticons.com/online/) to quickly generate all of the image sizes you need.

launchimage\*: These images are the hardware launch image shown at the start of your game. iOS first displays this image, and then once your app is loaded switches to your app. Apple suggests that you keep the launch image and the very first thing you display to your users the same. This design is meant to make apps look like they always launch instantly upon being opened. You must specify launch image files of each appropriate size for your game to display properly while testing on iOS!

pre\_rendered\_icons: If true \(1\) will disable the overlay which iOS adds to icons otherwise. If you do not disable this option then your final icon will have an extra gloss layer added on top by iOS.

bundle\_identifier: Generally this is in the format of com.company.product.version - it is a unique identifier of your app, and is in this way so that no other app in the world will have the same identifier. The first part of the identifier is generally based on your primary web-site domain, and it’s only possible for one company to own a unique domain so this in the best case should ensure uniqueness.

infoplist: If you wish to use a custom Info.plist file you can define one here. You can duplicate the standard infoplist included with Defold, and modify it to your needs. Remember that as Defold updates are released you may need to manually update your custom infoplist file so that all features work.

android - Settings. appicon\*: Pre-made icon images of various sizes which are used in different areas of the Android OS.

pushicon\*: Pre-made icon images of various sizes which are shown on the user receiving a push notification for the game app.

push\_field\_title: Specifies which field in the payload JSON to be used as the text title by default.

push\_field\_text: Specifies which field in the payload JSON to be used as the text body by default.

version\_code: Must be an integer. This is an internal number which must increase as you release builds and public them to the Android markets. A higher number determines that a build is more recent. This is not shown to users anywhere. Simply increase it by 1 each new version.

package: The unique package identifier generally in the form of com.company.app

gcm\_sender\_id: Google Cloud Messaging Sender ID. When you set up your app in the Google Play Developer Console you can get this ID from your app’s Services & APIs tab. This must be set to enable push notifications for Android on Google Play.

manifest: If you wish you can define a custom manifest file. The best practice is to bundle your Android application once, and then take the generated manifest from within it. Then customize it as you need. As new versions of Defold are released, you may need to redo this in order to get most recent changes which the Defold engine needs.

iap\_provider: This can be set to either “Amazon” or “GooglePlay” depending on which store you are building for. Defold supports the Amazon 2.0 store API. Defold will default to assuming “GooglePlay”.

input\_method: The default value is KeyEvent, which represents the older style of input for Android devices, and is default only to prevent breakage for older Defold projects. You should absolutely always change this value to HiddenInputField as it does a better job of handling popular software keyboards. The KeyEvent is the default only so as to not break older Defold projects.

osx - Mac OS X Settings. app\_icon: The .icns icon file used for the Mac OS X .app file generated. You can use the site [https://iconverticons.com/online/](https://iconverticons.com/online/) to generate a .icns file from a .png file. You can use up to a 1024x1024 image and it will generate all of the sizes.

infoplist: Like with iOS apps you can use custom Info.plist files. If you wish to use a custom infoplist first bundle your app for Mac OS X, and then right click on the app -&gt; Show Package Contents -&gt; Contents -&gt; Copy and paste the Info.plist file there into your Defold project’s folder, then define that within your game.project file. bundle\_identifier: Unique bundle identifier generally in the form of com.company.app for example: com.apple.itunes

windows - Settings app\_icon: The .ico file used when you make Windows build bundles. This file is used by the main .exe file as its icon. Again you can use the site [https://iconverticons.com/online/](https://iconverticons.com/online/) to generate your .ico from a .png file. The site will automatically generate the correct sizes based off your source image as long as you upload a large enough image. 1024x1024 or 512x512 would be fine.

html5 - Settings. set\_custom\_heap\_size: If true \(1\) a custom heap size will be set.

custom\_heap\_size: Custom heap size expressed in bytes. The default value is shown as 0 in the Project Editor, but this should not be used. The true default heap size is 256MB of memory - 268435456 Bytes. You most likely will not need to increase this value, and instead more likely will want to decrease this value when optimizing your game so that your project prepares a smaller heap size. include\_dev\_tool: If true \(1\) then when you bundle HTML5 builds memory tracking tools will be included.

htmlfile, cssfile: For convenience, you can define custom .html and .css files for HTML5 builds. You should make your custom versions based off the versions made when you bundle your HTML5 app as these files will not be processed at all only included in the ultimate bundle.

splash\_image: You can define a custom splash screen image, which is loaded by the browser, and shown while your application data is being loaded in the background. By default, a progress bar is shown too. All of this can be customized, and is covered in the later chapter Releasing on HTML5.

archive\_location\_prefix: Allows you to define an alternative location to host your archive file, such as hosting it on a CDN. For example, “[http://mygreatcdn.com/games/my\_game/“](http://mygreatcdn.com/games/my_game/“)

archive\_location\_suffix: As you update your HTML5 game, you may need to ensure that the updated version, and not the cached version is downloaded. You can add a suffix to the end of your archive location URI in order to force the user’s client to download the newer version. For example, “?build=5”

particle\_fx - ParticleFX Settings. max\_count: The maximum number of ParticleFX instances allowed.

max\_particle\_count: The maximum number of single particles allowed over all Particle FX instances.

iap - In App Purchase Settings. auto\_finish\_transactions: If true \(1\) then IAP transactions will be auto finished after they have been initiated and did not error. If you do not have this set to true then you must handling finalizing transactions yourself. For example: “iap.finish\(self, transaction\)” see later chapter on IAP for more information on handling IAP transactions properly.

network - Settings http\_timeout: How long to wait in seconds before timing out HTTP requests. You can also define custom http timeouts in seconds with every http.request call. See later chapter on HTTP Requests.

library - When this project is used as a library for another project. include\_dirs: Space separated list of directories which will be included by any projects which include this project as a library through Defold’s systems.

script - Settings. shared\_state: If true \(1\) state will be shared between all Lua scripts. By default, Defold keeps unique context between the different script types: Game Object scripts, GUI scripts, and the Render script. Rather than enable shared state, it’s generally better to access shared data instead through included Lua modules. Having shared\_state temporarily enabled can be useful with debugging.

tracking - Defold application tracking settings. app\_id: A unique App ID for your Defold project can be found on its dashboard page. If you do not define an App ID no analytics tracking will take place. If you do enter your App ID, and then open your app, it will send basic usage data to the Defold servers, which you can then view on your Defold dashboard for the project. Usage data is very useful when making decisions for your project’s future. The Defold team plans to improve the Defold Analytics to include features such as custom events. So you could, for example, view the number of times your users have completed a specific level, or how far they went through your tutorial before giving up - this kind of data can give you a highly valuable insight into what you need to improve to keep your users happy and playing.

