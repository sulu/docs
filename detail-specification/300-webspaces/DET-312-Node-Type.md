# Node Type

Node Type indicates that a specifi node is:

* content: has own node content
* internal-link: links to an other node
* external-link: links to a external web-page

## Content
Nothing special. Node has content and an own URL.

## Internal Link
Node has a link to another Node and no own URL. If this Page is mentioned (for example in Navigation) the Title and URL of the linked page will apear.
The Title of this internal link node is only for backend and for UX reasons.

## External Link
Node has a link to an external URL and has no own URL. If this Page is mentioned (for example in Navigation) the Title of the node and the external URL will apear.
The Title of this external link node is important for ankor title and content.

## Storage
The node type is stored as an attribute in the property `i18n:<locale>-nodeType`. And the Template is changed to `internal-link` or `external-link`.
