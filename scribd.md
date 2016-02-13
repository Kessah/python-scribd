<pre>
*NAME*<br>
scribd - Scribd client library.<br>
<br>
*FILE*<br>
__init__.py<br>
<br>
*DESCRIPTION*<br>
This is a simple yet powerful library for the Scribd API, allowing to write<br>
Python applications or websites that upload, convert, display, search, and<br>
control documents in many formats using the Scribd platform.<br>
<br>
For more information on the Scribd platform, visit:<br>
http://www.scribd.com/about<br>
<br>
The underlying RESTful API documentation can be found at:<br>
http://www.scribd.com/developers<br>
<br>
Copyright (c) 2009, Arkadiusz Wahlig <arkadiusz.wahlig@gmail.com><br>
<br>
Distributed under the new BSD License, see the<br>
accompanying LICENSE file for more information.<br>
<br>
*PACKAGE CONTENTS*<br>
multipart<br>
xmlparse<br>
<br>
*CLASSES*<br>
object<br>
[Resource]<br>
[Document]<br>
[User]<br>
[VirtualUser]<br>
[Error](exceptions.Exception)<br>
[MalformedResponseError]<br>
[NotReadyError]<br>
[ResponseError]<br>
<br>
*FUNCTIONS*<br>
*config*(key, secret)<br>
Configures the API key and secret. These values have to be<br>
configured before any operation involving API calls can be performed.<br>
<br>
Parameters:<br>
key<br>
The API key assigned to your Scribd user account.<br>
secret<br>
The API secret assigned to your Scribd user account.<br>
<br>
API key and secret values are obtained by signing up for a Scribd<br>
account and registering it as an API account. The website will in<br>
turn provide you with both values.<br>
<br>
*find*(query, **kwargs)<br>
Searches for public documents and returns a list of them.<br>
<br>
Parameters:<br>
Refer to [User].find() method.<br>
<br>
Returns:<br>
A list of [Document] objects.<br>
<br>
This function searches for public documents by default.<br>
<br>
The returned document have the owner attribute set to the<br>
scribd.api_user object.<br>
<br>
*login*(username, password)<br>
Logs the given Scribd user in and returns the corresponding [User] object.<br>
<br>
Parameters:<br>
username<br>
Name of the user.<br>
password<br>
The user's password.<br>
<br>
Returns:<br>
A [User] object.<br>
<br>
*signup*(username, password, email, name=None)<br>
Creates a new Scribd user and returns the corresponding [User] object.<br>
The user is already logged in.<br>
<br>
Parameters:<br>
username<br>
Name of the new user.<br>
password<br>
Password of the new user.<br>
email<br>
E-mail address of the user.<br>
<br>
Returns:<br>
A [User] object.<br>
<br>
*update*(docs, **fields)<br>
A faster way to set the same attribute of many documents.<br>
<br>
Parameters:<br>
docs<br>
A sequence of [Document] objects.<br>
keyword arguments<br>
Document attributes to set.<br>
<br>
Example:<br>
Instead of:<br>
<br>
for doc in docs:<br>
doc.some_attribute_1 = some_value_1<br>
doc.some_attribute_2 = some_value_2<br>
doc.save()<br>
use:<br>
<br>
update(docs, some_attribute_1=some_value_1,<br>
some_attribute_2=some_value_2)<br>
<br>
All documents must have the same owner. The operation is faster because<br>
it requires only one API call.<br>
<br>
*xfind*(query, **kwargs)<br>
Similar to find() function but returns a generator object<br>
searching for documents and iterating over them.<br>
<br>
Parameters:<br>
Refer to [User].xfind() method.<br>
<br>
Returns:<br>
A generator object yielding [Document] objects.<br>
<br>
This function searches for public documents by default.<br>
<br>
The returned document have the owner attribute set to the<br>
scribd.api_user object.<br>
<br>
*DATA*<br>
*api_user* = <scribd.[User] 'api_user'><br>
<br>
*VERSION*<br>
1.1.0<br>
</pre>