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

# Content Script
If you need access to the current page's DOM, then you have to use a content script. The code is run within the context of the current web page, which means that it will be executed with every refresh. To add such a script, use the following syntax.

`"content_scripts": [
    {
        "matches": ["http://*/*", "https://*/*"],
        "js": ["content.js"]
    }
]`

# Browser Action
A browser action, which allows us to place a clickable icon right next to Chrome's Omnibox for easy access.Clicking that icon will open a popup window that will allow the user to choose the background color of the current page.

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
