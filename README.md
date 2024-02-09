# Simpli.fi HTML5 Developer Docs and Samples

## About

This document describes how to create Simpli.fi compatible HTML5 ads.

## Background

A Simpli.fi compatible HTML5 ad has two parts. The first part is your creative, the HTML5 ad itself. The second part are the Simpli.fi Macros - a set of fields that are replaced in the ad creative when it is displayed to users. In order for the ad to function properly you must insert the Simpli.fi Macros into the HTML5 content of your ad.

## What is an HTML5 ad?

HTML5 ads are essentially just web pages, but they conform to a specific set of rules and are sized to fit in a standard ad location. The IAB publishes industry standards and recommendations that define the specifics of HTML5. At the time of this writing, these general recommendations are outlined in their [Fixed Size Ad Specifications](https://www.iab.com/wp-content/uploads/2019/04/IABNewAdPortfolio_LW_FixedSizeSpec.pdf). We proactively work with the IAB and contribute feedback on these specifications.

## What are the Simpli.fi Macros?

Simpli.fi Macros are placeholders that are used to set replacement values for the ad when the ads are served. You can think of them just like fields in a mail merge document. The list of macros is defined by Simpli.fi and are used in ads to set the target url for clicks, perform cache busting, and create dynamic HTML5 ads.

Please reach out to the Simpli.fi helpdesk or your client success rep in order to obtain an up-to-date list of supported macros.

## Creating a Basic Ad

### Getting Started

We’ll begin by creating a very simple custom HTML5 ad and providing the macro for the click tracking to work. Here are the basic steps:

Create a new folder on your computer that will contain the ad.
Add an image. In our example the ad will be a 300x250 ad, so the dimensions of our image will be 300x250 pixels.

Add an HTML page that references the image. Below is the HTML we will use for the ad.

### Basic Ad HTML

```
<!DOCTYPE html>
<html>
  <head>
    <meta name=”ad.size” content=”width=300,height=250”>
  </head>
  <body>
    <img src=”300x250.jpg” onclick=”window.open('{{clickMacro}}')"/>
  </body>
</html>
```

### Uploading the Ad

Next we’re going to create a zip file that contains the ad HTML and image file, and upload it to the Simpli.fi UI.

Save the contents of the basic ad HTML above into a new file named `index.html`. Next, create a zip file that contains the `index.html` and `300x250.jpg`.

> NOTE: Only the actual files should be added to the zip. If you include the folder from the step above into the zip, it is rejected by ad validation in the UI.

Once you have created the zip file, drag and drop (or click browse) the zip file into your ad campaign in the UI. The ad, if valid, is automatically extracted and its contents saved.

The uploaded ad is automatically click-verified to ensure it clicks through to the target URL, if specified in the UI. If click verification fails, hover over the click-verify button/icon to view error messages. Click the click-verify button to reattempt the process, as needed.

## HTML5 Ad Validations

In order for your HTML5 ad to pass validation, it must meet the following requirements:

* Zip file must be 250 kb or smaller.
* Zip file may contain up to 50 files.
* There must be a single file named `index.html`.
* HTML5 ad `index.html` must include a:
  * ```<!DOCTYPE html>``` declaration.
  * ```<html>``` tag.
  * ```<head>``` tag.
  * ```<body>``` tag.
* Zip file may contain any of the other following file types:
  * `.css`, `.js`, `.html`, `.gif`, `.png`, `.jpg`, `.jpeg`, `.svg`
* Subfolders are not allowed.
* HTML5 ad total render size must not exceed 2.1 MB.
* External reference are allowed, but must not exceed 10.
* External references cost against your overall render size limit; however, the following domains are exempt:
  * `s0.2mdn.net/ads/`
  * `ajax.googleapis.com`
  * `fonts.googleapis.com`
  * `fonts.gstatic.com`
  * `tpc.googlesyndication.com`
* If you use a `<video>` or `<audio>` tag you must host the external asset.
* Videos that play by default **must not** play audio by default.
* Audio **must not** play by default.

## API Usage

HTML5 Assets are now available through the Ads endpoint and are returned as a collection of assets under the ad.

HTML5 Assets are not directly accessible. If you make a mistake and need to change an asset after it has been uploaded just delete the ad and recreate it.


## Additional Information

* If you include an `ad.size` meta tag in the ad when you upload it, the system will automatically detect and choose the correct ad size for you automatically. The ad size meta tag is defined within the `<head>` section of the `index.html`. For example:

  ```
  <meta name="ad.size" content="width=300,height=250">
  ```
* Macro replacement is only performed on the `index.html`. Placing macros into referenced javascript files is not supported.
* Expandable ads are not supported.
* When creating ads with the Google Web Designer, you must select "Non-Google Ad" from the Environment drop down list. DoubleClick, AdMob and AdWords environment ads are not supported.
* If you have trouble getting your ad to automatically click-verify, try adding the `clickthru` class to the element that opens the target URL for the ad.
