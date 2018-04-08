# currentcy
The objective is to have a CSV file in your dropbox containing monthly exchange rate data with EUR as a base.<br />
The resulting CSV follows this format:
```
201709,EUR,1
201709,USD,1.19
201710,EUR,1
201710,USD,1.18
```
It should be easy to add a new month of data to the file so that in the end a little script could be automatically run every month to update the CSV for you.
## Structure of the solution
It is a very simple node.js (without express.js) back-end server that has an access to your dropbox (to update the csv) and to an api (to get currency data) that will add exchange rates to the CSV on a GET request, for a specific month to be indicated in the URL
## Getting started
### Prerequisites
#### Linux environment
You need to have npm and node.js installed.
#### Currency API
You need to create an account on https://openexchangerates.org/ to get an API key. It is free and you get the right to 1,000 request per month, which is largly sufficient for our use case.
#### Dropbox
You need a dropbox account, of course, and you need to create an app in https://www.dropbox.com/developers/apps.<br />
Choose "Dropbox API".<br />
Then for the type of access I took "full dropbox" because I wanted my CSV to be in a specific shared folder. You can choose "App Folder" if your ok with your CSV being in "Apps/your_app_name/".<br />
Finally you need to go in your new app settings to generate an access token.
### .env
You need to create a ".env" file in your local copy with your own environment parameter. You can reuse the content in "example.env".<br />
* RATE_API_KEY is the openexchangerates API key you retreived in the previous step.
* DBX_TOKEN is the Dropbox token you retreived in the previous step.
* FILE_PATH is the path from the root of your Dropbox (if you choose "Full Dropbox" access type) to the CSV file you want to create and maintain. Format to respect :"/path/to/file.csv" (e.g. "/currency.csv").
## Run it!
This is for running and calling the server on localhost:3000 (assuming you kept the defaults in .env)
### Launch the server
```
npm install
npm run dev
```
### Make a call for march 2016
Click on http://localhost:3000/add/2016-03
### Get historical monthly data from 01/2015 to 12/2017
Install curl if you don't have it. And make sequencial URL call according to https://curl.haxx.se/docs/manpage.html
```
apt-get install curl
curl http://localhost:3000/add/[2015-2017]-[01-12]
```
