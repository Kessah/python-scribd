<pre>
class *User*([Resource])<br>
Represents a Scribd user.<br>
<br>
Use login() or signup() functions to instantiate.<br>
<br>
Resource attributes:<br>
Refer to "Result explanation" section of:<br>
http://www.scribd.com/developers/api?method_name=user.login<br>
<br>
Method resolution order:<br>
User<br>
[Resource]<br>
object<br>
<br>
Methods defined here:<br>
<br>
*all*(self, **kwargs)<br>
Returns a list of all user documents.<br>
<br>
Parameters:<br>
Refer to the "Parameters" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.getList<br>
<br>
Note. Parameters "api_key", "api_sig", "session_key", "my_user_id"<br>
are managed internally by the library.<br>
<br>
Returns:<br>
A list of [Document] objects.<br>
<br>
Refer to "Result explanation" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.getList<br>
for a list of document's initial resource attributes.<br>
<br>
*find*(self, query, **kwargs)<br>
Searches for documents and returns a list of them.<br>
<br>
Parameters:<br>
Refer to the "Parameters" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.search<br>
<br>
Note. Parameters "api_key", "api_sig", "session_key", "my_user_id"<br>
are managed internally by the library. Parameter "num_start" is not<br>
supported. Parameter "num_results" is not supported.<br>
<br>
Additional parameters:<br>
offset<br>
(optional) The offset into the list of documents.<br>
limit<br>
(optional) The number of documents to return<br>
(default 10, max 1000).<br>
<br>
Note on the "scope" parameter:<br>
Only if scope=='user', the returned documents will have the<br>
owner attribute set to this user object. Otherwise it will be<br>
the scribd.api_user which will impact the ability to change<br>
the document's properties. You may set the owner attributes<br>
later if you have can determine the documents owner yourself.<br>
Refer to the [Document] class for operations requiring a proper<br>
owner object.<br>
<br>
Returns:<br>
A list of [Document] objects.<br>
<br>
Refer to "Result explanation" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.search<br>
for a list of document's initial resource attributes.<br>
<br>
*get*(self, doc_id)<br>
Returns a document with the specified id.<br>
<br>
Parameters:<br>
doc_id<br>
(required) Identifier of the document to be returned.<br>
The user has to be the owner of this document.<br>
<br>
Returns:<br>
A [Document] object.<br>
<br>
Refer to "Result explanation" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.getSettings<br>
for a list of document's initial resource attributes.<br>
<br>
*get_autologin_url*(self, next_url='')<br>
Creates and returns an URL that logs the user in when visited and<br>
redirects to the specified URL.<br>
<br>
Parameters:<br>
Refer to the "Parameters" section of:<br>
http://www.scribd.com/developers/api?method_name=user.getAutoSigninUrl<br>
<br>
Note. Parameters "api_key", "api_sig", "session_key", "my_user_id"<br>
are managed internally by the library.<br>
<br>
Returns:<br>
An URL (string).<br>
<br>
*upload*(self, file, name=None, **kwargs)<br>
Uploads a file as a new document and returns the corresponding<br>
[Document] object.<br>
<br>
Parameters:<br>
Refer to the "Parameters" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.upload<br>
<br>
Note. Parameters "api_key", "api_sig", "session_key", "my_user_id"<br>
are managed internally by the library. Parameter "file" is<br>
documented below.<br>
<br>
file<br>
(required) File-alike object to upload. The file is loaded<br>
into memory using the read() method and uploaded.<br>
name<br>
(optional) Name of the file. Either a full path or just the<br>
name. Only the name is used. Does not have to point to an<br>
existing file. If None, the name will be read from the "name"<br>
attribute of the file object (objects created using the open()<br>
built-in function provide this attribute).<br>
<br>
Returns:<br>
A [Document] object.<br>
<br>
Refer to "Result explanation" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.upload<br>
for a list of document's initial resource attributes.<br>
<br>
*upload_from_url*(self, url, **kwargs)<br>
Uploads a file from a remote URL as a new document and returns<br>
the corresponding document object.<br>
<br>
Parameters:<br>
Refer to the "Parameters" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.upload<br>
<br>
Note. Parameters "api_key", "api_sig", "session_key", "my_user_id"<br>
are managed internally by the library. Parameter "file" is not<br>
supported.<br>
<br>
url<br>
(required) A URL of the document to upload.<br>
<br>
Returns:<br>
A [Document] object.<br>
<br>
Refer to "Result explanation" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.upload<br>
for a list of document's initial resource attributes.<br>
<br>
*xall*(self, **kwargs)<br>
Similar to all() method but returns a generator object<br>
iterating over all user documents.<br>
<br>
Parameters:<br>
Refer to the "Parameters" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.getList<br>
<br>
Note. Parameters "api_key", "api_sig", "session_key", "my_user_id"<br>
are managed internally by the library. Parameter "limit" is not<br>
supported.<br>
<br>
Additional parameters:<br>
page_size<br>
(optional) The number of documents acquired by a single API<br>
call. The generator repeats the calls until all documents are<br>
returned. Defaults to 100.<br>
<br>
Returns:<br>
A generator object yielding [Document] objects.<br>
<br>
Refer to "Result explanation" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.getList<br>
for a list of document's initial resource attributes.<br>
<br>
Note. If you're not interested in all documents (currently there<br>
may be max. 1000 of them), just stop iterating the generator object.<br>
<br>
*xfind*(self, query, **kwargs)<br>
Similar to find() method but returns a generator object searching<br>
for documents and iterating over them.<br>
<br>
Parameters:<br>
Refer to the "Parameters" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.search<br>
<br>
Note. Parameters "api_key", "api_sig", "session_key", "my_user_id"<br>
are managed internally by the library. Parameter "num_start" is not<br>
supported. Parameter "num_results" is not supported.<br>
<br>
Additional parameters:<br>
offset<br>
(optional) The offset into the list of documents.<br>
page_size<br>
(optional) The number of documents acquired by a single API<br>
call. The calls are repeated until all documents are returned.<br>
<br>
Returns:<br>
A generator object yielding [Document] objects.<br>
<br>
Refer to "Result explanation" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.search<br>
for a list of document's initial resource attributes.<br>
<br>
Note. If you're not interested in all documents (currently there<br>
may be max. 1000 of them), just stop iterating the generator object.<br>
<br>
----------------------------------------------------------------------<br>
Methods inherited from [Resource]:<br>
<br>
*get_attributes*(self)<br>
Returns a dictionary with the resource attributes. </pre>