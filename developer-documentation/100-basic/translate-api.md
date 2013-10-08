####Programming API

Two posibilities:

1. Template extension
2. Sandbox Function

#####Template extension

Add each Template you need to the templates array of your component and use it in your render method.

!Caution! : the extension add .html to the name of template.

* main.js:
```
return {
  templates: ['/contact/template/account/form']
  
  ...
  
  render: function() {
    this.$el.html(this.renderTemplate('/contact/template/account/form', { ... }));
    
    ...
  }
};
```


In the template use the translate function. This function will be added to the context automatically.

* account.form.html.twig:

```
...
<label class="required"><%=translate('contact.accounts.name')%></label>
...                
```

#####Sandbox Function

```
this.sandbox.translate('public.delete')
```

If the translation for the key is not found in the messages, the key will be displayed.

####Basic

Actual Keys find [here ...](https://github.com/massiveart/sulu-docs/blob/master/detail-specification/100-basic/DET-101-Translation-Keys.md)

Add Messages to Husky at start:

```
app = new Husky({
    debug: {
        enable: true
    },
    culture: {
        name: language,
        messages: messages
    }
});
```
