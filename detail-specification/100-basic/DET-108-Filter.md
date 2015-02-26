# Filters
The basic idea behind the filters is that one can filter a collection of an entity according to the userdefined filter criteria. This filter logic can be applied to all lists (products, ...) as well as special distribuition lists in the CRM bundle containing contacts or accounts.

## The FilterController
This controller should be a typical rest controller and provide an api to create, update and delete filters as well as an api to get a single or a list of filters (by the entity name). It is an abstract class and should be used by the concrete filter controlleres e.g. a ContactFilterController. A filter controller will process the request and delegate the work to the filter manager. Each FilterController instance should provide the an array of FieldDescriptors which is used to display the list of entities (filterListFieldDescriptors) and another array of FieldDescriptors which are used to define/restrict the possible filterable columns and relations.

### The Filter entity
The filter entity consists of three fields:
- id
- name (of the filter)
- entityName (which should be the class name of the doctrine entity where this filter can be applied to ```Contact::class```)

A filter entity can be related to multiple filter criterias.

__When the filter should be multilingual a translation for the name would be needed!__

### FilterCriteria
The filter criteria entity consists of following fields:
- id
- fieldName (which should match a field descriptor name)
- operand (=, >=, <= !=, ...)
- value (the value the filter criteria should match / not match / ...)
- filterId (the filter this criteria belongs to)

__For now (first version) all criteria will be conected with AND!__

## FilterManager
This manager processes the requests from the filter controller and provides the result of a filter used on a collection of entities. Therefor it uses the ListBuilder like in many cgetActions and will append the conditions to build the query according to the given FilterCriteria entities (QueryBuilder).
