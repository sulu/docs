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

#### Dialog usage with callbacks

Example from: [sulu-cmf/SuluContactBundle@3d0d4e2](https://github.com/sulu-cmf/SuluContactBundle/commit/3d0d4e21829323bb4b33494e8681ad97dac3ef3b)

```
 // show dialog
this.sandbox.emit('sulu.dialog.confirmation.show', {
    content: {
        title: "Be careful!",
        content: "<p>The operation you are about to do will delete data.<br/>This is not undoable!</p><p>Please think about it and accept or decline.</p>"
    },
    footer: {
        buttonCancelText: "Don't do it",
        buttonSubmitText: "Do it, I understand"
    },
    callback: {
        submit: function() {
            this.sandbox.emit('husky.dialog.hide');
            if (!!callbackFunction) {
                callbackFunction(true);
            }
        }.bind(this),
        cancel: function() {
            this.sandbox.emit('husky.dialog.hide');
            if (!!callbackFunction) {
                callbackFunction(false);
            }
        }.bind(this)
    }
});
```

