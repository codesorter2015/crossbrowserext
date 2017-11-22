# Chrome Extension Inline Installation
Inline installation is composed of two parts:
* A declarative <link> tag
* A call to the JavaScript function chrome.webstore.install().

# Step 1: Verified site requirement
For security reasons, inline installations can only be initiated by a page on a site that is verified as being associated with that item in the Chrome Web Store. 
[webmasters](https://www.google.com/webmasters/tools/home?hl=en)

# Step 2: Go to the Chrome Developer Dashboard
[Chrome Developer Dashboard](https://chrome.google.com/webstore/developer/dashboard)
Click the name of the relevant extension and get item id from here.

# Step 3: Enable inline install
There is an option for inline install which you need to enable if you want inline installation.

# Step 4: Websites option
You will need to choose a website linked to your Google account. This will be the site where users will be able to do direct installation of the extension.

# Step 5: Add the google site verification code into your website
<meta name="google-site-verification" content="Dz-jhfg8795834984534534VLTNjmDuppIps-vgfhfgGG" />

# Step 6: Adding a Chrome Web Store link in the Website
One or more <link> tags in the <head> section referencing the items that the user can install. 
Each <link> tag must have the following format:
`<link rel="chrome-webstore-item" href="https://chrome.google.com/webstore/detail/itemID">`
Replace the itemID with actual item id(Check Step2)

# Step 7: Add the below code in the inside <body> tag

```
<a class="btn default" id="btnAct" href="javascript:chrome.webstore.install('https://chrome.google.com/webstore/detail/jgbloeglgbldipmjdeegdeibgehdcofk', successCallback, failureCallback)" style="padding:0 10px;">Activate</a>
<script>
    function successCallback(){
        alert("Install Successfully...!");
    }
    function failureCallback(){
        alert('Some error occured while installation.');
    }
```

# Reference URls as belows:
* You can refer to the Inline Install documentation from Google [here](https://developer.chrome.com/webstore/inline_installation?hl=en).
* [setup-chrome-extension-for-inline-installation](http://noelarlante.com/setup-chrome-extension-for-inline-installation/)

