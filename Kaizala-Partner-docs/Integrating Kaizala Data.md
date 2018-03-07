## Integrating Kaizala Data to your existing dashboards

###### Create custom report or plug your Kaizala data to your existing dashboards using Kaizala APIs. 
###### As a third party organization - You want to plug Kaizala data to your existing dashboard, then you can do it using the following ways: 
###### 1. Get Kaizala data through Power BI-Content Pack and create a Custom report on PowerBI 
###### 2.Access Kaizala data through connectors and pass on to  existing dashboard in the format that it understands. You can access data using Kaizala Connecters:  
###### a.[APIs](https://docs.microsoft.com/en-us/kaizala/connectors/api)  - Kaizala Connectors enable 3rd party developers to integrate Kaizala into their business processes by providing the ability to perform a curated set of actions in Kaizala using REST based API calls. The scope of the API is for external systems to call the end-point and perform actions on-demand. That is, this will be a PULL model – where individual endpoints need to be called to perform specific actions using Kaizala API's. 
###### b.[webhooks](https://docs.microsoft.com/en-us/kaizala/connectors/webhooks) - The PUSH model where Kaizala platform can trigger actions can be configured using webhooks.  
###### Kaizala Connectors enable 3rd party developers to integrate Kaizala into their business processes by providing the ability to perform a curated set of actions in Kaizala using REST based API calls. The scope of the API is for external systems to call the end-point and perform actions on-demand. That is, this will be a PULL model – where individual endpoints need to be called to perform specific actions using Kaizala [APIs](https://docs.microsoft.com/en-us/kaizala/connectors/api). The PUSH model where Kaizala platform can trigger actions can be configured using [webhooks](https://docs.microsoft.com/en-us/kaizala/connectors/webhooks). 
![](https://github.com/Microsoft/kaizala-docs-preview/blob/harishvalurouthu-patch-1/kaizala/PartnerDocs/Images/GetImage.png)
##### Integration Using Webhooks: 
###### This is a PUSH based mechanism. Once Webhook is registered on particular action, Whenever user submits data on that action on Kaizala Application - Kaizala Server will send a event notification (HTTP POST message) with response payload (JSON Format) to the configured URL endpoint. Once data is notified on customers endpoint, Logic for parsing the response payload should trigger and Insert data in to the respective tables in the storage (Database or sharepoint,..) and Visualizations can be built by querying data from the storage. Advantage of this is any Organization can get Kaizala data in to their Custom dashboards without disrupting their existing work flows. 
###### Lets drill down in to the above process and see it in detail: 
#### How to register a webhook on endpoint? 
###### Once you configure a URL endpoint on which you wanted to notify the Kaizala events, You can subscribe for a notification on the group or a particular  action. You can use the 3rd party Rest API clients like  Postman/ Advanced Rest Client, etc. to subscribe for a webhook. Signature of registering a webhook on particular Action is given below: 
![](https://github.com/Microsoft/kaizala-docs-preview/blob/harishvalurouthu-patch-1/kaizala/PartnerDocs/Images/GetImage_2.png)
###### Go to [Kaizala API Documentation!](https://docs.microsoft.com/en-us/kaizala/connectors/api) and click on the
![](https://github.com/Microsoft/kaizala-docs-preview/blob/harishvalurouthu-patch-1/kaizala/PartnerDocs/Images/GetImage%20_1.png)
#####  Go through the steps to get the AccessToken and register a wekbhook. 
 
###### As you have now registered a webhook, Kaizala server will keep notifying the events on the registered URL every time event occurs. Event response is in the below JSON format: 
 
###### Sample Event Response in JSON: 
###### {   
###### "objectId":"com.microsoft.kaizala.OrderFormDemo", 
###### "objectType":"ActionPackage", 
###### "eventType":"ActionResponse", 
###### "eventId":"75609730-f5d2-4f07-XXXX-ccca96dd9e76", 
###### "data":{   
###### "actionId":"eb40446b-3dc7-4e8e-XXXX-44ccc5ae760c", 
###### "actionPackageId":"com.microsoft.kaizala.OrderFormDemo", 
###### "packageId":"com.microsoft.kaizala.OrderFormDemo", 
###### "groupId":"af461a3c-49cf-47cf-XXXX-83b5d348318d", 
###### "responseId":"75609730-f5d2-4f07-XXXX-ccca96dd9e76", 
###### "isUpdateResponse":false, 
###### "responder":"+911234567890", 
###### "responderName":"FooName", 
###### "responderProfilePic":"", 
###### "isAnonymous":false, 
###### "responseDetails":{   
###### "responseWithQuestions":[   
###### {   
###### "title":"Retailer Outlet", 
###### "type":"SingleOption", 
###### "options":[   
###### {   
###### "title":"ABC Traders" 
###### }, 
###### {   
###### "title":"BCD Distributors" 
###### }, 
###### {   
###### "title":"EFG wholesale" 
###### } 
###### ], 
###### "answer":[   
###### "ABC Traders" 
###### ] 
###### }, 
###### {   
###### "title":"Rice 1KG", 
###### "type":"Numeric", 
###### "options":[   
###### ], 
###### "answer":1.0 
###### }, 
###### {   
###### "title":"Rice 5KG", 
###### "type":"Numeric", 
###### "options":[   
###### ], 
###### "answer":2.0 
###### }, 
###### {   
###### "title":"Mixed Fruit Juice 250ml", 
###### "type":"Numeric", 
###### "options":[   
###### ], 
###### "answer":4.0 
###### }, 
###### {   
###### "title":"Location", 
###### "type":"Location", 
###### "options":[   
 
###### ], 
###### "answer":{   
###### "lt":99.1234567, 
###### "lg":88.1234567, 
###### "n":"FooAddress" 
###### } 
###### } 
###### ] 
###### } 
###### }, 
###### "context":"Any data which is required to be returned in callback. Current webhook data can be seen by refreshing:[: https://requestb.in/12786un1?inspect!](https://requestb.in/12786un1?inspect)
###### "fromUser":"+911234567890", 
###### "fromUserName":"FooName", 
###### "fromUserProfilePic":"" 
###### } 
###### On the Registered End Point - Have business logic to parse the event response and insert data in to the respective storage tables. As data is now available at your end, Query data from storage and show visualizations on your existing dashboards. With this approach - You can create the visualizations of Kaizala data on existing dashboards. In this approach you will be getting the data notified in Realtime using the Webhook end point.  
#### How to PULL data using Kaizala API's? 
###### If you want to Pull data from Kaizala in regular Intervals and update data in the dashboard- then You can call Kaizala API's using Connectors and Pull data for the required Action Package, update data in to the Storage and refresh Dashboard. 
###### For Querying the responses of an Action Package - You can see the API signature and the response by Going to the Postman collection mentioned above and go to Content Query API's--> Fetch action responses in a group and replace with your group, action package details and  
![](https://github.com/Microsoft/kaizala-docs-preview/blob/harishvalurouthu-patch-1/kaizala/PartnerDocs/Images/GetImage_3.png)
