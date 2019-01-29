project_path: /web/tools/_project.yaml
book_path: /web/tools/_book.yaml
description: TODO

{# wf_updated_on: 2019-02-06 #}
{# wf_published_on: 2019-02-01 #}
{# wf_blink_components: Platform>DevTools #}

# Inspect Network Activity In Chrome DevTools {: .page-title }

{% include "web/_shared/contributors/kaycebasques.html" %}

This is a hands-on tour of some of the most commonly-used DevTools features related
to inspecting a page's network activity.

## When to use the Network panel {: #overview }

In general, use the Network panel when you need to make sure that resources are being
downloaded or uploaded as expected. The most common use cases for the Network panel are:

* Making sure that resources are actually being uploaded or downloaded at all.
* Inspecting the properties of an individual resource, such as its HTTP headers, content,
  size, and so on.

[speed]: /web/tools/chrome-devtools/speed/get-started

If you're looking for ways to improve page load performance, *don't* start with the Network
panel. There are many types of load performance issues that aren't related to network
activity. Start with the Audits panel because it gives you targeted suggestions on how to
improve your page. See [Optimize Website Speed][speed].

## Open the Network panel {: #open }

To get the most out of this tutorial, open up the demo and follow along with the instructions
yourself.

1. Open the [Get Started Demo](https://devtools.glitch.me/network/basics.html){: .external }.

     <figure>
       <img src="/web/tools/chrome-devtools/network-performance/imgs/tutorial/demo.png"
            alt="The demo"/>
       <figcaption>
         <b>Figure X</b>. The demo
       </figcaption>
     </figure>

     You might prefer to move the demo to a separate window.

     <figure>
       <img src="/web/tools/chrome-devtools/network-performance/imgs/tutorial/windows.png"
            alt="The demo in one window and this tutorial in a different window"/>
       <figcaption>
         <b>Figure X</b>. The demo in one window and this tutorial in a different window
       </figcaption>
     </figure>

1. [Open DevTools](/web/tools/chrome-devtools/open) by pressing
   <kbd>Control</kbd>+<kbd>Shift</kbd>+<kbd>J</kbd> or 
   <kbd>Command</kbd>+<kbd>Option</kbd>+<kbd>J</kbd> (Mac). The **Console**
   panel opens.

     <figure>
       <img src="/web/tools/chrome-devtools/network-performance/imgs/tutorial/console.png"
            alt="The Console"/>
       <figcaption>
         <b>Figure X</b>. The Console
       </figcaption>
     </figure>

     You might prefer to dock DevTools to the bottom of your window.

     <figure>
       <img src="/web/tools/chrome-devtools/network-performance/imgs/tutorial/docked.png"
            alt="DevTools docked to the bottom of the window"/>
       <figcaption>
         <b>Figure X</b>. DevTools docked to the bottom of the window
       </figcaption>
     </figure>

1. Click the **Network** tab. The Network panel opens.

     <figure>
       <img src="/web/tools/chrome-devtools/network-performance/imgs/tutorial/network.png"
            alt="DevTools docked to the bottom of the window"/>
       <figcaption>
         <b>Figure X</b>. DevTools docked to the bottom of the window
       </figcaption>
     </figure>

Right now the Network panel is empty. That's because DevTools only logs network activity
while it's open and no network activity has occurred since you opened DevTools.

## Log network activity {: #load }

To view the network activity that a page causes:

[reload]: /web/tools/chrome-devtools/images/shared/reload.png

1. Reload the page. The Network panel logs all network activity in the **Network Log**.

     <figure>
       <img src="/web/tools/chrome-devtools/network-performance/imgs/tutorial/log.png"
            alt="The Network Log"/>
       <figcaption>
         <b>Figure X</b>. The Network Log
       </figcaption>
     </figure>

     Each row of the **Network Log** represents a resource.

     Each column represents information about that resource. TODO Status, Type, Initiator

     By default the resources are listed chronologically. The network activity for the top
     resource initiated first, and the network activity for the bottom resource initiated last.

     When inspecting page load network activity, the top resource is usually the network request
     for the main HTML document.

1. So long as you've got DevTools open, it will record network activity in the Network Log.
   To demonstrate this, first look at the bottom of the **Network Log** and make a mental
   note of the last activity.
1. Now, click the **Get Data** button in the demo.
1. Look at the bottom of the **Network Log** again. There's a new resource called
   `getstarted.json`. Clicking the **Get Data** button caused the page to request this file.

## Show more information {: #information }

The columns of the Network Log are configurable. You can hide columns that you're not using.
There are also many columns that are hidden by default which you may find useful.

1. Right-click the header of the Network Log table and select **Domain**. The domain of
   each resource is now shown.

<aside class="objective">
  <b>Tip!</b> You can see the full URL of a resource by hovering over its name.
</aside>

## Simulate a slower network connection {: #throttle }

The network connection of the computer that you use to build sites is probably
faster than the network connections of the mobile devices of your users. By throttling
the page you can get a better idea of how long a page takes to load on a mobile device.

1. Click the **Throttling** dropdown, which is probably set to **Online**.
1. Select **Slow 3G**.
1. Long-press **Reload** ![Reload][reload]{: .inline-icon }
   and then select **Empty Cache And Hard Reload**.

[cache]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching

     On repeat visits, the browser usually serves some files from its [cache][cache]{: .external },
     which speeds up the page load. **Empty Cache And Hard Reload** forces the browser to go
     the network for all resources. This is helpful when you want to see how a first-time
     visitor experiences a page load.

<aside class="objective">
  <b>Tip!</b> See <a href="/web/tools/chrome-devtools/device-mode/">Simulate Mobile Devices
  With Device Mode</a> to discover other DevTools features related to simulating
  mobile devices, such as overriding geolocation and simulating device orientations.
</aside>

## Inspect a resource's details {: #details }

To view more information about a particular resource:

1. Click `getstarted.html`. The **Headers** tab is shown.

1. Click the **Preview** tab. A basic rendering of the HTML is shown.

     This tab is helpful when an API returns an error code in HTML and it's easier to read
     the rendered HTML than the HTML source code, or when inspecting images.

1. Click the **Response** tab. The HTML source code is shown.

1. Click the **Timing** tab. A breakdown of the network activity for this resource is shown.

## Search network headers and responses {: #search }

Use the **Search** pane when you need to search the HTTP headers and responses of all resources
for a certain string or regular expression.

[policies]: /web/tools/lighthouse/audits/cache-policy

For example, suppose you want to check if your resources are using reasonable [cache
policies][policies].

[search]: /web/tools/chrome-devtools/images/shared/search.png

1. Click **Search** ![Search][search]{: .inline-icon }. The Search pane opens to the left
   of the Network log.

1. Type `Cache-Control` and press <kbd>Enter</kbd>. The Search pane lists all instances of
   `Cache-Control` that it finds in resource headers or responses.

## Filter resources {: #filter }

DevTools provides numerous workflows for filtering out resources that aren't relevant to the
task at hand. Here are some of the most common ones.

TODO highlight filters pane image

The **Filters** pane should be enabled by default. But if you can't see it:

If you can't see the **Filters** pane:

[filter]: /web/tools/chrome-devtools/images/shared/filter.png

1. Click **Filter** ![Filter][filter]{: .inline-icon }.

### Filter by property {: #property }

The **Filter** text box lets you filter resources based on properties of each resource.
For example, to filter out all resources that aren't from the `raw.githubusercontent.com`
domain:

1. Type `domain:raw.githubusercontent.com` into the **Filter** text box.
1. Delete `domain:raw.githubusercontent.com` in order to see all resources again.

[props]: /web/tools/chrome-devtools/network-performance/reference#filter-by-property

See [Filter requests by properties][props] for the full list of properties.

### Filter by resource type {: #type }

To focus in on a certain type of file, such as stylesheets:

1. Click **CSS**. All other file types are filtered out.
1. To also see scripts, hold <kbd>Control</kbd> or <kbd>Command</kbd> (Mac) and then
   click **JS**.
1. Click **All** to remove the filters and see all resources again.

See [Filter requests](/web/tools/chrome-devtools/network-performance/reference#filter)
for other filtering workflows.

## Block requests {: #block }

Accidents happen. How does a page look and behave when some of its resources aren't
available? Does it fail completely, or is it still somewhat functional? Block requests
to find out:

1. Press <kbd>Control</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> or
   <kbd>Command</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> (Mac) to open the **Command Menu**.
1. Type `block`, select **Show Request Blocking**, and press <kbd>Enter</kbd>.

[add]: /web/tools/chrome-devtools/images/shared/add.png

1. Click **Add Pattern** ![Add Pattern][add]{: .inline-icon }.
1. Type `main.css`.
1. Click **Add**.
1. Reload the page. As expected, the page's styling is slightly messed up because its main
   stylesheet has been blocked.

     Note the `main.css` row in the Network Log. The red text means that the resource was blocked.

## Capture screenshots {: #screenshots }

Screenshots let you see how a page looked over time while it was loading.

[screenshots]: /web/tools/chrome-devtools/images/shared/screenshots.png

1. Click **Capture Screenshots** ![Capture Screenshots][screenshots]{: .inline-icon }.
1. Reload the page again via the **Empty Cache And Hard Reload** workflow. See
   [Simulate a slower connection](#throttle) if you need a reminder on how to do this.

## Next steps {: #next-steps }

Check out the [Network Reference](/web/tools/chrome-devtools/network-performance/reference)
to discover more DevTools features related to inspecting network activity.

## Test your knowledge {: #test }

Answer the questions below to reinforce the knowledge and skills that you learned throughout
this tutorial.

<div class="devsite-tracking-question">
  <div>
    When figuring out how to improve load performance, the Network panel is the best place
    to start.
  </div>
  <div class="gc-analytics-event"
       data-category="TODO" data-value="1"
       data-label="TODO">
    <div>True</div>
    <div>TODO</div>
  </div>
  <div class="gc-analytics-event"
       data-category="TODO" data-value="0"
       data-label="TODO">
    <div>False</div>
    <div>TODO</div>
  </div>
</div>

<div class="devsite-tracking-question">
  <div>
    Sometimes the Network panel is empty. Why is that?
  </div>
  <div class="gc-analytics-event"
       data-category="TODO" data-value="1"
       data-label="TODO">
    <div>Because DevTools only logs network activity when it's open.</div>
    <div>Correct.</div>
  </div>
  <div class="gc-analytics-event"
       data-category="TODO" data-value="0"
       data-label="TODO">
    <div>Because something is broken.</div>
    <div>Incorrect. Please try again.</div>
  </div>
</div>

## Feedback {: #feedback }

{% include "web/_shared/helpful.html" %}
