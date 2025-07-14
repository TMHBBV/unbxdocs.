---
title: Unbxd Events Validator
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

While there are multiple events that are tracked by Unbxd Analytics, it is now easier to validate the analytics onto your sites via our Chrome Extension.  This extension can help to detect Analytics Integration Issues.

We have currently classified Analytics Issues into 2 broad categories:

* Is the analytics script included and required objects (liked “UnbxdAnalyticsConf”) are initialized with correct values?
* Are the relevant events fired correctly?
* Are all events required for a particular page type fired correctly (search or browse page along with recommendations widget)
* Are the events having all the required mandatory additional parameters (for example: “pid” must be sent for a click event)
* Are there any additional parameters that can be sent in each event to improve analytics ( these are shown as warning items)
* Any more validations that can be done on events correlation (for example: is the same “pid” sent in an **impression** > **Click** > **Cart** > **Order Flow**)
* Once the events are detected and a validation report is generated, you can download the report to validate it yourself or send it to us for further analysis for any required support in the integration.

<Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=0fpLvHW5uTk" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252F0fpLvHW5uTk%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253D0fpLvHW5uTk%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252F0fpLvHW5uTk%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22640%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=0fpLvHW5uTk" providerUrl="https://www.youtube.com/" providerName="YouTube" />

The extension intercepts the network calls on the page to look for 1p.jpg calls, validates the event as per the page type, and reports it on the extensions UI.

## How to install and use the extension?

1. Install the extension from the Chrome Store.
2. Go to any customer website and open the Developer Tools. You will see “ValidateUnbxdAnalytics” as a tab in the Developer Tools. Click on it.
3. Select your page (either Search or Category Page) and check the “Recommendation Widget” checkbox if you want to test the recommendations widget on that page as well.
4. Click on “Start Testing”.
5. Proceed to play around with customers’ websites and generate the Unbxd Analytics events. These will start showing up in the extensions UI

## Reports Download

* Once you’re done with all the actions to generate the events, click the “Stop” button. This will generate a report which states any missing mandatory or good to have events.
* You can also download the CSV report of the same by clicking the “Download CSV” button.