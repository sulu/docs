##![basic](https://raw.github.com/massiveart/sulu-docs/master/system-requirements/images/basic.png)DET-101 Translations

####Database Diagram

![Translations database diagram](https://raw.github.com/massiveart/sulu-docs/master/detail-specification/images/db/translate.png)

####Description

tr_codes contains all the translation keys, which are available in our system. A package is a collection of consolidated keys. These packages have multiple catalogues, one for each language. The catalogues hold all the translations from the package-codes in the tr_translations-table. The location is an optional field for each code, by which the codes can be grouped into seperate sections.

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
