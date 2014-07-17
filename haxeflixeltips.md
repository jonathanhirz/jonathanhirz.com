---
layout: page
title: HaxeFlixel Tips
---

To automatically add your Bundle Identifier to your iOS/Xcode builds, add the **package** attribute to your app node in **Project.xml**. You can also specify a version number that will carry over to your Xcode project settings.

{% highlight xml %}
<app title="spaceSpuds" file="spaceSpuds" main="Main" version="0.1.1" company="jonathanHirz" package="com.jonathanHirz.spaceSpuds" />
{% endhighlight %}
