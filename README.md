# Termux

termux-app
Repository navigation
Code
Issues
463
 (463)
Pull requests
78
 (78)
Termux - a terminal emulator application for Android OS extendible by variety of packages.

f-droid.org/en/packages/com.termux
License
 View license
Security policy
 Security policy
 55k stars
 6.6k forks
 1.5k watching
 19 Branches
 95 Tags
 Activity
 Custom properties
Public repository
termux/termux-app
Name	
agnostic-apollo
agnostic-apollo
last month
.github
4 months ago
app
3 months ago
art
5 years ago
docs/en
4 years ago
fastlane/metadata/android/en-US
5 years ago
gradle/wrapper
4 months ago
site/assets/sponsors
8 months ago
terminal-emulator
last month
terminal-view
4 months ago
termux-shared
4 months ago
Repository files navigation
README
License
Security
Termux application
Build status Testing status Join the chat at https://gitter.im/termux/termux Join the Termux discord server Termux library releases at Jitpack

Termux is an Android terminal application and Linux environment.

Note that this repository is for the app itself (the user interface and the terminal emulation). For the packages installable inside the app, see termux/termux-packages.

Quick how-to about Termux package management is available at Package Management. It also has info on how to fix repository is under maintenance or down errors when running apt or pkg commands.

We are looking for Termux Android application maintainers.

NOTICE: Termux may be unstable on Android 12+. Android OS will kill any (phantom) processes greater than 32 (limit is for all apps combined) and also kill any processes using excessive CPU. You may get [Process completed (signal 9) - press Enter] message in the terminal without actually exiting the shell process yourself. Check the related issue #2366, issue tracker, phantom cached and empty processes docs and this TLDR comment on how to disable trimming of phantom and excessive cpu usage processes. A proper docs page will be added later. An option to disable the killing should be available in Android 12L or 13, so upgrade at your own risk if you are on Android 11, specially if you are not rooted.

Contents
Termux App and Plugins
Installation
Uninstallation
Important Links
Debugging
For Maintainers and Contributors
Forking
Sponsors and Funders
Termux App and Plugins
The core Termux app comes with the following optional plugin apps.

Termux:API
Termux:Boot
Termux:Float
Termux:Styling
Termux:Tasker
Termux:Widget
Installation
Latest version is v0.118.3.

NOTICE: It is highly recommended that you update to v0.118.0 or higher ASAP for various bug fixes, including a critical world-readable vulnerability reported here. See below for information regarding Termux on Google Play.

Termux can be obtained through various sources listed below for only Android >= 7 with full support for apps and packages.

Support for both app and packages was dropped for Android 5 and 6 on 2020-01-01 at v0.83, however it was re-added just for the app without any support for package updates on 2022-05-24 via the GitHub sources. Check here for the details.

The APK files of different sources are signed with different signature keys. The Termux app and all its plugins use the same sharedUserId com.termux and so all their APKs installed on a device must have been signed with the same signature key to work together and so they must all be installed from the same source. Do not attempt to mix them together, i.e do not try to install an app or plugin from F-Droid and another one from a different source like GitHub. Android Package Manager will also normally not allow installation of APKs with different signatures and you will get errors on installation like App not installed, Failed to install due to an unknown error, INSTALL_FAILED_UPDATE_INCOMPATIBLE, INSTALL_FAILED_SHARED_USER_INCOMPATIBLE, signatures do not match previously installed version, etc. This restriction can be bypassed with root or with custom roms.

If you wish to install from a different source, then you must uninstall any and all existing Termux or its plugin app APKs from your device first, then install all new APKs from the same new source. Check Uninstallation section for details. You may also want to consider Backing up Termux before the uninstallation so that you can restore it after re-installing from Termux different source.

In the following paragraphs, "bootstrap" refers to the minimal packages that are shipped with the termux-app itself to start a working shell environment. Its zips are built and released here.

F-Droid
Termux application can be obtained from F-Droid from here.

You do not need to download the F-Droid app (via the Download F-Droid link) to install Termux. You can download the Termux APK directly from the site by clicking the Download APK link at the bottom of each version section.

It usually takes a few days (or even a week or more) for updates to be available on F-Droid once an update has been released on GitHub. The F-Droid releases are built and published by F-Droid once they detect a new GitHub release. The Termux maintainers do not have any control over the building and publishing of the Termux apps on F-Droid. Moreover, the Termux maintainers also do not have access to the APK signing keys of F-Droid releases, so we cannot release an APK ourselves on GitHub that would be compatible with F-Droid releases.

