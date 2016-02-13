<pre>
class *Document*([Resource])<br>
Represents a Scribd document.<br>
<br>
Use methods of the [User] objects to instantiate.<br>
<br>
Attributes:<br>
owner<br>
A [User] object owning the document. This always is a valid<br>
object but may not be the true owner of the document if it could<br>
not be determined. This may be the case if the document was obtained<br>
from find() or xfind() function/method. In the worst case, the owner<br>
will be set to the scribd.api_user object which is the default user<br>
associated with the current API account.<br>
<br>
You may set this attribute if you can determine the true owner<br>
yourself.<br>
<br>
Refer to the object methods documentation to learn which ones<br>
require a true owner to be set.<br>
<br>
Resource attributes:<br>
The initial set of the attributes depend on how this object<br>
was obtained.<br>
<br>
Refer to "Result explanation" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.getList<br>
if the object was obtained by the [User] object's all() or<br>
xall() methods.<br>
<br>
Refer to "Result explanation" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.search<br>
if the object was obtained by find() or xfind() (either global<br>
functions or [User] object's methods).<br>
<br>
Refer to "Result explanation" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.upload<br>
if the object was obtained by one of the [User] object's<br>
uploads methods.<br>
<br>
Refer to "Result explanation" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.getSettings<br>
if the object was obtained by the [User] object's get() method.<br>
<br>
If the owner attribute points to a true owner of the document,<br>
the load() method may be used to obtain a full set of resource<br>
attributes. For more information refer to the load() method<br>
documentation.<br>
<br>
Method resolution order:<br>
Document<br>
[Resource]<br>
object<br>
<br>
Methods defined here:<br>
<br>
*delete*(self)<br>
Deletes the document from Scribd platform.<br>
<br>
Requires the document owner to be the user that uploaded this<br>
document.<br>
<br>
*get_access_list*(self)<br>
This method can be used for tracking and verification purposes. It returns<br>
a list of virtual users currently authorized to view this secure document.<br>
<br>
Returns:<br>
A list of [VirtualUser] objects.<br>
<br>
This method is part of iPaper Secure. For more info about iPaper Secure visit:<br>
http://www.scribd.com/publisher/ipaper_secure<br>
<br>
*get_conversion_status*(self)<br>
Obtains and returns the document current conversion status.<br>
<br>
Returns:<br>
A string. Refer to the "Result explanation" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.getConversionStatus<br>
<br>
Requires the document owner to be the user that uploaded this<br>
document.<br>
<br>
*get_download_url*(self, doc_type='original')<br>
Returns a link that can be used to download a static version of the<br>
document.<br>
<br>
Parameters:<br>
Refer to the "Parameters" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.getDownloadUrl<br>
<br>
Note. Parameters "api_key", "api_sig", "session_key", "my_user_id",<br>
"doc_id" are managed internally by the library.<br>
<br>
Returns:<br>
An URL (string).<br>
<br>
*get_scribd_url*(self)<br>
Returns a link to the document's page on scribd.com.<br>
<br>
Works for private documents too by adding the secret<br>
password to the link. May call the load() method to<br>
obtain the secret password.<br>
<br>
*load*(self)<br>
Retrieves the detailed meta-data for this document and updates<br>
object's resource attributes.<br>
<br>
Refer to the "Result explanation" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.getSettings<br>
for the names and descriptions of the resource attributes.<br>
<br>
Requires the document owner to be the user that uploaded this<br>
document.<br>
<br>
*replace*(self, file, name=None, **kwargs)<br>
Uploads a new file in place of the current document. All<br>
resource attributes including doc_id remain intact.<br>
<br>
Parameters:<br>
Refer to the [User].upload() method.<br>
<br>
Note. Parameter "rev_id" is managed internally by the library.<br>
<br>
Requires the document owner to be the user that uploaded this<br>
document.<br>
<br>
*replace_from_url*(self, url, **kwargs)<br>
Uploads a new file from a remote URL in place of the current<br>
document. All resource attributes including doc_id remain intact.<br>
<br>
Parameters:<br>
Refer to the [User].upload_from_url() method.<br>
<br>
Note. Parameter "rev_id" is managed internally by the library.<br>
<br>
Requires the document owner to be the user that uploaded this<br>
document.<br>
<br>
*save*(self)<br>
Saves the changed object's resource attributes.<br>
<br>
Has to be called after a resource attribute has been altered<br>
to make the change permanent.<br>
<br>
Refer to the "Parameters" section of:<br>
http://www.scribd.com/developers/api?method_name=docs.changeSettings<br>
for the names and descriptions of the resource attributes<br>
that are saved by this call.<br>
<br>
Requires the document owner to be the user that uploaded this<br>
document.<br>
<br>
*set_access*(self, user, allowed)<br>
This method allows you to disable a virtual user's access to this secure<br>
document, or to re-enable it after a previous call. It is not necessary nor<br>
possible to grant initial access to a document using this call - that is done<br>
through the embed code.<br>
<br>
Parameters:<br>
user<br>
Virtual user's name or [VirtualUser] object.<br>
allowed<br>
If False, disables access. If True, re-enables access.<br>
<br>
This method is part of iPaper Secure. For more info about iPaper Secure visit:<br>
http://www.scribd.com/publisher/ipaper_secure<br>
<br>
----------------------------------------------------------------------<br>
Methods inherited from [Resource]:<br>
<br>
*get_attributes*(self)<br>
Returns a dictionary with the resource attributes. </pre>