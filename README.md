# Text Twist Security Analysis By David Boulden
## Write up analyzing text twist web app by Stephen Moss for vulnerabilities.
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
Another possible solution is to create a .htaccess file and deny access to users trying to reach sensitive data with something along the lines of:
```
<files filetohide.sqlite>
order allow,deny
deny from all
</files>
```
### Vulnerability 2: 
