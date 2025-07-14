---
title: iOS SDK
deprecated: false
hidden: false
metadata:
  robots: index
---
The Unbxd SDK implements support for making network calls to the Unbxd platform and lets you easily configure and integrate Unbxd Site Search in your eCommerce application.

# Features

The following features are currently supported with Unbxd SDK.

| Features              | Description                                                                                                                                                                                                                                               |
| :-------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Analytics             | Allows you to track various visitor events on the eCommerce store such as product clicks, add to cart, orders, etc.                                                                                                                                       |
| Unbxd Commerce Search | Allows you to interact with the Unbxd platform and implement all search related functionality with ease.                                                                                                                                                  |
| Autosuggest           | For autocompletion of search queries and showcasing products relevant to query as you type.                                                                                                                                                               |
| Browse                | Allows you to interact with the Unbxd platform and implement all category related functionality with ease. You can customize the experience on various pages – Category, Brand, or any other attribute by leveraging various built-in features of Browse. |
| Recommendations       | Allows you to integrate the Unbxd recommendations widgets that showcase personalized product suggestions to visitors on every page of your eCommerce store.                                                                                               |

# Unbxd SDK for iOS

The Unbxd SDK implements support for making network calls to the Unbxd platform and lets you easily configure and integrate Unbxd Site Search in your eCommerce application.

## Features

The following features are currently supported with Unbxd SDK.

| Features              | Description                                                                                                                                                                                                                                               |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Analytics             | Allows you to track various visitor events on the eCommerce store such as product clicks, add to cart, orders, etc.                                                                                                                                       |
| Unbxd Commerce Search | Allows you to interact with the Unbxd platform and implement all search related functionality with ease.                                                                                                                                                  |
| Autosuggest           | For autocompletion of search queries and showcasing products relevant to query as you type.                                                                                                                                                               |
| Browse                | Allows you to interact with the Unbxd platform and implement all category related functionality with ease. You can customize the experience on various pages – Category, Brand, or any other attribute by leveraging various built-in features of Browse. |
| Recommendations       | Allows you to integrate the Unbxd recommendations widgets that showcase personalized product suggestions to visitors on every page of your eCommerce store.                                                                                               |

## Prerequisites

Before you get started with the integration, you need to:

* **Get your Site Key**: Set up your Unbxd account and obtain an API key, Site key. These keys are generated at the time of account creation and can be accessed within Console at **Manage > Configure Site > Keys**.
* **Upload your Product catalog**: A product catalog contains product-specific information for products in your inventory, like, title, price, category, color, description, availability, etc. Unbxd product discovery algorithms rely on the products and their fields within your feed data. You need to upload your catalog as a single JSON file.

For more information on product feed, see [here](https://unbxd.com/docs).

## Dependencies

* **Alamofire** 5.1.3 or above – Alamofire is a Swift-based HTTP networking library for iOS and Mac OS X.
* **CocoaLumberjack** 3.4.1 or above – Logging framework.

## Supported Platforms

Unbxd SDK is a dynamic framework programmed using Swift 4. This can be integrated with iOS applications with version 9.0 and above. The Framework is compatible with both Swift and Objective-C.

<Embed typeOfEmbed="youtube" url="https://www.youtube.com/watch?v=9tZ25lY9XqU" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fwww.youtube.com%252Fembed%252F9tZ25lY9XqU%253Ffeature%253Doembed%26display_name%3DYouTube%26url%3Dhttps%253A%252F%252Fwww.youtube.com%252Fwatch%253Fv%253D9tZ25lY9XqU%26image%3Dhttps%253A%252F%252Fi.ytimg.com%252Fvi%252F9tZ25lY9XqU%252Fhqdefault.jpg%26type%3Dtext%252Fhtml%26schema%3Dyoutube%22%20width%3D%22854%22%20height%3D%22480%22%20scrolling%3D%22no%22%20title%3D%22YouTube%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://www.youtube.com/watch?v=9tZ25lY9XqU" providerUrl="https://www.youtube.com/" providerName="YouTube" />

<br />

## Installation

Cocoapods is an application level dependency manager for Cocoa projects. It provides a standard format for managing external libraries. You can install it with the command below:

```bash
$ gem install cocoa pods
```

To integrate UnbxdSDK into your Xcode project using Cocoapods, specify it in your `Podfile`:

```ruby
source 'https://github.com/CocoaPods/Specs.git'  
source 'https://github.com/unbxd/iOS-SDK-Pod.git'  
platform :ios, '10.0'

target 'demo-unbxd' do  
  use_frameworks!
  pod 'Unbxd'
end 
```

Run the command below:

```bash
$ pod install
```

## Initialization

To begin, you will need to initialize the client. Import UnbxdSDK framework as below:

```swift
import Unbxd 
```

UnbxdSDK is initialized with an API key and Site key.

```swift
let client = Client(siteKey: "<SITE-KEY>", apiKey: "<API-KEY>", logsConfig: LogsConfig)
```

**LogsConfig** – Used to configure log level and provide folder path where log file to be saved. Example:

```swift
let logsFolderPath = "\(NSHomeDirectory())/Documents"  
LogsConfig(logLevel: .verbose, folderPath: logsFolderPath) 
```

All the SDK methods are invoked on a shared instance of `UbClient`.

**IMPORTANT**: We advise you to use your API Key in encrypted form on your frontend and never share it with anyone.