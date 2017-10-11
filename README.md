# Basic Structure API.AI Facebook Chatbot with Nodejs and Typescript

Basic structure of Facebook Chatbot connected to API.AI (now Dialogflow 🙂), using Typescript.

On the following tutorial you can see the process of creating a Facebook application and API.AI agent and more:

http://www.girliemac.com/blog/2017/01/06/facebook-apiai-bot-nodejs/


## Dependencies
apiai: "^4.0.3"

body-parser: "^1.18.2"

express: "^4.16.2"

request: "^2.83.0"

@types/node: "^8.0.33"


## Install and Run

Install dependencies: 
```
npm install
```

In one terminal, http ngrok server:
```
ngrok http 5000
```

Use the https url in 'Edit Subscription' in Webhook section of your Facebook App.

Install Typescript:
```
npm install -g typescript
```

In other terminal on project root directory:

Compile Typescript
```
tsc
```

Compile after any change
```
tsc --watch
```

Finally, in other terminal run with: 
```
node .\build\webhook.js
```


## API.AI
We can connect this project to API.AI (Dialogflow) in two ways.

1 . Using the Nodejs library 'apiai'

```
    let apiai = apiaiApp.textRequest(text, {
        sessionId: sender // use any arbitrary id
    });

    apiai.on('response', (response) => {
        let aiText = response.result.fulfillment.speech;
        //...
    });

    apiai.on('error', (error) => {
        //...
    });

    apiai.end();
```

2 . Telling the API.AI project that send POST to a URL from our Express server.
   This is done in the 'Fulfillment' section, indicating the URL to which send the POST.
   
   For example, in '/ai':
```
app.post('/ai', (req, res) => {
  if (req.body.result.action === 'myAction') {
    let oneParameter = req.body.result.parameters['param1'];

    return res.json({
          speech: msg,
          displayText: msg,
          source: 'myAction'});

  }
}
```