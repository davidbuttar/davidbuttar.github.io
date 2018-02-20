---
layout: post
title:  "Testing Observable.timer with Angular CLI and fakeAsync"
date:   2018-02-20 16:59:37 +0000
categories: Testing, rxjs
---
I've had numerous issues testing Angular RxJS streams with any kind of timer functionality such as Observable.timer or
debouceTime, with many solutions I tried either not working or being hugely convoluted. However I have 
found a fairly simple fix using **fakeAsyc** and the  **discardPeriodicTasks** function.

Application Code
----------------
 
Assuming you have something like a polling stream set up during component init:

{% highlight typescript %}
Observable.timer(0, 10000).mergeMap(() => {
    return this.someHttpCall(id);
}).subscribe((data: any) => {
    this.answer = data.answer;
});
{% endhighlight %}

Karma Test
----------
 
Assuming you have otherwise a typical angular cli component test set up:

{% highlight typescript %}
it('should call the http and populate the data', fakeAsync(() => {
    tick(1000);
    discardPeriodicTasks();
    fixture.detectChanges();
    expect(component.answer).toBe(4);
}));
{% endhighlight %}
