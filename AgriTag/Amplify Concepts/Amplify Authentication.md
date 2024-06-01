#AWS #AmplifyGen2 #Authentication

The **Authenticator** offers a way to add authentication flows into the app. Encapsulating authentication workflow, backed by backend Auth resources. Powered by Amazon Cognito.

*Authentication* is a process to validate who users are. A system that validates is referred to as an *Identity Provider* or *IdP.* Typical IdP's these days are Facebook, Google, etc.

##### Username Authentication
**Username attributes** in Cognito can be configured to accept an email or a phone number as the "username". Verification of ownership to specified email or phone number to confirm the account is necessary. It is common to consider a "username" for display purposes. 
``` ts
userAttributes: {
	preferredUsername: {
		mutable: true,
		required: false
	}
}
```

However, this is not the type of username that users can sign in with, it more *masks personal information* like email or phone number. To allow users to sign up with an immutable username, use *CDK to modify auth resource's* **usernameAttributes** configuration directly.

Attributes can be configured to be *required* for user sign-up in addition to whether the values are *mutable*. Additional attributes can be configured to be optional, and mutable after sign-up. 

##### Multi-Factor Authentication
###### Configuration MFA
**defineAuth** is used to enable MFA for your app. 

###### MFA Options
**MFA enforcement** whether to require it or not. If it is required, all users will need to complete MFA to sign in. If optional, users have a choice. 
**MFA methods** between *TOTP, SMS, or both*. It is recommended to use TOTP-based MFA and save SMS for account recovery. 

###### MFA with SMS
An *origination number*, is required for setting up SMS authentication codes. 

##### Enable TOTP after a user is signed in
TOTP MFA can be setup after a user has signed in. The conditions for this are:
- MFA marked *Optional* or *Required* in user pool
- 