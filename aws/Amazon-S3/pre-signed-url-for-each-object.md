# Generate a Pre-signed URL To Download Every Object In S3

The following code snippet generates a `GET pre-signed URL` for every object in a S3 bucket:
- Write a list of S3 object in to a `*.json` file
    - valid `*json` is created
- Read S3 content and parse `*json` file
- Iterate over the S3 content and print out key:value - `valueID`
- Extract only `valueID` from the array
- Generate GET pre-signed URL for the specific S3 object
- Push GET pre-signed URL into array
- Create a valid JSON again and write GET pre-signed URLs into the file for the later use

```javascript
// Create pre-signed GET URL for every object in S3
function getObject(){
try {
  const s3 = new AWS.S3();
  // List content of the S3 bucket
  const params = {
    Bucket: 'test-bucket', /* required */
    // Prefix: 'values'  // Can be your folder name
  };
  s3.listObjectsV2(params, function(err, data) {
    // an error occurred
    if (err)
      console.log(err, err.stack);
    // successful response
    else
      // Write S3 bucket content into JSON file (create a valid JSON file)
      bucketRawContent = JSON.stringify(data)
      fs.writeFileSync('bucketRawContent.json', s3BucketRawContent);

      // Read S3 bucket content (parse JSON file)
      rawdata = fs.readFileSync('bucketRawContent.json');
      bucketParsedContent = JSON.parse(rawdata);

      // Iterate over S3 bucket content and print value ID
      let listOfPreSignedGetUrl = []
      for (let i = 0; i < bucketParsedContent.Contents.length; i++)
      {
        // Extract only value ID
        valueID = bucketParsedContent.Contents[i].Key
        valueID = valueID.substring(valueID.indexOf("/") + 1);

        // Generate the pre-signed GET URL.
        preSignedGetURL = s3.getSignedUrl('getObject', {
        Bucket: 'test-bucket/values',
        Key: `${valueID}`, //filename
        Expires: 3600 //time to expire in seconds
        })

        // Push pre-signed GET URLs into the array
        listOfPreSignedGetUrl.push(preSignedGetURL)
      }
      console.log('Pre-signed GET URL:', listOfPreSignedGetUrl)

      // Create a valid JSON again and write pre-signed GET URLs into the file
      const getUrl = JSON.stringify(listOfPreSignedGetUrl, null, 4);

     // Write list of GET pre-signed URL in to a JSON file
      fs.writeFile("preSignedGetUrl.json", getUrl, 'utf8', function (err) {
        if (err) {
            console.log("An error occured while writing JSON Object to File.");
            return console.log(err);
        }
    });
  });
  } catch (error) {
    console.log('Error ---->')
    console.log(error)
  }
}

````
