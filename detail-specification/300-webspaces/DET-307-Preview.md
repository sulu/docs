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
| update  | `{property: '<property>', data: '<data>'}` | OK for form and the changes for the preview |
| close   | none                                       | none |

## Fallback

To support older Browser or Server which cannot start a Websocket server, the API allows to poll for changes. For this task there is an Preview Controller which has folowing actions:

* render
	* renders the whole HTML Document for the page
	* Example URL: TODO
* update
	* Send update for given page
	* Example Request: TODO 
* changes
	* Returns changes for given page since last request
	* Example Request: TODO
	* Example Response: TODO


## RDFA