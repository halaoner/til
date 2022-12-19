# Generate AWS Temporary Credentials

The following code snippet generate AWS temporary credentials done by [AWS SDK for JavaScript](https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/welcome.html).

> NOTE: Identity Pool must be created!

```javascript
// Set the region where your identity pool exists.
AWS.config.region = 'eu-east-1';

// Configure the credentials provider to use your identity pool.
AWS.config.credentials = new AWS.CognitoIdentityCredentials({
    IdentityPoolId: 'eu-east-1:8bb01198-b1dc-4a1c-b11f-5822e7e891c4',
});
    // Make the call to obtain credentials.
    AWS.config.credentials.get(function(){

    // Credentials will be available when this function is called.
    const accessKeyId = AWS.config.credentials.accessKeyId;
    const secretAccessKey = AWS.config.credentials.secretAccessKey;
    const sessionToken = AWS.config.credentials.sessionToken;

    console.log('Obtaining AWS temporary credentials from Amazon Cognito...');

    AWS.config.update({credentials: AWS.config.credentials, region: 'eu-east-1'});
    // Call some function here
    getObject()
});
```