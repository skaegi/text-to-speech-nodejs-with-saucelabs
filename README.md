# Example of an IBM Bluemix DevOps Services Toolchain integrated with Sauce Labs

(work in progress)

<!-- A simple pipeline with a HelloWorld Node.js application that runs tests via Sauce Labs. This is an easy way to get a pre-configured pipeline with all the environment variables set and ready to go! The Sauce Labs username and API key fields will need to be filled in with valid information before the stage will run correctly.-->

Give it a try! Click the button below to fork into IBM DevOps Services and deploy your own copy of this application on Bluemix, with a DevOps toolchain already configured and waiting for you to engage.

[![Deploy To Bluemix](https://bluemix.net/deploy/button.png)](https://dev01.hub.jazz.net/deploy/index.html?repository=https://github.com/skaegi/text-to-speech-nodejs-with-saucelabs&otc=true)

## Text to Speech Nodejs Starter Application

  The IBM Watson [Text to Speech][service_url] service is designed for streaming, low latency, synthesis of audio from text. It is the inverse of the automatic speech recognition. The TTS service can be accessed via a REST interface or directly via TCP.

## Getting Started

1. Create a Bluemix Account

    [Sign up][sign_up] in Bluemix, or use an existing account. Watson Services in Beta are free to use.

2. Download and install the [Cloud-foundry CLI][cloud_foundry] tool

3. Edit the `manifest.yml` file and change the `<application-name>` to something unique.
  ```none
  applications:
  - services:
    - text-to-speech-service
    name: <application-name>
    command: node app.js
    path: .
    memory: 256M
  ```
  The name you use will determinate your application url initially, e.g. `<application-name>.mybluemix.net`.

4. Connect to Bluemix in the command line tool.
  ```sh
  $ cf api https://api.ng.bluemix.net
  $ cf login -u <your user ID>
  ```

5. Create the Text to Speech service in Bluemix.
  ```sh
  $ cf create-service text_to_speech standard text-to-speech-service
  ```

6. Push it live!
  ```sh
  $ cf push
  ```


## Running locally
  The application uses [Node.js](http://nodejs.org/) and [npm](https://www.npmjs.com/) so you will have to download and install them as part of the steps below.

1. Copy the credentials from your `text-to-speech-service` service in Bluemix to `app.js`, you can see the credentials using:

    ```sh
    $ cf env <application-name>
    ```
    Example output:
    ```sh
    System-Provided:
    {
    "VCAP_SERVICES": {
      "text_to_speech": [{
          "credentials": {
            "url": "<url>",
            "password": "<password>",
            "username": "<username>"
          },
        "label": "text_to_speech",
        "name": "text-to-speech-service",
        "plan": "free"
     }]
    }
    }
    ```

    You need to copy `username`, `password` and `url`.

2. Install [Node.js](http://nodejs.org/)
3. Go to the project folder in a terminal and run:
    `npm install`
4. Start the application
5.  `node app.js`
6. Go to `http://localhost:3000`

## Troubleshooting

To troubleshoot your Bluemix app the main useful source of information are the logs, to see them, run:

  ```sh
  $ cf logs <application-name> --recent
  ```

## License

  This sample code is licensed under Apache 2.0. Full license text is available in [LICENSE](LICENSE).

## Contributing

  See [CONTRIBUTING](CONTRIBUTING.md).

## Open Source @ IBM
  Find more open source projects on the [IBM Github Page](http://ibm.github.io/)

[service_url]: http://www.ibm.com/smarterplanet/us/en/ibmwatson/developercloud/text-to-speech.html
[cloud_foundry]: https://github.com/cloudfoundry/cli
[sign_up]: https://apps.admin.ibmcloud.com/manage/trial/bluemix.html?cm_mmc=WatsonDeveloperCloud-_-LandingSiteGetStarted-_-x-_-CreateAnAccountOnBluemixCLI
