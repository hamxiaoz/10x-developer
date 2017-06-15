# Actions on Google / Google Assistant

#### How does Actions on Google work?
10k view:   
`voice -> parse (via API.AI) -> fullfillment (via API.AI or Lambda)`

Detail view:   
`Voice -> API.AI -> Intents -> Entity (similar to enum) + Action (ex, 'list.tasks') -> Response: in API.AI or webhook (-> Lambda)`

For fullfillment, you can use local machine with ngrok or, you can deploy Lambda directly to staging.

## Actions on Google
Componenet:
- https://github.com/actions-on-google/conversation-components-nodejs/blob/master/api-ai/index.js
- https://developers.google.com/actions/reference/nodejs/Carousel

Sample with Lambda:
- https://github.com/bradyholt/google-action-tiger/blob/master/lambda-function/index.js

## API.AI 
the doc is outdates, UI is different now
- https://docs.api.ai/docs/concept-events


---

## TODO
- Get Started page: https://developers.google.com/actions/distributing-your-apps
- https://developers.google.com/actions/components/
- Deployment guide: https://developers.google.com/actions/apiai/deploy-fulfillment
