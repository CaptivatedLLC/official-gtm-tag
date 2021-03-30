# Official Captivated Widget Google Tag Manager Template

This tag wraps all the capabilities the [Captivated Widget](https://captivated.works) offers, without requiring a single line of code.

## Installation

### Install the template into your GTM workspace

1. Go to your Google Tag Manager workspace editor.
2. Select **Templates > Tag Templates > Search Gallery**, and search for *Captivated Messaging*. The **Captivated Messaging** template should appear.
3. Select the **Captivated Messaging** template and then click **Add to workspace**.

At this point, the Captivated Widget functionality is available to your workspace, but it is not in use until it is installed on a page through a tag.

### Add the widget to your website

1. Go to **Tags > New**.
2. Click inside *Tag Configuration* to begin setting up the tag type.
3. In the right menu, find **Captivated Messaging** and select it.
4. In the top bar, name the tag *Captivated Installation*.
5. The *Method / Event* field specifies what you want the widget to do for this tag. In this case, you want to install the widget onto the page.  Select **Install Captivated on the page**.
6. For the *Widget Script URL* field, you must specify the URL for your unique widget.  If the widget shortcode is:

```html
<script defer="true" src="https://api.captivated.works/widget.js?id=1157b856-7d3b-11e7-b4d5-e3842bdc5072"></script>
```

... then the URL is `https://api.captivated.works/widget.js?id=1157b856-7d3b-11e7-b4d5-e3842bdc5072`.

7. Next, you will need to set up the trigger that causes this tag to fire.  Typically, the widget is installed on all pages when the page is loaded.  To achieve this, click inside *Triggering* and select **All Pages**.
8. Click **Save**.

The next time the workspace is published, the widget should appear when the specified trigger is fired.

## Triggering Events (Optional)

Want to capture in your analytics when a website visitor opens the widget, registers for chat, sends a text message, etc.?  Captivated's GTM integration makes this simple.  Not only can you capture analytics, but you can trigger any custom event.

Captivated offers the following events to be available:

* When the Captivated widget window is opened
* When the Captivated widget window is closed
* When the visitor initiates a chat conversation
* When the visitor sends a chat message
* When the visitor sends a text message
* When the visitor ends the chat

To trigger a `dataLayer` event when one of these widget events occurs:

1. Install the widget as described above. Of course, the event will not fire if the widget is not installed on the page.
2. Go to **Tags > New**.
3. Click inside *Tag Configuration* to begin setting up the tag type.
4. In the right menu, find **Captivated Messaging** and select it.
5. In the top bar, name the tag appropriately, e.g. *Captivated Chat Message Sent*.
6. The *Method / Event* field specifies what you want the widget to do for this tag. Select the event you want to attach to.
7. For the *Event Name* field, specify the name of the `dataLayer` event you want to trigger.  If not specified, a sensibly named event will be triggered, e.g. `captivated-widget-sent-chat-message`.  It is recommended that you name your own event so that you can manage the process more easily.
8. Next, you will need to set up when this trigger gets added to the page.  In most cases, it makes sense to add these tags immediately to the page so that it is triggered any time the event is fired.  These tags can even be added to the page before the widget is actually installed.  To add the event immediately to a page, click inside *Triggering* and select **All Pages**.
9. Click **Save**.

From there, you can set up additional triggers for these new `dataLayer` events.
