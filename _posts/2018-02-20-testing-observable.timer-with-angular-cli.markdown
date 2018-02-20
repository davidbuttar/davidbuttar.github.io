---
layout: post
title:  "Testing Observable.timer with Angular CLI and fakeAsync"
date:   2018-02-20 16:59:37 +0000
categories: Testing, rxjs
---
I've had numerous issues testing angular rxjs streams with any kind of timer functionality such as Observable.timer or
debouceTime but wanted to share the following working example. I found the I needed to use the discardPeriodicTasks(); function.

Application Code:

{% highlight typescript %}
Observable.timer(0, 10000).mergeMap(() => {
      return this.someHttpCall(id);
    }).subscribe((data: any) => {
      this.answer = data.answer;
    });
{% endhighlight %}

Karma test, assuming you have otherwise a typical angular cli component test set up:

{% highlight json %}
it('should call the http and populate the data', fakeAsync(() => {
    fixture.detectChanges();
    tick(1000);
    discardPeriodicTasks();
    expect(component.answer).toBe(4);
  }));
{% endhighlight %}
