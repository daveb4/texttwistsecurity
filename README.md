# Text Twist Security Analysis By David Boulden
## Write up analyzing ![Text Twist web app by Stephen Moss](https://project1-smoss.herokuapp.com/index.html)for vulnerabilities.

### Vulnerability 1: Indexing
The first vulnerability I found was with the indexing of the web page. If a malicious user guesses the names of some of the files or uses something like a metasploit webcrawler to search through the directory that holds the webpage, they can get a hold of sensitive data, such as:
#### The database
![Database Download](/text-twist-screenshots/sqlitedownload.png)
#### or the JSON object:
![JSON Object](/text-twist-screenshots/jsonobject.png)
A possible solution to this vulnerability is to restrict access to these pages by handling the url in the javascript and redirecting the user, an implementation could be something along the lines of:
```javascript
if (window.location.href == <insert sensitive data location here>){
  window.location = <wherever user should be redirected>;
}
```
Another possible solution is to create an htaccess file in the root directory and deny access to users trying to reach sensitive data with something along the lines of:
```
<files filetohide.sqlite>
order allow,deny
deny from all
</files>
```
### Vulnerability 2: POST Request Data
The second vulnerability I found was in the console log POST request of the webpage. The POST request showed the JSON object of each of the possible answers to the rack, so a user could copy the values from the JSON object and enter them in the input box to get maximum points out of each rack.
![POST Request](/text-twist-screenshots/postrequest.png)
Due to the nature of request methods, the user can access the values passed in the requests, so the possible solution I would suggest is using obfuscation. Encoding the values in the front end request and decoding them in the back end with something like an AES encryption would prevent the user from viewing the answers directly without compromising the functionality of the web app.
### Vulnerability 3: Updating variables in Console