The F-Droid app often may not notify you of updates and you will manually have to do a pull down swipe action in the Updates tab of the app for it to check updates. Make sure battery optimizations are disabled for the app, check https://dontkillmyapp.com/ for details on how to do that.

Only a universal APK is released, which will work on all supported architectures. The APK and bootstrap installation size will be ~180MB. F-Droid does not support architecture specific APKs.

GitHub
Termux application can be obtained on GitHub either from GitHub Releases for version >= 0.118.0 or from GitHub Build Action workflows. For android >= 7, only install apt-android-7 variants. For android 5 and 6, only install apt-android-5 variants.

The APKs for GitHub Releases will be listed under Assets drop-down of a release. These are automatically attached when a new version is released.

The APKs for GitHub Build action workflows will be listed under Artifacts section of a workflow run. These are created for each commit/push done to the repository and can be used by users who don't want to wait for releases and want to try out the latest features immediately or want to test their pull requests. Note that for action workflows, you need to be logged into a GitHub account for the Artifacts links to be enabled/clickable. If you are using the GitHub app, then make sure to open workflow link in a browser like Chrome or Firefox that has your GitHub account logged in since the in-app browser may not be logged in.

The APKs for both of these are debuggable and are compatible with each other but they are not compatible with other sources.

Both universal and architecture specific APKs are released. The APK and bootstrap installation size will be ~180MB if using universal and ~120MB if using architecture specific. Check here for details.

Security warning: APK files on GitHub are signed with a test key that has been shared with community. This IS NOT an official developer key and everyone can use it to generate releases for own testing. Be very careful when using Termux GitHub builds obtained elsewhere except https://github.com/termux/termux-app. Everyone is able to use it to forge a malicious Termux update installable over the GitHub build. Think twice about installing Termux builds distributed via Telegram or other social media. If your device get caught by malware, we will not be able to help you.

The test key shall not be used to impersonate @termux and can't be used for this anyway. This key is not trusted by us and it is quite easy to detect its use in user generated content.

Keystore information
Google Play Store (Experimental branch)
There is currently a build of Termux available on Google Play for Android 11+ devices, with extensive adjustments in order to pass policy requirements there. This is under development and has missing functionality and bugs (see here for status updates) compared to the stable F-Droid build, which is why most users who can should still use F-Droid or GitHub build as mentioned above.

Currently, Google Play will try to update installations away from F-Droid ones. Updating will still fail as sharedUserId has been removed. A planned 0.118.1 F-Droid release will fix this by setting a higher version code than used for the PlayStore app. Meanwhile, to prevent Google Play from attempting to download and then fail to install the Google Play releases over existing installations, you can open the Termux apps pages on Google Play and then click on the 3 dots options button in the top right and then disable the Enable auto update toggle. However, the Termux apps updates will still show in the PlayStore app updates list.

If you want to help out with testing the Google Play build (or cannot install Termux from other sources), be aware that it's built from a separate repository (https://github.com/termux-play-store/) - be sure to report issues there, as any issues encountered might very well be specific to that repository.

Uninstallation
Uninstallation may be required if a user doesn't want Termux installed in their device anymore or is switching to a different install source. You may also want to consider Backing up Termux before the uninstallation.

To uninstall Termux completely, you must uninstall any and all existing Termux or its plugin app APKs listed in Termux App and Plugins.

Go to Android Settings -> Applications and then look for those apps. You can also use the search feature if it’s available on your device and search termux in the applications list.

Even if you think you have not installed any of the plugins, it's strongly suggested to go through the application list in Android settings and double-check.

Important Links
Community
All community links are available here.

The main ones are the following.

Termux Reddit community
Termux User Matrix Channel (Gitter)
Termux Dev Matrix Channel (Gitter)
Termux X (Twitter)
Termux Support Email
Wikis
Termux Wiki
Termux App Wiki
Termux Packages Wiki
Miscellaneous
FAQ
Termux File System Layout
Differences From Linux
Package Management
Remote Access
Backing up Termux
Terminal Settings
Touch Keyboard
Android Storage and Sharing Data with Other Apps
Android APIs
Moved Termux Packages Hosting From Bintray to IPFS
Running Commands in Termux From Other Apps via RUN_COMMAND intent
Termux and Android 10
Terminal
Debugging
You can help debug problems of the Termux app and its plugins by setting appropriate logcat Log Level in Termux app settings -> <APP_NAME> -> Debugging -> Log Level (Requires Termux app version >= 0.118.0). The Log Level defaults to Normal and log level Verbose currently logs additional information. Its best to revert log level to Normal after you have finished debugging since private data may otherwise be passed to logcat during normal operation and moreover, additional logging increases execution time.

