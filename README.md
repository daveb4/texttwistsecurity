# Text Twist Security Analysis By David Boulden
## Write up analyzing text twist web app by Stephen Moss for vulnerabilities.
### Vulnerability 1: Indexing
The first vulnerability I found was with the indexing of the web page. If a malicious user guesses the names of some of the files or uses something like a metasploit webcrawler to search through the directory that holds the webpage, they can get a hold of sensitive data, such as:
#### The database
![Database Download](/text-twist-screenshots/sqlitedownload.png)
#### or the JSON object:
![JSON Object](/text-twist-screenshots/jsonobject.png)
