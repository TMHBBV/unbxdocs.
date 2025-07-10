---
title: Common Attributes
deprecated: false
hidden: false
metadata:
  robots: index
---
The following attributes are utilized as parameters across various endpoints and resources within the API.

​

# uid (userId)

A unique identifier (uid) is generated for each shopper, remaining consistent unless manually cleared. This uid is a random number tied to the shopper’s specific browser and device. If a shopper uses different browsers or devices, separate uids are created for each. For a consistent experience across all devices and browsers, you can use your logged-in shoppers’ customer id and sync the experience.

| Name | Type   |
| :--- | :----- |
| uid  | String |

## How to generate a userId?

To handle session management effectively across multiple platforms with a shared catalog and user base, businesses must maintain a mapping system that links each user to a unique identifier ‘uid’. This ensures consistent tracking and seamless user experiences across platforms.

1. Default Behavior: `var uid = 'uid-' + date.getTime() + '-' + Math.floor(Math.random() * 100000);`
2. For Logged-in Users: `var uid = md5(customerId)`

## What are the constraints?

1. Use the code provided to generate the uid, ensuring it meets the required type and length specifications.
2. It should be stored (e.g., in cookies or local storage) and included in the API payload.
3. Do NOT generate an ID that violates GDPR compliance or contains personally identifiable information (such as deviceID or unencrypted userID) that could be linked back to the shopper.
   # visitId
   A session or visit random identifier that expires after 30 minutes of inactivity.

| Name    | Type   |
| :------ | :----- |
| visitId | String |

## How to generate visitId?

1. For web browsers: This will be created by Netcore Unbxd Analytics script in the form of cookies.
2. For mobile apps: visitId = `'visitId-' + now + '-' + Math.floor(Math.random() * 100000);`

## What are the constraints?

1. The visitId should automatically reset after 30 minutes of user inactivity.
2. Once the visitId has been reset due to inactivity, the Visit event must be fired to log the start of a new session.\
   ​

# url

The url attribute refers to the web address of the page where the shopper initiates a search.

| Name | Type      |
| :--- | :-------- |
| url  | URLString |

For example, if a shopper is on a category page of an ecommerce site, such as: `https://www.example.com/electronics/laptops` and they use the search bar on that page, then the URL of the page where the search was triggered (before the search results page loads) would be: `https://www.example.com/electronics/laptops`.

This URL is captured to provide context on where the search originated.

​\
referrer
It refers to the URL of the previous webpage that directed the user to the current page. It helps track the flow of a user’s journey. If the user accesses the page directly (for instance, by typing the URL or using a bookmark), the referrer URL will be empty.

referrer: sessionStorage.getItem('urlPrevious') || document.referrer || '';

Name	Type\
referrer	URL string
For example:

If a user is browsing on a category page for “Gaming Laptops” at this URL: [https://www.example.com/gaming-laptops](https://www.example.com/gaming-laptops). And from there, they click on a product and navigate to the below link: [https://www.example.com/electronics/laptop-1](https://www.example.com/electronics/laptop-1)

In this case, the referrer would be: [https://www.example.com/gaming-laptops](https://www.example.com/gaming-laptops)

This information is useful for understanding how users navigate to specific pages and which external sources or internal pages are driving traffic.

​\
UnbxdKey
A unique site key is assigned to each of your environments (Dev, Stage and Prod) and sites configured with Unbxd. Also called SiteKey within the console.

Name	Type\
UnbxdKey	String
To access the UnbxdKey/sitekey,

Login to the Unbxd Console ↗\
Select the required site from the top-menu picker drop-down.
Navigate to Manage > Configure Site > Keys.
In the Keys page, you will find the Site Key. You can use the Copy button to get the Site key without any errors.
​
action
The action attribute specifies the type of user interaction or event being tracked. Common examples of actions include “click,” “visit,” “search,” or any other relevant user engagement on your website. This attribute helps categorize and identify the event being recorded.

For instance, if a user clicks on a product, the action will be recorded as “click,” whereas if a user visits a product page, it will be logged as a “visit.”

Event	Action Value to be Passed	Data Type\
Search Hit	search	String
Add to Cart	cart	String
Visitor	visitor	String
Product Click	click	String
Orders	order	String
​
timestamp
The timestamp (t) is a crucial parameter that denotes the exact moment an event is sent to the server. It combines the current time in milliseconds (since January 1, 1970, UTC) with a randomly generated number between 0 and 1 to ensure uniqueness. The formula used for this is: t = new Date().getTime() + '|' + Math.random();

Here’s a breakdown of how the formula works:

new Date().getTime(): This JavaScript function retrieves the current time in milliseconds from the epoch (January 1, 1970). It provides the exact time the event is triggered on the user’s device.\
'|' (Pipe Symbol): This is simply a separator used to combine the timestamp with the random number, making it easier to parse the values later.
Math.random(): This generates a random decimal number between 0 and 1. Adding this randomness to the timestamp ensures that even if two events are triggered at the exact same millisecond, their timestamp values will be unique due to the random decimal.
For Example:

Let’s say the current time is 1662365253141 milliseconds, and the random number generated is 0.6835012308821242. The value of t will be: t = 1662365253141 | 0.6835012308821242.

This timestamp helps maintain uniqueness, especially in scenarios where multiple events are fired in quick succession, ensuring each event can be accurately identified and processed.