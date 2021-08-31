# SMS-Appointment-Reminders

## Introduction
This app connects the appointment data stored in the TrakGene SQL Server database with the SMS provider Tiwlio to send appointment reminders. The operator can configure the reminder time and SMS template in the interface. In addition, the configuration interface provides options for different time zones to automatically start scheduled tasks to send appointment reminders in batches.

## Getting Started
**Installing Node**
  - In order to use Express you will first have to install Nodejs and the Node Package Manager (NPM) on your operating system. 
  - Go to [nodejs](https://nodejs.org/en/) to download the required installer.

**Installing Express**
  - Open a terminal and type `npm install express`.

**Installing dotenv**
  - Type `npm install dotenv` in the command line of the terminal.

**Installing node-mssql to connect Microsoft SQL Server**
  - Type `npm install mssql` in the command line of the terminal.

**Installing Twilio-node**
  - Type `npm install twilio` in the command line of the terminal.

**How To Set Environment Variables for Twilio (Optional)**
  - Please refer to [how-to-set-environment-variables](https://www.twilio.com/blog/2017/01/how-to-set-environment-variables.html) for more details.

**Installing Node-Cron Package**
  - Type `npm install --save node-cron` in the command line of the terminal.
  - Type `npm install --save cron` in the command line of the terminal.

**Installing Moment Timezone**
  - Type `npm i moment-timezone` in the command line of the terminal.

**Start App**
  - Type `npm start` in the root directory to start the app, then open a browser and navigate to [http://localhost:3000/](http://localhost:3000/).

## Development Manual
This app is basically implemented by "MSSQL + Express.js + Node.js + Bootstrap + Pug" stack.

**/node_modules** npm package installation directory

>**/routes** Routing files directory
 - appointments.js: Used to request and response for all pages (GET/POST methods).
 - dboperations.js: Used to connect to MSSQL database, query and update related tables.
 - sendsms.js: Used to introduce Twilio to customize and send reminders to all eligible appointment owners.
 - timezone.js: Used to get and set the time zone of the scheduled task.



