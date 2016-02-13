<pre>
class *VirtualUser*([User])<br>
Provides an easy way to implement virtual users within the current<br>
Scribd API account.<br>
<br>
This is useful if Scribd is used as a backend for a platform with its<br>
own user authentication system.<br>
<br>
Virtual users are also used to control access to the embedded documents<br>
when using iPaper Secure. For more info about iPaper Secure visit:<br>
http://www.scribd.com/publisher/ipaper_secure<br>
<br>
Virtual users are created just by instantiating this class passing the<br>
name of the virtual user to the constructor. This will most probably<br>
be the name used by your own authentication system.<br>
<br>
Because this is a subclass of the [User] class, the virtual users provide<br>
the same set of operations (except get_autologin_url()) as normal users.<br>
<br>
Resource attributes:<br>
None.<br>
<br>
Method resolution order:<br>
VirtualUser<br>
[User]<br>
[Resource]<br>
object<br>
<br>
Methods defined here:<br>
<br>
*__init__*(self, my_user_id)<br>
Instantiates a new object.<br>
<br>
Parameters:<br>
my_user_id<br>
Name of the virtual user. Every time an object is created<br>
with the same name, it will refer to the same virtual user.<br>
<br>
*get_access_list*(self)<br>
This method can be used for tracking and verification purposes.<br>
It returns a list of the secure documents that this virtual user is<br>
currently allowed to access.<br>
<br>
Note that calling [Document].set_access() will not insert a document<br>
into this list (though it can remove one) - that can only be done with<br>
the user viewing an active embed code.<br>
<br>
Returns:<br>
A list of [Document] objects.<br>
<br>
This method is part of iPaper Secure. For more info about iPaper Secure visit:<br>
http://www.scribd.com/publisher/ipaper_secure<br>
<br>
*get_autologin_url*(self, next_path='')<br>
This method is not supported by virtual users.<br>
<br>
*set_access*(self, allowed)<br>
This method allows you to disable a user's access to secure documents,<br>
or to re-enable it after a previous call. It is not necessary to grant<br>
initial access to documents - that is done through the embed code.<br>
<br>
Parameters:<br>
allowed<br>
If False, disables access. If True, re-enables access.<br>
<br>
This method is part of iPaper Secure. For more info about iPaper Secure visit:<br>
http://www.scribd.com/publisher/ipaper_secure<br>
<br>
----------------------------------------------------------------------<br>
Methods inherited from [User]:<br>
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