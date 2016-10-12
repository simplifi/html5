#Simpli.fi HTML5 Developer Docs and Samples

##ABOUT
This document describes how to create Simpli.fi compatible HTML5 ads.

##BACKGROUND
A Simpli.fi compatible HTML5 ad has two parts. The first part is your creative, the HTML5 ad itself. The second part are the Simpli.fi Macros, a set of fields that are replaced in the ad creative when it is displayed to users. In order for the ad to function properly you must insert the Simpli.fi Macros into the HTML5 content of your ad.

##What is an HTML5 ad?
HTML5 ads are essentially just web pages, but they conform to a specific set of rules and are sized to fit in a standard ad location. The IAB is currently working on an industry standard set of recommendations that define the specifics of HTML5, but at the time of this writing those recommendations are in draft form. We have been proactively working with the IAB by contributing feedback to their draft and have implemented a number of the existing recommendations already. More information can be found at about HTML5 ads can be found at http://www.iab.net/html5.

##What are the Simpli.fi Macros?
Simpli.fi Macros are placeholders that are used to set replacement values for the ad when the ads are served. You can think of them just like fields in a mail merge document. The list of macros is defined by Simpli.fi and are used in ads to set the target url for clicks, perform cache busting and create dynamic HTML5 ads.

##CREATING A BASIC AD
Getting Started
We’ll begin by creating a very simple custom HTML5 ad and providing the macro for the click tracking to work. Here are the basic steps:
Create a new folder on your computer that will contain the ad.
Add an image. In our example the ad will be a 300x250 ad, so the dimensions of our image will be 300x250.
Add an html page that references the image. Below is the html we will use for the ad.
###BASIC AD HTML
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
###Uploading the ad
Next we’re going to create a zip file that contains the ad html and image file and upload it to the UI.
Save the HTML contents from BASIC AD HTML into a new file named index.html. Next, create a zip file that contains the index.html and 300x250.jpg. NOTE: Only the actual files should be added to the zip. If you include the folder from step 1 above in the zip it will be rejected by the ad validation.
Once you have created the zip file, drag and drop (or click browse) the zip file into your ad campaign in the Simpli.fi UI. The ad will be automatically extracted and its contents will be displayed at the bottom when you open the row.
Use the click verify button to ensure that your ad clicks through to the target URL you specified in the UI. NOTE: If you land on a 403 error page, check to be sure that you have entered a target URL.

##HTML5 Ad Validations
In order for the HTML5 ad to pass validation, your HTML5 ad must meet the following requirements:
* Each file in the zip cannot exceed 250kb in size.
* The overall rendered (unzipped) ad cannot exceed 2mb in size.
* There must be a file named index.html
* HTML5 ad index.html must include:
 * ```<!DOCTYPE html>``` declaration
 * ```<html>``` tag
 * ```<head>``` tag
 * ```<body>``` tag
* The zip file should contain the HTML for the ad as well as any of the other following file types:
 * .CSS
 * .JS
 * .HTML
 * .GIF
 * .PNG
 * .JPG
 * .JPEG
 * .SVG
 * .JSON
* Zip files can contain up to 50 files
* Subfolders are not allowed
* All content used in HTML5 ad must be contained in the ZIP file. No external references are allowed except resources for ```<video>``` and ```<audio>```.
 * If you use of the ```<video>``` or ```<audio>``` tag you must host the external assets.
* Videos that play by default MUST NOT play audio by default.
* Audio MUST NOT play by default.

##API Usage
HTML5 Assets are now available through the Ads endpoint and are returned as a collection of assets under the ad.
HTML5 Assets are not directly accessible. If you make a mistake and need to change an asset after it has been uploaded just delete the ad and recreate it.

##Simpli.fi Macros
```
'{{clickTag}}'             : The URL where clicks should be sent for tracking
'{{targetUrl}}'            : The destination URL of the ad
'{{clickMacro}}'           : The combination of {{clickTag}} and {{targetUrl}}
'{{escapedClickTag}}'      : URL Encoded clickTag
'{{doubleEscapedClickTag}}': Double URL Encoded clickTag
'{{sifiUserId}}'           : The Simpli.fi identifier for this user
'{{sifiImpression}}'       : The URL of the ad at the time it was served
'{{queryParams}}'          : The original query string parameters
'{{exchangeUserId}}'       : The id of the user the exchange has assigned
'{{exchangeId}}'           : The id of the exchange where the ad was bought
'{{keywordId}}'            : The id of the keyword for the transaction
'{{keyword}}'              : The keyword for targeted for the transaction
'{{escapedKeyword}}'       : The keyword in escaped format
'{{cacheBust}}'            : A unique value generated to prevent caching
'{{adId}}'                 : The id of the creative
'{{adPosition}}'           : The position of the creative on the page
'{{adSize}}'               : The size of the creative
'{{campaignId}}'           : The id of the campaign that ran the creative
'{{countryId}}'            : The MAXMIND Country ID
'{{regionId}}'             : The MAXMIND Region ID
'{{metroId}}'              : The MAXMIND Metro ID
'{{geoId}}'                : The MAXMIND Geo ID
'{{userAgent}}'            : The User Agent string sent in the bid request
'{{ip}}'                   : The IP address of the user being served        NOTE: AdX truncates the last octet of the IP so this data may be unreliable.
'{{referer}}'              : The unescaped referrer sent in the bid request NOTE: Not all exchanges forward this data consistently. It may be unreliable.
'{{escapedReferer}}'       : The escaped referrer sent in the bid request   NOTE: Not all exchanges forward this data consistently. It may be unreliable.
```
##Additional Information
* If you include an ad.size meta tag in the ad when you upload it the system will automatically detect and choose the correct ad size for your automatically. The Ad size meta tag is defined within the <head> tag. For example:
```<meta name="ad.size" content="width=300,height=250">```
* Macro replacement is only performed on the index.html. Placing macros into referenced javascript files is not supported.
* Expandable ads are not supported.
* When creating ads with the Google Web Designer you must select Non-Google Ad from the Environment drop down list when creating the ad. DoubleClick, AdMob and AdWords environment ads are not supported.
* Mobile Ad Networks (MoPub) must use target=”_blank” on links due to their limited support for IFrames. See here for further details: https://dev.twitter.com/mopub-demand/marketplace/iframe
