# !!! Important Notice !!!

Dropbox has changed this API and this does not work anymore. (that is the unfortunate fate of undocumented APIs...)


# dropbox-comments-downloader

A quick and dirty dropbox comments download tool (with undocumented /comments2/list_comments API)

# Test

You can test it here : https://rpeyron.github.io/dropbox-comments-downloader/dropbox-comments-downloader.html

# Use

1. Authenticate using the "Authenticate" button, you will be asked to log on your dropbox account and accept to give access to the "Comments Downloader" application. You may have a security warning as this application is not often used. You can read the source before to be sure it does nothing harmful.
2. Select a file in your dropbox with the "Select" button. For now you can only download comments from your own dropbox, but the API should work on other files you have access (with another file selector)
3. An overview of the comments will be printed below with the page number, the author, and the text of the comment
4. The full JSON of the comments is downloadable by clicking on the "Download JSON" button. You will get the raw JSON with all the comments features (threads, indicators, comment location,...)

# Install on your server

To install it on your own server you must create your own Dropbox application :
- Go to : https://www.dropbox.com/developers/apps/
- Create a new application
- Update the code with your *APP key* ; you must change two places :
  * In the data-app-key field of the javascript for dropin : `<script type="text/javascript" src="https://www.dropbox.com/static/api/2/dropins.js" id="dropboxjs" data-app-key="<your APP key>"></script>`
  * In the beginning of the script : `var CLIENT_ID = '<your APP key>';`
- Add the the URL of your file in the Redirect URIs list of your application in the Dropbox console
- Add the domain you are using in the Chooser/Saver domains list of your application in the Dropbox console
  
# Develop

You will see in the code that there is a strange Dropbox javascript file inclusion :
- one is fot the Dropbox javascript API
- one is for the Chooser component (as I am too lazy to rewrite it)

Unfortunately the two javascript libraries are not compatible, and both redefine and needs the Dropbox global variable. That is why I save it before loading the next library. It is ugly, I hope Dropbox will make the two libraries compatible !

In fact, as list_comments is not included in the javascript API, I am using the HTTP API and the inclusion of the Dropbox javascript API is useless for now, but I left it because it could be handy for future improvements.
