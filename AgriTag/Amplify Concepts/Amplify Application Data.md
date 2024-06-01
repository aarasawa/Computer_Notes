#AmplifyGen2 #AWSAmplify 

The file *amplify/data/resource.ts*, contains the application data schema. 

**defineData** function turns the schema into a fully functioning data backend.

Example schema:
``` typescript
const schema = a.schema ({
	Chat: a.model({
		name: a.string(),
		message: a.hasMany('Message', 'chatId'),
	}),
	Message: a.model({
		text: a.string(),
		chat: a.belongsTo('Chat', 'chatId'),
		chatId: a.id()
	}),
});
```
This is a data schema for a messaging application.

On the frontend, *generateClient* gives a typed client instance to integrate CRUD operations for the models in the application code. 
``` typescript
// generate data client using Schema from backend
const client = generateClient<Schema>();

// list all messages
const { data } = await client.models.Message.list();

// create a new message
const { errors, data: newMessage } = await client.models.Message.create({
	text: 'My message text'
});
```