The plugin apps do not execute the commands themselves but send execution intents to Termux app, which has its own log level which can be set in Termux app settings -> Termux -> Debugging -> Log Level. So you must set log level for both Termux and the respective plugin app settings to get all the info.

Once log levels have been set, you can run the logcat command in Termux app terminal to view the logs in realtime (Ctrl+c to stop) or use logcat -d > logcat.txt to take a dump of the log. You can also view the logs from a PC over ADB. For more information, check official android logcat guide here.

Moreover, users can generate termux files stat info and logcat dump automatically too with terminal's long hold options menu More -> Report Issue option and selecting YES in the prompt shown to add debug info. This can be helpful for reporting and debugging other issues. If the report generated is too large, then Save To File option in context menu (3 dots on top right) of ReportActivity can be used and the file viewed/shared instead.

Users must post complete report (optionally without sensitive info) when reporting issues. Issues opened with (partial) screenshots of error reports instead of text will likely be automatically closed/deleted.

Log Levels
Off - Log nothing.
Normal - Start logging error, warn and info messages and stacktraces.
Debug - Start logging debug messages.
Verbose - Start logging verbose messages.
For Maintainers and Contributors
The termux-shared library was added in v0.109. It defines shared constants and utils of the Termux app and its plugins. It was created to allow for the removal of all hardcoded paths in the Termux app. Some of the termux plugins are using this as well and rest will in future. If you are contributing code that is using a constant or a util that may be shared, then define it in termux-shared library if it currently doesn't exist and reference it from there. Update the relevant changelogs as well. Pull requests using hardcoded values will/should not be accepted. Termux app and plugin specific classes must be added under com.termux.shared.termux package and general classes outside it. The termux-shared LICENSE must also be checked and updated if necessary when contributing code. The licenses of any external library or code must be honoured.

The main Termux constants are defined by TermuxConstants class. It also contains information on how to fork Termux or build it with your own package name. Changing the package name will require building the bootstrap zip packages and other packages with the new $PREFIX, check Building Packages for more info.

Check Termux Libraries for how to import termux libraries in plugin apps and Forking and Local Development for how to update termux libraries for plugins.

The versionName in build.gradle files of Termux and its plugin apps must follow the semantic version 2.0.0 spec in the format major.minor.patch(-prerelease)(+buildmetadata). When bumping versionName in build.gradle files and when creating a tag for new releases on GitHub, make sure to include the patch number as well, like v0.1.0 instead of just v0.1. The build.gradle files and attach_debug_apks_to_release workflow validates the version as well and the build/attachment will fail if versionName does not follow the spec.

Commit Messages Guidelines
Commit messages must use the Conventional Commits spec so that chagelogs as per the Keep a Changelog spec can automatically be generated by the create-conventional-changelog script, check its repo for further details on the spec. The first letter for type and description must be capital and description should be in the present tense. The space after the colon : is necessary. For a breaking change, add an exclamation mark ! before the colon :, so that it is highlighted in the chagelog automatically.

<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
Only the types listed below must be used exactly as they are used in the changelog headings. For example, Added: Add foo, Added|Fixed: Add foo and fix bar, Changed!: Change baz as a breaking change, etc. You can optionally add a scope as well, like Fixed(terminal): Fix some bug. Do not use anything else as type, like add instead of Added, etc.

Added for new features.
Changed for changes in existing functionality.
Deprecated for soon-to-be removed features.
Removed for now removed features.
Fixed for any bug fixes.
Security in case of vulnerabilities.
Forking
Check TermuxConstants javadocs for instructions on what changes to make in the app to change package name.
You also need to recompile bootstrap zip for the new package name. Check building bootstrap, here and here.
Currently, not all plugins use TermuxConstants from termux-shared library and have hardcoded com.termux values and will need to be manually patched.
If forking termux plugins, check Forking and Local Development for info on how to use termux libraries for plugins.
