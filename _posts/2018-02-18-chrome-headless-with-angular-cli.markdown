---
layout: post
title:  "Chrome Headless with Angular CLI"
date:   2018-02-18 14:43:37 +0000
categories: jekyll update
---
By default angular cli runs tests with Google Chrome, however this is not always desirable. In particular if you are
running a continuous integration job on a headless server, normal Chrome will not work, fortunately switching to Chrome
Headless is simple. There are a few different options you may want to consider.

Option 1 is to use the command line and pass in a flag, this is probably what you would do when running a build in a CI tool such as
Jenkins or Travis. You can run the following command:

{% highlight command %}
ng test --browsers ChromeHeadless
{% endhighlight %}

Option 2 is to change the karma config. Open the file karma.config.js in the root directory and change the browsers section as follows:

{% highlight json %}
browsers: ['ChromeHeadless']
{% endhighlight %}
