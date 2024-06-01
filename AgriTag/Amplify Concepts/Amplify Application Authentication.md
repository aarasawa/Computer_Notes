#AmplifyGen2 #AWSAmplify  #Authentication 

The auth works similar to data. The file for configuration and schemas is in *amplify/auth/resource.ts.*

For example, you can change the verification email subject line:
``` typescript
export const auth = defineAuth({
	loginWith: {
		email: {
			verificationEmailSubject: 'Welcome 👋 Verify your email!'
		}
	}
});
```

Authentication flow with customized sign-in and registration flow, MFA, and 3rd-party social providers. **Cognito** is added to AWS account when auth is added to the application. 
``` typescript
import { withAuthenticator } from '@aws-amplify/ui-react';
function App({ 
	signOut,
	user
}) {
	return (
		<>
		<h1> Hello {user.username} </h1>
		<button onClick={ signOut }> Sign out </button>
		</>
	);
}
export default withAuthenticator(App);
```