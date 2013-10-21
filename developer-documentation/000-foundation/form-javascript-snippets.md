# Form Javascript Snippets #

#### Submit form via enter key####


```
this.sandbox.dom.keypress(this.formId, function(event) {
    if (event.which === 13) {
        event.preventDefault();
        this.save();
    }
}.bind(this));
```
