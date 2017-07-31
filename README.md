# 604_web_services_assignment

My blog was created using Salesforce. After spending a few days trying to figure out Google App Engine, given the time constraints, I did not have the ability to traverse through the tree of information that I didn't know to get a working blog on Google App Engine. So I frankensteined together an alternate solution that meets all of the basic requirements for the assignment:
(1)The blog is implemented via Salesforce, and can be successfully called via cURL for all requirements. The .apxc file is the apex file controlling the salesforce blog.
(2)My Google App Engine backend can still be successfully called via cURL, but it performs a different function than the blog. The .java files are the default echo example files.



TO CALL THE BLOG VIA CURL:

-First you need to get the access token to call the web service. To get it, enter the following text into the terminal verbatim:
curl -v https://login.salesforce.com/services/oauth2/token -d "grant_type=password" -d "client_id=3MVG9CEn_O3jvv0zxKlX1XJsby8v5Sfw62FcBeyGWwA5z887eOFNrf7U50pIcH9XD7lf31obTdOQua2V1R7E2" -d "client_secret=7700008400078563904" -d "username=cawilson1@gmail.com" -d "password=1234chope8gISpn4reHK2QCICAukAoyW" -H 'X-PrettyPrint:1'

-For each of the subsequent calls, the text in the "access_token" field of the JSON response will have to be used in the "Authorization: Bearer" header. Just replace whereever I've written "<access_token>" with the actual access token when using cURL requests. The blogposts are numbered starting at index 0, which is how they are identified. Below are the cURL formats for POST, GET, DELETE, and PUT.


for POST:
curl https://na50.salesforce.com/services/apexrest/blog/ -H "Content-Type: application/xml" -H 'Authorization: Bearer <access_token>' -H 'X-PrettyPrint:1' -X POST -d '<request><blogtext>ENTER TEXT HERE</blogtext></request>'

-Any text between "<blogtext>" and "</blogtext>" will be the text in the blog post.


for GET:
curl https://na50.salesforce.com/services/apexrest/blog/0 -H "Content-Type: application/xml" -H 'Authorization: Bearer <access_token>' -H 'X-PrettyPrint:1' -X GET

-Type the number of the blogpost that you want to retrieve at the end of the URL after "blog/". Blog posts start at 0 and each new post is appended and has an incremented index. The example above calls a GET service for blog 0 (i.e. the first blog).


for DELETE:
curl https://na50.salesforce.com/service/apexrest/blog/1 -H "Content-Type: application/xml" -H 'Authorization: Bearer <access_token>' -H 'X-PrettyPrint:1' -X DELETE

-Sometimes this process has a delay of a few minutes.


for PUT:
curl https://na50.salesforce.com/services/apexrest/blog/0 -H "Content-Type: application/xml" -H 'Authorization: Bearer <access_token>' -H 'X-PrettyPrint:1' -X PUT -d '<request><blogtext>ENTER TEXT HERE</blogtext></request>'

-PUT is the only one that has both XML to change the blog's text and an integer at the end of the URL. As before, the number at the end of the URL dictates which blog to update, and the text in between "<blogtext>" and "</blogtext>" becomes the new text for that blogpost.




TO CALL THE GOOGLE APP ENGINE ENDPOINT:

Even though the blog doesn't work on Google App Engine, Google App Engine can still be requested successfully for the Google's echo example. Directions to cURL the Google App Engine app are presented below. 


curl -H "Content-Type: application/json" -X POST -d '{"message":"hello world"}' https://test-project-174900.appspot.com/_ah/api/echo/v1/echo

(1) "hello world" can be replaced with any other in quotes text and that message will be returned
(2) if a message is recieved about being temporarily over the serving quota, type the exact same cURL command replacing "test-project-174900" with "green-diagram-174817". This performs the same intended action.
