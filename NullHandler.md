<pre>
class *NullHandler*(logging.Handler)<br>
Empty logging handler used to prevent a warning if the application<br>
doesn't use the logging module.<br>
<br>
Method resolution order:<br>
NullHandler<br>
logging.Handler<br>
logging.Filterer<br>
<br>
Methods defined here:<br>
<br>
*emit*(self, record)<br>
<br>
----------------------------------------------------------------------<br>
Methods inherited from logging.Handler:<br>
<br>
*__init__*(self, level=0)<br>
Initializes the instance - basically setting the formatter to None<br>
and the filter list to empty.<br>
<br>
*acquire*(self)<br>
Acquire the I/O thread lock.<br>
<br>
*close*(self)<br>
Tidy up any resources used by the handler.<br>
<br>
This version does removes the handler from an internal list<br>
of handlers which is closed when shutdown() is called. Subclasses<br>
should ensure that this gets called from overridden close()<br>
methods.<br>
<br>
*createLock*(self)<br>
Acquire a thread lock for serializing access to the underlying I/O.<br>
<br>
*flush*(self)<br>
Ensure all logging output has been flushed.<br>
<br>
This version does nothing and is intended to be implemented by<br>
subclasses.<br>
<br>
*format*(self, record)<br>
Format the specified record.<br>
<br>
If a formatter is set, use it. Otherwise, use the default formatter<br>
for the module.<br>
<br>
*handle*(self, record)<br>
Conditionally emit the specified logging record.<br>
<br>
Emission depends on filters which may have been added to the handler.<br>
Wrap the actual emission of the record with acquisition/release of<br>
the I/O thread lock. Returns whether the filter passed the record for<br>
emission.<br>
<br>
*handleError*(self, record)<br>
Handle errors which occur during an emit() call.<br>
<br>
This method should be called from handlers when an exception is<br>
encountered during an emit() call. If raiseExceptions is false,<br>
exceptions get silently ignored. This is what is mostly wanted<br>
for a logging system - most users will not care about errors in<br>
the logging system, they are more interested in application errors.<br>
You could, however, replace this with a custom handler if you wish.<br>
The record which was being processed is passed in to this method.<br>
<br>
*release*(self)<br>
Release the I/O thread lock.<br>
<br>
*setFormatter*(self, fmt)<br>
Set the formatter for this handler.<br>
<br>
*setLevel*(self, level)<br>
Set the logging level of this handler.<br>
<br>
----------------------------------------------------------------------<br>
Methods inherited from logging.Filterer:<br>
<br>
*addFilter*(self, filter)<br>
Add the specified filter to this handler.<br>
<br>
*filter*(self, record)<br>
Determine if a record is loggable by consulting all the filters.<br>
<br>
The default is to allow the record to be logged; any filter can veto<br>
this and the record is then dropped. Returns a zero value if a record<br>
is to be dropped, else non-zero.<br>
<br>
*removeFilter*(self, filter)<br>
Remove the specified filter from this handler. </pre>