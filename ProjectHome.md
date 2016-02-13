## python-scribd ##

Simple yet powerful library for the [Scribd API](http://www.scribd.com/developers/api), allowing to write Python applications or websites that upload, convert, display, search, and control documents in many formats using the [Scribd](http://www.scribd.com) platform.

[Scribd](http://www.scribd.com) is the largest social publishing company in the world — the website where more than 60 million people each month discover and share original writings and documents.

## Documentation ##

First time visitors should read the [Getting started](GettingStarted.md) and [Examples](Examples.md) sections.

Returning developers may want to see the [scribd reference manual](scribd.md).

The changes made to the successive releases are listed in the ChangeLog.

## Quick example ##

```
import scribd

# Pass your Scribd API account keys to the library.
scribd.config('api_key', 'api_secret')

# List all documents of the user that registered the API account.
for document in scribd.api_user.all():
    print 'Title:', document.title
    print 'Description:' document.description

# Log some user in.
user = scribd.login('jsmith', 'password')

# Upload a private document on the user's behalf.
document = user.upload(open('document_to_upload.pdf', 'rb'), access='private')

# Set the document's author.
document.author = 'John Smith'
document.save()
```

## Requirements ##

  * All the library requires is **Python 2.4** or newer.
  * **Python 3.0** isn't supported yet.