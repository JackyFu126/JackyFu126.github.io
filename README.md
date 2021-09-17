# SMS-Appointment-Reminders

## Introduction
This app connects the appointment data stored in the TrakGene SQL Server database with the SMS provider Tiwlio to send appointment reminders. The web homepage displays appointment information for users who are eligible to send reminders. The operator can configure the reminder time and SMS template in the interface. In addition, the configuration interface provides options for different time zones to automatically start scheduled tasks to send appointment reminders in batches.

## Getting Started (Only For Developers)
**Installing Node**
  - In order to use Express you will first have to install Nodejs and the Node Package Manager (NPM) on your operating system. 
  - Go to [nodejs](https://nodejs.org/en/) to download the required installer.

**Installing Express**
  - Open a terminal and type `npm install express`.

**Installing dotenv**
  - Type `npm install dotenv` in the command line of the terminal.

**Installing node-mssql to connect Microsoft SQL Server**
  - Type `npm install mssql` in the command line of the terminal.
  - If you encounter problems like *`Failed to connect to localhost:1433-Could not connect (sequence)`* when accessing SQL server Data in node js, please refer to [stackoverflow](https://stackoverflow.com/questions/25577248/node-js-mssql-tedius-connectionerror-failed-to-connect-to-localhost1433-conn)/[video](https://www.youtube.com/watch?v=boVqsffat0Q) to congirue the TCP/IP service of SQL Server Network Configuration.

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

>**/node_modules**: Directory of npm installation package.

>**/routes**: Directory of routing files.
 - **appointments.js**: Used to request and response for all pages (GET/POST methods).
 - **dboperations.js**: Used to connect to MSSQL database, query and update related tables.
 - **sendsms.js**: Used to introduce Twilio to customize and send reminders to all eligible appointment owners.
 - **timezone.js**: Used to get and set the time zone of the scheduled task.

>**/views**: Directory of Pug template files.
 - **layout.pug**: The main interface displaying all eligible appointment owners to send SMS.
 - **index.pug**: The auxiliary interface showing customized appointment reminder information.
 - **configSMS.pug**: The SMS Config interface used to display the fields in the kt_sms_config table so that system administrators can specify the customized notification text and the time before appointment date to send reminders.
 - **configTimeZone.pug**: The Time Zones Config interface for configuring time zones to launch scheduled tasks.
 - **error.pug**: The page showing the error message.

>**app.js**: App entry file.

>**.env** The environment variable file is used to store Twilio's confidentials and database connection data.
  - **Twilio's confidentials**: You can find your **TWILIO_ACCOUNT_SID** and **TWILIO_AUTH_TOKEN** in your [Twilio Account Settings](https://console.twilio.com/?frameUrl=%2Fconsole%3Fx-target-region%3Dus1). You will also need a **Twilio_Phone_Number**, which you may find [here](https://console.twilio.com/us1/develop/phone-numbers/manage/active?frameUrl=%2Fconsole%2Fphone-numbers%2Fincoming%3Fx-target-region%3Dus1).

>**config.js**: Used to read .env data to connect to the TrakGene SQL Server database and Twilio server.

>**scheduler.js**: Used to launch a scheduled task according to the specified time zone.

>**/notifications**
  - **notificationsWorker.js**: Used to call sendsms.js to send notifications at the specified time.

>**package.json/package-lock.json**:. Used to record the configuration information of the project, and the dependencies of various modules.

>**kt_sms_config**: This new table is created in the TrakGene database to record the SMS configuration updates.
  - **timeBeforeApptToSend(int)**: Specify a reminder time before the appointment date to send SMS.
  - **customNotificationText(text)**: Customize the notification text.

## Deployment
  - Type `npm run build-package` in the command line of the terminal.
  - Click the genetated "sms-appointment-reminders.exe" to run the app in Windows.
  - For testing, you can access [Logs/Messaging](https://console.twilio.com/us1/monitor/logs/sms?frameUrl=%2Fconsole%2Fsms%2Flogs%3F__override_layout__%3Dembed%26bifrost%3Dtrue%26x-target-region%3Dus1&currentFrameUrl=%2Fconsole%2Fsms%2Flogs%3F__override_layout__%3Dembed%26bifrost%3Dtrue%26x-target-region%3Dus1) to check whether the SMS was sent successfully.
