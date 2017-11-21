# Inline Installation
Inline installation is composed of two parts:
* A declarative <link> tag
* A call to the JavaScript function chrome.webstore.install().

# Adding a Chrome Web Store link
One or more <link> tags in the <head> section referencing the items that the user can install. 

Each <link> tag must have the following format:

`<link rel="chrome-webstore-item" href="https://chrome.google.com/webstore/detail/itemID">`

