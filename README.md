# 604_web_services_assignment

The implementation of the blog on Google App Engine was not successful, but of all of the components of the blog were successfully implemented via Salesforce. Even though the blog doesn't work on Google App Engine, Google App Engine can still be requested successfully for the example given. Directions to cURL both the Salesforce blog and the Google App Engine app are presented below. All of the .java files are the unchanged files provided with Google's example. These are executed when using cURL to call Google App Engine. All of the .apex files are the files that implement the Salesforce REST service blog. These are executed when using cURL to call Salesforce.

To call Google App Engine:

curl -H "Content-Type: application/json" -X POST -d '{"message":"hello world"}' https://test-project-174900.appspot.com/_ah/api/echo/v1/echo

(1) "hello world" can be replaced with any other in quotes text and that message will be returned


(2) if a message is recieved about being temporarily over the serving quota, type the exact same cURL command replacing "test-project-174900" with "green-diagram-174817". This performs the same action.
