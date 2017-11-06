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

"background": {
    "scripts": ["background.js"],
    "persistent": false/true
}

# Content Script
If you need access to the current page's DOM, then you have to use a content script. The code is run within the context of the current web page, which means that it will be executed with every refresh. To add such a script, use the following syntax.

"content_scripts": [
    {
        "matches": ["http://*/*", "https://*/*"],
        "js": ["content.js"]
    }
]

