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

Accomplishing this requires a few steps in order for the event to cascade into Google Analytics or another app.  The data flows as follows:

1. The user performs an action, such as opening the widget window.
2. The Captivated widget triggers its event.
3. A GTM tag listens for this event and pushes information to the `dataLayer` upon execution.
4. A GTM trigger looks for matching information to be pushed to the `dataLayer` and then executes the trigger.
5. Other GTM tags listen for that trigger and perform an action, such as logging the event in Google Analytics.

Therefore, the steps are to create the GTM tag to convert the widget event into a `dataLayer` event, then create the trigger to convert the `dataLayer` event into an actionable GTM event, and finally to create another tag to perform the event when the trigger occurs.

### Create tags to push information to the dataLayer

To push these events to the `dataLayer` when one of these widget events occurs:

1. Install the widget as described above. Of course, the event will not fire if the widget is not installed on the page.
2. Go to **Tags > New**.
3. Click inside *Tag Configuration* to begin setting up the tag type.
4. In the right menu, find **Captivated Messaging** and select it.
5. In the top bar, name the tag appropriately, e.g. *Captivated Chat Message Sent*.
6. The *Method / Event* field specifies what you want the widget to do for this tag. Select the event you want to attach to.
7. For the *Event Name* field, specify the name of the `dataLayer` event you want to trigger.  If not specified, a sensibly named event will be triggered, e.g. `captivated-widget-sent-chat-message`.  It is recommended that you name your own event so that you can manage the process more easily.
8. Next, you will need to set up when this trigger gets added to the page.  In most cases, it makes sense to add these tags immediately to the page so that it is triggered any time the event is fired.  These tags can even be added to the page before the widget is actually installed.  To add the event immediately to a page, click inside *Triggering* and select **All Pages**.
9. Click **Save**.

### Create triggers to convert the dataLayer event into an actionable event

Triggers watch for data being pushed to the `dataLayer`, and when one matches the specified criteria, will execute the trigger, which will then execute all tags that are listening for that trigger.

1. Go to **Triggers > New**.
2. Click inside *Trigger Configuration* to begin setting up the trigger.
3. In the right menu, find **Custom Event** and select it.
4. For *Event Name*, specify the event name specified when creating the `dataLayer` event, such as `captivated-widget-sent-chat-message`.
5. For *This trigger fires on*, select **Some Custom Events**.
6. For *Fire this trigger when an Event occurs and all of these conditions are true*, specify **Event equals** the event name, such as `captivated-wdiget-sent-chat-message`.
7. At the very top of the screen, name the trigger the same name as the event, for the sake of consistency.
8. Click **Save**.

Repeat this series of steps for each widget event you want to track.

### Create a tag to send to analytics when the trigger occurs

The final step is to connect the trigger to the final action you want to take, such as logging the event in Google Analytics.  We will use Google Analytics as the example here.

1. Go to **Tags > New**.
2. Click inside *Tag Configuration*.
3. In the right menu, find **Google Analytics: Universal Analytics** and select it.
4. For *Track Type*, select **Event** because you want it to trigger when your custom event occurs.
5. For *Category*, specify **Captivated Widget**.  This way, all of these events will be categorized together in Google Analytics.
6. For *Action*, specify **{{Event}}**.  This means "use the name of the event that was triggered".  This way, the event names you specified in the previous steps will automatically flow through as the action name in Google Analytics.
7. If you want to track the URL where this event occurred, for *Label*, specify **{{Page URL}}**.  You can track a different property as well, or none at all.
8. If you need to specify the GA Tracking ID, click the checkbox *Enable override settings in this tag* and enter the Tracking ID below.
9. In the *Triggering* section at the bottom, click inside it to select the first trigger.  On the right, select one of the triggers you set up in the previous section.  Then click the plus sign to add the next trigger, and repeat until all of the Captivated triggers have been added.
10. At the very top, name the tigger **Captivated to Google Analytics**.
11. Click **Save**.

By doing this, you created one tag that listens to all of the Captivated triggers and sends the specific event name for the trigger upon execution.
