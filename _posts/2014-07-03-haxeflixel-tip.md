---
layout: post
title: HaxeFlixel / Xcode tip for faster builds
---

Today I have been rebuilding a HaxeFlixel project in Xcode multiple times. I realized that each time I would rebuild, the **Debug Information Format** setting would revert back to the default, which is **DWARF with dSYM File**. This setting, which I admittedly don't fully understand, really slows down building the project, sending it to my iPhone, and slows down the game too. I think the extra debug information is unnecessary, and it *really* slows down my workflow. So, how do we change this default setting to **DWARF**? Glad you asked, because I spent an hour or two figuring this out today, and I would love to share.

First off, this guide is obviously for Mac only, as you need a Mac to run Xcode. Not sure how this applies to the Windows world.

Now, find you Haxe directory on your hard drive. Mine is located at:

{% highlight bash %}
/usr/lib/haxe/lib/lime/1,0,0/templates/iphone
{% endhighlight %}

The version number might be different, but this folder will hold the default Xcode project that Haxe will use to make your game's project. Trying to open this project directly throws an error for me, so what you have to do is right click on the **PROJ.xcodeproj** and Show Package Contents. Open up **project.pbxproj** and look for the build configuration settings section. It looks like this:

{% highlight bash %}
/* Begin XCBuildConfiguration section */
		C01FCF4F08A954540054247B /* Debug */ = {/* Build configuration list for PBXProject "::APP_TITLE::" */
			isa = XCBuildConfiguration;
			buildSettings = {
				ALWAYS_SEARCH_USER_PATHS = NO;
				ARCHS = ::CURRENT_ARCHS::;
				::if (OBJC_ARC)::
				CLANG_CXX_LANGUAGE_STANDARD = "gnu++0x";
				CLANG_ENABLE_OBJC_ARC = YES;
				CLANG_WARN__DUPLICATE_METHOD_MATCH = YES;
				::end::
				"CODE_SIGN_IDENTITY[sdk=iphoneos*]" = "::KEY_STORE_IDENTITY::";
				COPY_PHASE_STRIP = NO;
				GCC_C_LANGUAGE_STANDARD = gnu99;
				GCC_DYNAMIC_NO_PIC = NO;
				GCC_OPTIMIZATION_LEVEL = 0;
				GCC_PREPROCESSOR_DEFINITIONS = (
					"DEBUG=1",
					"$(inherited)",
				);
				GCC_SYMBOLS_PRIVATE_EXTERN = NO;
				GCC_WARN_ABOUT_RETURN_TYPE = YES;
				GCC_WARN_UNINITIALIZED_AUTOS = YES;
				GCC_WARN_UNUSED_VARIABLE = YES;
				IPHONEOS_DEPLOYMENT_TARGET = ::DEPLOYMENT::;
				SDKROOT = iphoneos;
				TARGETED_DEVICE_FAMILY = "::TARGET_DEVICES::";
            	::THUMB_SUPPORT::
				VALID_ARCHS = "::VALID_ARCHS::";
			};
			name = Debug;
		};
		C01FCF5008A954540054247B /* Release */ = {/* Build configuration list for PBXProject "::APP_TITLE::" */
			isa = XCBuildConfiguration;
			buildSettings = {
				ALWAYS_SEARCH_USER_PATHS = NO;
				ARCHS = ::CURRENT_ARCHS::;
				::if (OBJC_ARC)::
				CLANG_CXX_LANGUAGE_STANDARD = "gnu++0x";
				CLANG_ENABLE_OBJC_ARC = YES;
				CLANG_WARN__DUPLICATE_METHOD_MATCH = YES;
				::end::
				"CODE_SIGN_IDENTITY[sdk=iphoneos*]" = "::KEY_STORE_IDENTITY::";
				/* COMPRESS_PNG_FILES = NO; */
				COPY_PHASE_STRIP = YES;
				GCC_C_LANGUAGE_STANDARD = gnu99;
				/* GCC_ENABLE_SYMBOL_SEPARATION = YES; */
				GCC_WARN_ABOUT_RETURN_TYPE = YES;
				GCC_WARN_UNINITIALIZED_AUTOS = YES;
				GCC_WARN_UNUSED_VARIABLE = YES;
				IPHONEOS_DEPLOYMENT_TARGET = ::DEPLOYMENT::;
				OTHER_CFLAGS = "-DNS_BLOCK_ASSERTIONS=1";
				/* PRECOMPS_INCLUDE_HEADERS_FROM_BUILT_PRODUCTS_DIR = YES; */
				SDKROOT = iphoneos;
				TARGETED_DEVICE_FAMILY = "::TARGET_DEVICES::";
            	::THUMB_SUPPORT::
				VALID_ARCHS = "::VALID_ARCHS::";
				VALIDATE_PRODUCT = YES;
			};
			name = Release;
{% endhighlight %}

What you want to do is add the config line:
{% highlight bash %}
DEBUG_INFORMATION_FORMAT = dwarf;
{% endhighlight %}

into both  the Debug and Release sections. I added them after the
{% highlight bash %}
COPY_PHASE_STRIP = YES;
{% endhighlight %}

line so things would be alphabetical, but I don't think it matters where you add it.

Now, when you build a new iOS/Xcode project with HaxeFlixel, or update your Xcode project, you should have this debug setting as the default, and your builds will be much faster.

**Two things I forgot to mention:** you need to change the permissions on the project.pbxproj file so you can write the changes. Right click, Get Info, scroll down to permission, click the lock icon, enter admin password, change 'everyone' from 'read-only' to 'read & write'. Two, every time the lime package updates, you need to make this change again. I am going to submit a pull request to have this changed permanently, but I don't know if this is a priority for the team.