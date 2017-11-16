# Cross Browser Extension Framework
We are in the process of building single code framework for browser extension which works in the same way with all major browsers: Firefox, Chrome, Internet Explorer,Microsoft Edge and Safari.

# Browser Extension
A browser extension is a small software programs that extends the functionality of a web browser. 
Some extensions are authored using web technologies such as HTML, JavaScript, and CSS.

# Background Pages
Every extension has an invisible background page which is run by the browser.

There are two types.

* Persistent pages - It is active, all of the time.
* Event pages - It is active only when it is needed.Google encourages developers to use event pages, because this saves memory and improves the overall performance of the browser.

Here is how you should describe it in the manifest file:

`"background": {
    "scripts": ["background.js"],
    "persistent": false/true
}`

Background pages are long-running scripts that help you manage state and coordinate tasks across extension components

# Content Script
If you need access to the current page's DOM, then you have to use a content script. The code is run within the context of the current web page, which means that it will be executed with every refresh. To add such a script, use the following syntax.

`"content_scripts": [
    {
        "matches": ["http://*/*", "https://*/*"],
        "js": ["content.js"]
    }
]`

Content scripts are arbitrary CSS and Javascript that are injected into selected pages.

# Browser Action
A browser action, which allows us to place a clickable icon right next to Chrome's Omnibox for easy access.Clicking that icon will open a popup window that will allow the user to choose the background color of the current page.

A Browser action appears in the toolbar of every tab.

# Page Action
A page action selectively appears in the omnibox and can be toggled on or off for each tab.

# Manifest File
The very first thing we'll need to create is a manifest file named manifest.json.

It is a metadata file in JSON format that contains properties like your extension's name, description, version number and so on. 

To learn more about the manifest, read the [Manifest File Format documentation](https://developer.chrome.com/extensions/manifest)

# Load the extension
* Visit chrome://extensions in your browser url
* Ensure that the Developer mode checkbox in the top right-hand corner is checked.
* Click Load unpacked extension to pop up a file-selection dialog.
* Navigate to the directory in which your extension files live, and select it.
> If the extension is valid, it'll be loaded up and active right away! If it's invalid, an error message will be displayed at the top of the page. Correct the error, and try again.

# Content Security Policy (CSP)
Let’s define a policy that only allows script to execute when it comes from one of those two sources:
`Content-Security-Policy: script-src 'self' https://apis.google.com`

CSP provides a rich set of policy directives that enable fairly granular control over the resources that a page is allowed to load.
 
script-src is a directive that controls a set of script-related privileges for a specific page.

Four keywords are also accepted in the source list:
* 'none', as you might expect, matches nothing.
* 'self' matches the current origin, but not its subdomains.
* 'unsafe-inline' allows inline JavaScript and CSS
* 'unsafe-eval' allows text-to-JavaScript mechanisms like eval
These keywords require single-quotes. 
script-src 'self' (with quotes) authorizes the execution of JavaScript from the current host.
script-src self (no quotes) allows JavaScript from a server named “self”


# chrome.i18n
Using chrome.i18n, we will implement internationalization across your whole extension.

You need to put all of its user-visible strings into a file named messages.json. Each time you add a new locale, you add a messages file under a directory named _locales/localeCode, where localeCode is a code such as en for English.

The manifest file must define "default_locale".
`Ex: "default_locale": "en"`

In your extension or app's JavaScript code, refer to a string named messagename like this:
chrome.i18n.getMessage("messagename")

Predefined messages:
The internationalization system provides a few predefined messages to help you localize.

Here's an example of using @@extension_id in a CSS file to construct a URL:

`body {
 background-image:url('chrome-extension://__MSG_@@extension_id__/background.png');
}`

# Override Pages
* Allows you to replace:
    * Bookmark Manager
    * History
    * New Tab
* Can contain html,javascript and css

# CRX file
A crx file is really just a zip file of your extension directory plus 2 more things:
* Public key
* Signature - (Generated with private key and zipped content)

# Auto Update
Browser will check that url every few hours for an xml file, and can fetch updated crx files over a plain,non-ssl connection because it check the signature inside the crx file before installing it.
Using "update_url":"http://yourwebsite.com/yourextension.xml" (in your manifest.json file)

If you hosting your extension in our gallery,you don't need to worry about autoupdate, chrome will take care of it for you.

# Notes
* Extension id has made up of 32 characters
* When we designed the system we wanted to have a single globally unique identifier for each extension. So that there are no conflicts with other extensions. The mechanism we settled on uses one public/private key pair per extension with hash of the public key determining the extension's id.
* Google chrome extensions are packaged into "crx" files
* If you are using gallery,we generate the crx file for you when you hit the publish button.
* If you want to host your extension on your own site,you will create the crx file with the "Pack Extension" button on the extensions management page in Google Chrome.
* Make sure your extension UI design is simpler and minimal.
* Fetch public data with XHR
* If you want extension to talk to a server ? Use XmlHttpRequest
* If you want it to presist some data? Use Cookies, LocalStorage or HTML5 Databases.
* An extension is a compressed directory
* Chrome is a global object to which all extension APIs are bound.
* Chrome currently defines about 40 objects and 40 methods. "Chrome" is a name of the top-level object automatically exposed to all extensions.
* Chrome extension has properties and methods. 
* The APIs is split into six modules, which are represented by objects contained in the "chrome" object. 
```
- `chrome.extension.*` that let you to send messages to communicate between extension components ana resolve the URLs of extension files.
- `chrome.browserAction.*`
- `chrome.pageAction.*` that let you enable and disable page actions
- `chrome.windows.*` that let you open,close,look up, and update browser windows. requires tabs permission - windows and tabs are so closely related they share a common permission.
- `chrome.bookmarks.*` requires bookmarks permission.
- `chrome.tabs.*` requires tabs permission.
```
* Using asynchronous APIs is more challenging,but it's in the service of the best user experience possible and It won't take long to get the hang of it.
* Refactor non-presentation code (let's improve the extension's performance and functionality by refactoring)  
* Google Chrome is multi-process architecture which means it will support synchronous/asynchronous APIs is more challenging,but it's in
# Example of a synchronous function

```JS
chrome.browserAction.onClicked.addListener(function(tab)
{
    chrome.tabs.create({url:chrome.extension.getURL('home.html')});
}); 
```

# Example of a asynchronous function
```JS
chrome.bookmarks.update(42,
   {title:"new title"}, 
   function(bookmarkNode){
   
   }
); 
```

# Security Architecture 
It's based on two principles :
* Lease Privilege
* Privilege Separation

# Architecture
Chrome
* manifest.json file.
* Background page - invisible page that holds your extension's main logic.
* Options page. - Allows users to configure your extension. Use localStorage to save option or Use chrome.storage(Supports the storage of objects.Data is synced with Chrome Sync.  
* Override pages.
* Popup
* Content Script - Used to interact with content loaded into the browser.
* Arbitrary Pages that you can show with chorme.tabs.create() or window.open()

# Ref Urls
* [Learn Basic](https://developer.chrome.com/extensions)
