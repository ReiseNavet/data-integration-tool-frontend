# Reisenavet Integration-tool frontend
Frontend for the integration tool built for ReiseNavet/SINTEF.

## User guide

See [wiki/User-guide](https://github.com/Kundestyrt-ReiseNavet/integration-tool-frontend/wiki/User-guide)

## Installation:

* Install [Node](https://nodejs.org/en/download/) to get npm (Node Package Manager).
* Install [Vue CLI](https://cli.vuejs.org/) by running `npm install -g @vue/cli`, to run the Vue dev-server.
* Install [Firebase CLI](https://firebase.google.com/docs/cli) by writing `npm install -g firebase` (for hosting of frontend).
  * To publish, you will require access to the firebase project.
  
* Restart the terminal window.

* Clone the repository into your preferred folder, and `cd` into it. 
* Install dependencies by running `npm install`.
* Run `npm run serve` to run a local development server, and you're there!

NOTE: For functionality, the backend must be running as well.

## Deployment:
Our system is entirely (both front-end and back-end) hosted on SINTEF's server at ProISP. 
The server is available on [this link](http://dataintegrasjon.reisenavet.no/) (not HTTPS), or on IP `46.250.220.200`

Before deployment:

* Install an SFTP-client
  * Windows: [WinSCP](https://winscp.net/eng/download.php)
  * Mac/Linux: [FileZilla](https://filezilla-project.org/download.php?show_all=1)

Deployment:

1. In project-root, run `npm build`. This will build html, css and js-files in a dist-folder (distribution). 
2. Connect to SFTP:
  * Protocol: `SFTP`
  * Hostname/IP: `46.250.220.200`
  * Port: `22`
  * Username: `student`
  * Password: Ask Sebastian or Audun
3. Copy the content of your local dist-folder (the one that was built during step 1) into this the server-folder `/var/www/reisenavet/html`
4. Done! The updated front-end is now available from [dataintegrasjon.reisenavet.no](http://dataintegrasjon.reisenavet.no/).

