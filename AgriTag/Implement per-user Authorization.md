#AWSAmplify #Authorization

The following code is being added to *amplify/data/resource.ts*:
``` typescript
1...
const schema = a.schmea({
	Todo: a
		.model({
			content: a.string(),
		})
		.authorization(allow => [allow.owner()])
});

2...
export const data = defineData({
	schema, 
	authorizationModes: {
		defaultAuthorizationMode: 'userPool',
	}	
});
```

###### 1. Schema Definition
A schema model named **Todo** has a single field *content* of type string. The part with *.authorization* specifies that only the owner of the Todo item can modify it. 

###### 2. Authorization Modes
*Configures authorization mode for the schema*. It indicates that authentication and authorization are managed using Amazon Cognito User Pool. 

###### Owners and User Pools
**User Pool Membership**: owners of Todo must be authenticated users part of the Cognito User Pool. Because *userPool* authorization mode relies on Cognito to authenticate users and manage their identities. 

**Owner Authorization**: *allow.owner()*. specifies only the user who created the Todo item (owner) has permission to modify it. Cognito User Pools manage user identities and provide necessary user information (userID) to enforce this rule. 