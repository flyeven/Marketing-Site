---
layout: post
title: How Facebook content placeholder works
header: Facebook content placeholder deconstruction
category: Deconstructions
author: george
permalink: /deconstructions/2014/11/15/facebook-content-placeholder-deconstruction.html 
---

This is the first post of my new blog series called Deconstructions. Showcasing cool things people are doing in web development and breaking them down step by step. My first target is a cool content placeholder from the most recent Facebook overhaul. Before your friend's latest selfie or dog picture loads you may have noticed this nice bit of polish.

### What is it?
Straight to the point here it is. Below you can see my clone and my HTML (I changed a few things to make it easier to see):

<div class="timeline-wrapper">
    <div class="timeline-item">
        <div class="animated-background facebook">
            <div class="background-masker header-top"></div>
            <div class="background-masker header-left"></div>
            <div class="background-masker header-right"></div>
            <div class="background-masker header-bottom"></div>
            <div class="background-masker subheader-left"></div>
            <div class="background-masker subheader-right"></div>
            <div class="background-masker subheader-bottom"></div>
            <div class="background-masker content-top"></div>
            <div class="background-masker content-first-end"></div>
            <div class="background-masker content-second-line"></div>
            <div class="background-masker content-second-end"></div>
            <div class="background-masker content-third-line"></div>
            <div class="background-masker content-third-end"></div>
        </div>
    </div>
</div>

{% highlight html %}
<div class="timeline-wrapper">
    <div class="timeline-item">
        <div class="animated-background">
            <div class="background-masker header-top"></div>
            <div class="background-masker header-left"></div>
            <div class="background-masker header-right"></div>
            <div class="background-masker header-bottom"></div>
            <div class="background-masker subheader-left"></div>
            <div class="background-masker subheader-right"></div>
            <div class="background-masker subheader-bottom"></div>
            <div class="background-masker content-top"></div>
            <div class="background-masker content-first-end"></div>
            <div class="background-masker content-second-line"></div>
            <div class="background-masker content-second-end"></div>
            <div class="background-masker content-third-line"></div>
            <div class="background-masker content-third-end"></div>
        </div>
    </div>
</div>
{% endhighlight %}

As you can see the demo only contains three types on elements:

#### A Wrapper
This is the easiest bit, it's just a centered div to wrap the content. I chose to use the same colours as Facebook.

<div class="timeline-wrapper">
    <div class="timeline-item">
    </div>
</div>

{% highlight css %}
.timeline-item {
    background: #fff;
    border: 1px solid;
    border-color: #e5e6e9 #dfe0e4 #d0d1d5;
    border-radius: 3px;
    padding: 12px;

    margin: 0 auto;
    max-width: 472px;
    min-height: 200px;
}
{% endhighlight %}

#### A Fancy Animated Background
This is where the magic happens. It's a box that is has a animated background and that background happens to be a CSS gradient.

<div class="timeline-wrapper">
    <div class="timeline-item">
        <div class="animated-background">
        </div>
    </div>
</div>

{% highlight css %}
@keyframes placeHolderShimmer{
    0%{
        background-position: -468px 0
    }
    100%{
        background-position: 468px 0
    }
}

