# DET 307 Preview ([Blog entry](http://www.sulu.io/post/74382940328/live-preview))


The Preview Service is the central component of Preview. It handles:

* Preview rendering (on top of real Websitecontroller)
* Content caching (mixing non persistend changes and phpcr values)
* Starting and stoping preview

After starting preview the serice creates a cache entry with user id and content uuid. there the content structure + changes wil be stored. When the form will call an update, the preview will update the cached structure, render the content partial (only content twig block) and extract the part wich the property has impact (with the rdfa property attribute). The Cache Component is a standard doctrine component, which can be injected.


![Comunication Concept](https://raw2.github.com/sulu-cmf/docs/master/detail-specification/images/Live-Preview.png)

As Communication channel, there are two possibilities:

* Over HTML5 - Websocket
* Fallback

The Changes will be delivered in the folowing format:

```
{
	'<property': {
		property: '<property>',
		content: [
			'<html of ocurence one>',
			'<html of ocurence two>',
			...
		]
	},
	...
}
```
In the Changes return value there is the inner html foreach occurence of, each changed property, in the order it occurs in the whole HTML Document.

## Websocket

Based on the [Ratchet](http://socketo.me/) Open Source Library. To handle the messages, connections, ... there is a PreviewMessageComponent which holds the command structure. 

Example:

```
{
	command: '<command>',
	content: '<uuid>',
	type: '<form|preview>',
	user: '1',
	params: {
		<any>
	}
}
```

The properties command, content and type ar mandatory to find out which window and content for preview it is. The command identifiy which command will be executed.

### Commands

| command | params                                     | answer |
| ------- | ------------------------------------------ | ------ |
| start   | none                                       | OK and a flag if the other part started (repeated after the other part started) |
| update  | `{changes: {'<property>': '<data>'}}` | OK for form and the changes for the preview |
| close   | none                                       | none |

## Fallback

To support older Browser or Server which cannot start a Websocket server, the API allows to poll for changes. For this task there is an Preview Controller which has folowing actions:

* render
	* renders the whole HTML Document for the page
	* URL Schema: `/admin/content/preview/<uuid>`
	* Example Request: `GET /admin/content/preview/0ad908b1-5b26-41ad-a9ac-2fc4371c147d`
* update
	* Send update for given page
	* URL Schema: `POST /admin/content/preview/<uuid>`
	* Example Request: 
	
```
POST /admin/content/preview/0ad908b1-5b26-41ad-a9ac-2fc4371c147d
{
	changes: [
		title: 'Test Title'
	]
}
```
* changes
	* Returns changes for given page since last request
	* URL Schema: `/admin/content/preview/<uuid>.json`
	* Example URL: `GET /admin/content/preview/0ad908b1-5b26-41ad-a9ac-2fc4371c147d.json`
	* Example Response:
	
```
{
	title:{
		property: "title",
		content:[
			"Test Title"
		]
	}
}
```

### Fallback detection

```php
var support = "MozWebSocket" in window ? 'MozWebSocket' : ("WebSocket" in window ? 'WebSocket' : null);
// no support
if (support === null) {
	console.log("Your browser doesn't support Websockets.");
	return false;
}
// let's invite Firefox to the party.
if (window.MozWebSocket) {
	window.WebSocket = window.MozWebSocket;
}
// support exists
return true;
```

* Check if Object WebSocket (HTML5) or MozWebSocket (Mozilla) exists
* if there is no of this goto fallback (Source: [http://www.marcofolio.net/webdesign/working_with_websockets.html](http://www.marcofolio.net/webdesign/working_with_websockets.html))
* if MozWebSocket then set WebSocket = MozWebSocket (Source: [http://eamusic.dartmouth.edu/~osetinsky/HTML5%20Demo%20%20Web%20Socket.html](http://eamusic.dartmouth.edu/~osetinsky/HTML5%20Demo%20%20Web%20Socket.html))



## RDFa ([Wikipedia](http://en.wikipedia.org/wiki/RDFa))

The essence of RDFa is to provide a set of attributes that can be used to carry metadata in an XML language (hence the 'a' in RDFa).

These attributes are:

* about – a URI or CURIE specifying the resource the metadata is about
* rel and rev – specifying a relationship and reverse-relationship with another resource, respectively
* src, href and resource – specifying the partner resource
* property – specifying a property for the content of an element or the partner resource
* content – optional attribute that overrides the content of the element when using the property attribute
* datatype – optional attribute that specifies the datatype of text specified for use with the property attribute
* typeof – optional attribute that specifies the RDF type(s) of the subject or the partner resource (the resource that the metadata is about).

The preview service uses the attribute property to locate the impact of changes in the rendered HTML-Document.


```html
<div vocab="http://schema.org/" typeof="Product">
  <p>Kaufen Sie den 
     <span property="name">Staubsauger XF704</span> 
     jetzt im Sonderangebot! 
     <img property="image" src="acmeXF704.jpg" />
  </p>
</div>
```
