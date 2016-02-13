## Terminology ##

Before we get started, lets clear out some terms:

  * python-scribd

> This is the full name of the library. It is used if referring to it in a broader context. An example is this Google Code project's name or the name of the download files containing the library.

  * scribd

> This is the name of the Python package provided by the library. It is the name used while importing and referring to the library from within Python scripts. Always written using lowercase letters only.

  * Scribd

> This is the name of the actual documents hosting service, i.e. the scribd.com website. Always written with capital letter "S".

## Installation ##

The library is distributed with the standard Python _distutils_ script (setup.py). After downloading and decompressing, open a system administrator terminal and issue the following command to perform the installation:

```
python setup.py install
```

## Getting started ##

The first thing to do before writing any code is to go to http://scribd.com and sign up for a user account.

The user account has to be enabled for API access. This is done using the form on http://www.scribd.com/developers/signup_api. You'll have to provide some basic description of your project. No approval is needed, the registration is completed immediately.

The API account is identified by an **API key**. This key has to be passed to the library before using it. You will find it on your profile page on scribd.com after enabling the API access.

The page also gives you an **API secret** key. This is used to digitally sign all requests sent to the API server to prevent the middle-man attacks. The signing is optional for the API but the library enforces it (for security reasons) so you'll need this key too.

## Initialization ##

The preferred way to import the [scribd](scribd.md) library is:

```
import scribd
```

other import forms are also supported but discouraged.

As said before, the library needs the **API key** and **API secret** before it can be used. The preferred way to pass them to it is:

```
scribd.config('your_api_key', 'your_api_secret')
```

This function sets the [scribd](scribd.md) module global variables, alternatively you can do it directly:

```
scribd.api_key = 'your_api_key'
scribd.api_secret = 'your_api_secret'
```

At this point you can start using the library freely, create documents, search for them, change their attributes, etc.

## User hierarchy ##

Every Scribd user is represented in the library by a [User](User.md) object. By passing your **API key** to the library, you've effectively let it log into your Scribd user account. The corresponding [User](User.md) object can be found in the

```
scribd.api_user
```

variable. You can use it now to access your documents or upload new ones. Refer to the [User](User.md) object documentation for more information.

The API also lets you log as a different user while still using your API account to access the Scribd API. This is done using the `login()` function from the [scribd](scribd.md) module. The function returns the corresponding [User](User.md) object.

```
jsmith_user = scribd.login('jsmith', 'password')
```

You can also log yourself in. This may seem redundant but overcomes one limitation of the `api_user` object. Unlike other [User](User.md) objects, it doesn't support resource attributes like `name` or `username`. This may be important to you or not, depending on what you want to accomplish.

A small digression on the **resource attributes** as it may be puzzling what they are. Basically, they are just like any other object attributes. The special thing about them is that they are defined by the responses of the Scribd API host, the library doesn't know their names or meaning (with few exceptions). This is exactly the reason why `api_user` has no resource attributes - it isn't created by an API call and there is no response to define them.

Finally your can sign up for a new user account using the `signup()` function from the [scribd](scribd.md) module.

```
johndoe_user = scribd.signup('johndoe', 'password', 'johndoe@example.com')
```

## Virtual users ##

Another users related feature are the virtual users. This mechanism lets you create "phantom" users within your API account. In other words, it lets you easily divide documents stored on your API account between virtual users. This is intended to make it easy for web applications with their own user authentication systems to integrate with Scribd's user model.

To create a virtual user, either for the first time or later, you instantiate the VirtualUser class:

```
phantom = scribd.VirtualUser('phantom')
```

In this example, `'phantom'` is the name of your choosing for the virtual user. VirtualUser objects derive from [User](User.md) objects and as such, provide all their documents management functionality.

Virtual users don't support resource attributes, similarly to the `api_user` object.

## Documents ##

If you're read the [User](User.md) object documentation, you know that it provides you with various ways for searching, listing or uploading of documents. For example the `upload()` method is used to put a new document on the Scribd platform. Here's how it could be used:

```
>>> document = user.upload(open('some_document.pdf', 'rb'))
```

In this example, the `user` is the [User](User.md) or [VirtualUser](VirtualUser.md) object as described in previous chapter. We pass an opened file object to the `upload()` method. The method will read the file and send it to the server along with the filename read from the file object's `name` attribute. There are additional arguments not mentioned here, for more information refer to the [User](User.md).upload() method documentation. The documents may also be uploaded from an URL, in this case the [User](User.md).upload\_from\_url() method should be used.

The method returns a [Document](Document.md) object which represents a document on the Scribd platform.

It is good to know now what resource attributes are as a document may provide a different set depending on how it was obtained. Freshly uploaded document have almost no attributes. This is intentional as we want to set them first:

```
>>> from datetime import date
>>> document.author = 'John Smith'
>>> document.when_published = date.today().isoformat() # Returns date in 'YYYY-MM-DD' format.
>>> document.license = 'pd'
```

We've used the `datetime` module to get today's date in ISO format required for the `when_published` attribute.

One very important step remains before we're done setting the attributes:

```
>>> document.save()
```

This sends the values to the Scribd API host.

Now lets do a little test and see if the values were really saved. First we'll discard the current document object:

```
>>> del document
```

Now we're going to reacquire the document object. In this example we're going to do it by accessing the list of all already uploaded documents. Assuming that we're using a fresh user account, the list will contain only one document, the one we've uploaded before.

```
>>> all_documents = user.all()
>>> document = all_documents[0]
```

The second line assigns the only [Document](Document.md) object to the `document` variable.

In normal circumstances, the `all()` call may return a lot of documents. To save network bandwidth, the returned document objects provide only the basic resource attributes by default. The three attributes we've set before are not among them. We have to explicitly tell the object to set them up, using the `load()` method:

```
>>> document.load()
```

Now we should be able to read back our attributes:

```
>>> document.author
'John Smith'
>>> document.when_published
'2009-06-06'
```

One thing to note here that happens behind the scenes is that the [Document](Document.md) objects perform all operations through their owner - a [User](User.md) object stored in the document's `owner` attribute.

Determining a true document owner may not always be possible, for example if the document objects are created by searching in the public documents library. In such case, a fallback user is used, the already known `api_user` object.

The implication is that if the owner object isn't a true owner of the document, operations like `load()` or `save()` cannot be performed and fail.

In the above example, we've used two ways of obtaining the [Document](Document.md) objects (`upload()` and `all()` methods), both of which are able to clearly determine the owner (it is the user object the methods were called on). Therefore it was safe to call `load()`and `save()` on these objects.