.animated-background {
    animation-duration: 1s;
    animation-fill-mode: forwards;
    animation-iteration-count: infinite;
    animation-name: placeHolderShimmer;
    animation-timing-function: linear;
    background: #f6f7f8;
    background: linear-gradient(to right,  #eeeeee 8%,#dddddd 18%,#eeeeee 33%);
    background-repeat: no-repeat;
    background-size: 800px 104px;
    height: 96px;
    position: relative;
}
{% endhighlight %}

#### Plenty of Tiny Masking Blocks
Without these the previous step just looks like a stupidly large progress bar. This gives the shape to the placeholder. It's just lots of little white divs that sit on top so you can't see the animation. This part gets messy fast. I have added some borders to this version to illustrate where the masks are placed (Try hovering on each block).

<div class="timeline-wrapper">
    <div class="timeline-item">
        <div class="animated-background outlined">
            <div class="background-masker header-top"></div>
            <div class="background-masker header-left"></div>
            <div class="background-masker header-right"></div>
            <div class="background-masker header-bottom"></div>
            <div class="background-masker subheader-left"></div>
            <div class="background-masker subheader-right"></div>
            <div class="background-masker subheader-bottom"></div>
            <div class="background-masker content-top"></div>
            <div class="background-masker content-first-end"></div>
            <div class="background-masker content-second-line"></div>
            <div class="background-masker content-second-end"></div>
            <div class="background-masker content-third-line"></div>
            <div class="background-masker content-third-end"></div>
        </div>
    </div>
</div>

{% highlight css %}
.background-masker {
    background: #fff;
    position: absolute;
}

/* Every thing below this is just positioning */

.background-masker.header-top,
.background-masker.header-bottom,
.background-masker.subheader-bottom {
    top: 0;
    left: 40px;
    right: 0;
    height: 10px;
}

.background-masker.header-left,
.background-masker.subheader-left,
.background-masker.header-right,
.background-masker.subheader-right {
    top: 10px;
    left: 40px;
    height: 8px;
    width: 10px;
}

.background-masker.header-bottom {
    top: 18px;
    height: 6px;
}

.background-masker.subheader-left,
.background-masker.subheader-right {
    top: 24px;
    height: 6px;
}


.background-masker.header-right,
.background-masker.subheader-right {
    width: auto;
    left: 300px;
    right: 0;
}

.background-masker.subheader-right {
    left: 230px;
}

.background-masker.subheader-bottom {
    top: 30px;
    height: 10px;
}

.background-masker.content-top,
.background-masker.content-second-line,
.background-masker.content-third-line,
.background-masker.content-second-end,
.background-masker.content-third-end,
.background-masker.content-first-end {
    top: 40px;
    left: 0;
    right: 0;
    height: 6px;
}

.background-masker.content-top {
    height:20px;
}

.background-masker.content-first-end,
.background-masker.content-second-end,
.background-masker.content-third-end{
    width: auto;
    left: 380px;
    right: 0;
    top: 60px;
    height: 8px;
}

.background-masker.content-second-line  {
    top: 68px;
}

.background-masker.content-second-end {
    left: 420px;
    top: 74px;
}

.background-masker.content-third-line {
    top: 82px;
}

.background-masker.content-third-end {
    left: 300px;
    top: 88px;
}
{% endhighlight %}

### Why would I ever use this?
We can't always remove having to wait for information but we can make the wait feel shorter. By giving some indication of what is going on and giving visual stimulus the user feels immediately more comfortable and less likely to leave. This is exactly like putting a progress bar on a long action. Apart from the fact it's some fancy polish, it's great usability. I think this feature is better than your average loading symbol because it actually feels like the content is almost there. After a quick search I found <a href="http://usabilitypost.com/2009/01/23/making-wait-times-feel-shorter/">this article</a> which explains it quite well.

### That's it
I have been looking for a situation I can use a loader like this but sadly one has not come up yet. I may use it for the upcoming GitHub integration while I am loading the list of repositories. If you found this useful or have any questions feel free to comment below. I am going to try to do one of these a week so if you see something you want deconstructed let me know.

Note: I used unprefixed CSS in the code examples to keep it clean. You can use <a href="http://prefixr.cloudvent.net/" target="_blank">Our CSS Prefixer</a> to get cross a cross browser version.

<style>
    @-webkit-keyframes placeHolderShimmer{
        0%{
            background-position:-468px 0
        }
        100%{
            background-position:468px 0
        }
    }

    @keyframes placeHolderShimmer{
        0%{
            background-position:-468px 0
        }
        100%{
            background-position:468px 0
        }
    }

    .timeline-wrapper {
        background-color: #e9eaed;
        color: #141823;
        padding: 20px;
        border: 1px solid #ccc;
        margin: 0 auto 1em;
    }

    .timeline-item {
        background: #fff;
        border: 1px solid;
        border-color: #e5e6e9 #dfe0e4 #d0d1d5;
        border-radius: 3px;
        padding: 12px;

        margin: 0 auto;
        max-width: 472px;
        min-height: 200px;
    }

    .animated-background {
        -webkit-animation-duration: 1s;
        animation-duration: 1s;
        -webkit-animation-fill-mode: forwards;
        animation-fill-mode: forwards;
        -webkit-animation-iteration-count: infinite;
        animation-iteration-count: infinite;
        -webkit-animation-name: placeHolderShimmer;
        animation-name: placeHolderShimmer;
        -webkit-animation-timing-function: linear;
        animation-timing-function: linear;
        background: #f6f7f8;
        background: #eeeeee;
        background: -webkit-gradient(linear, left top, right top, color-stop(8%, #eeeeee), color-stop(18%, #dddddd), color-stop(33%, #eeeeee));
        background: -webkit-linear-gradient(left, #eeeeee 8%, #dddddd 18%, #eeeeee 33%);
        background: linear-gradient(to right,  #eeeeee 8%,#dddddd 18%,#eeeeee 33%);
        -webkit-background-size: 800px 104px;
        background-size: 800px 104px;
        height: 96px;
        position: relative;
    }

    .background-masker {
        background: #fff;
        position: absolute;
        -webkit-box-sizing: border-box;
        -moz-box-sizing: border-box;
        box-sizing: border-box;
    }

    .outlined .background-masker {
        border: 1px solid #ddd;
    }


    .outlined:hover .background-masker {
        border: none;
    }

    .outlined:hover .background-masker:hover {
        border: 1px solid #ccc;
        z-index: 1;
    }

    .background-masker.header-top,
    .background-masker.header-bottom,
    .background-masker.subheader-bottom {
        top: 0;
        left: 40px;
        right: 0;
        height: 10px;
    }

    .background-masker.header-left,
    .background-masker.subheader-left,
    .background-masker.header-right,
    .background-masker.subheader-right {
        top: 10px;
        left: 40px;
        height: 8px;
        width: 10px;
    }

    .background-masker.header-bottom {
        top: 18px;
        height: 6px;
    }

    .background-masker.subheader-left,
    .background-masker.subheader-right {
        top: 24px;
        height: 6px;
    }


    .background-masker.header-right,
    .background-masker.subheader-right {
        width: auto;
        left: 300px;
        right: 0;
    }

    .background-masker.subheader-right {
        left: 230px;
    }

    .background-masker.subheader-bottom {
        top: 30px;
        height: 10px;
    }

    .background-masker.content-top,
    .background-masker.content-second-line,
    .background-masker.content-third-line,
    .background-masker.content-second-end,
    .background-masker.content-third-end,
    .background-masker.content-first-end {
        top: 40px;
        left: 0;
        right: 0;
        height: 6px;
    }

    .background-masker.content-top {
        height:20px;
    }

    .background-masker.content-first-end,
    .background-masker.content-second-end,
    .background-masker.content-third-end{
        width: auto;
        left: 380px;
        right: 0;
        top: 60px;
        height: 8px;
    }

    .background-masker.content-second-line  {
        top: 68px;
    }

    .background-masker.content-second-end {
        left: 420px;
        top: 74px;
    }

    .background-masker.content-third-line {
        top: 82px;
    }

    .background-masker.content-third-end {
        left: 300px;
        top: 88px;
    }
</style>
