##DET-003 Frontend Architecture

####General
The frontend architecture is built on [AuraJS](http://aurajs.com/), [Backbone](http://backbonejs.org/), [jQuery](http://jquery.com/) and our JS-Framework [husky](https://github.com/massiveart/husky). Additionally we have included the [Backbone relational extension](http://backbonerelational.org/). Aura abstracts all these framework, and makes it easy to exchange some framework with different ones (at least when we don't couple the API too strong).

####Components
#####Aura extension
Every bundle defines an extension called `main.js`, which is located in the bundle's js-root-directory. It adds the aura source for this component, defines all the routes available in this bundle and where the route heads to. 

#####Models
The component can define some bundle-global models in the js-root's `models`-folder, if several sub components need the same model.
If the model is only required by one sub component, the model should be located inside an own `models`-folder in the sub component.

These models extend the `Backbone.RelationalModel`-object instead of the `Backbone.Model`-object, as our requirements need the ability to save relationships between objects.

#####Aura components
A bundle, at least the ones which want to participate on the frontend side of the application, defines some Aura-components in its `components`-Folder in the js-root-directory. 

These components consist of a `main.js`-file, which is responsible of handling all the routings and events related to the model. The idea is that only this component knows about its models, so that we have a nice coupling.

Usually each components also consists of several sub-components, which are located in the `components`-folder of the component. These sub-components are responsible for displaying the data and send the edited data back to it's parent component. All these communication is handled via AuraJS-events.

####Sample flow
![Frontend Architecture diagram](https://raw.github.com/massiveart/sulu-docs/master/detail-specification/images/diagrams/frontend_architecture.png)

This diagram show the sample flow of one of our bundles. In this case we have an `ExampleBundle`, which is responsible for an `Entity`. The following list is describing the information flow for displaying an already existing item, edit it, and save the changes in the database.

1. a `sulu.router.navigate` event with the additional data for displaying the form and the id of the `Entity` is emitted
1. the `Backbone.Router` routes this event to a function which starts the aura component `Entities`, more precisely to its `main.js`-file, with the information that it should display a form and load the `Entity` with the id 1.
1. the aura component, which requires the `Entity`-model, fetches the data for the id 1
1. the aura component starts its sub component form with the data from the `Entity` attached
1. the user can edit the data, and click the save button, which emits  a `sulu.example.save`-event
1. the parent aura component listens on the `sulu.example.save`-event, fills the `Entity` with the new data, and tells the `Entity` to save itself
1. the entity sends the correct request to the REST-service, which updates the data in the database
