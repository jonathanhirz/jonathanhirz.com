---
layout: page
title: HaxeFlixel Tips
---

### FlxButton
FlxButton can be customized with your own images instead of using the default button. You need to design your button with three states: NORMAL, HIGHLIGHT, and PRESSED. These three states should be vertically stacked in your spritesheet, like [the default button](https://github.com/HaxeFlixel/flixel/blob/dev/assets/images/ui/button.png). Then in your code when you define your button, call **loadGraphic**, define the button as animated (true), and specify the width and height of one of the states. HaxeFlixel will take care of the rest.

{% highlight haxe %}
button = new FlxButton(FlxG.width/2, FlxG.height/2, "", callback);
button.loadGraphic("assets/images/button.png", true, width, height);
{% endhighlight %}


### Bundle ID
To automatically add your Bundle Identifier to your iOS/Xcode builds, add the **package** attribute to your app node in **Project.xml**. You can also specify a version number that will carry over to your Xcode project settings.

{% highlight xml %}
<app title="spaceSpuds" file="spaceSpuds" main="Main" version="0.1.1" company="jonathanHirz" package="com.jonathanHirz.spaceSpuds" />
{% endhighlight %}
