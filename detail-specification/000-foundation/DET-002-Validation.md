# DET-002 Validation

For Validation of Form's we have researched two possible cadidate:

* [jQuery Validation Plugin](http://jqueryvalidation.org/)
* [ParsleyJS](http://parsleyjs.org/)

## Requirements

1. Standard validation methods (mail, date, ...)
1. Easy adding own methods
1. Localization of dates, number, ...

|               | 1. | 2. | 3. |
| ------------- |:--:|:--:|:--:|
| jQuery Val.   | Y  | Y  | N  |
| ParsleyJS     | Y  | Y  | N  |

## Result

Both Candidates dont implement all requirements. But we have decided to use ParsleyJS and add the localization.

Parsley have folowing opportunities:

* Initialization without js code
* Strong validation methods like: greater than an other field
* It uses data attributes, isolation of style (not classes) and code
* Easy validation method extensions
* Modern

## ParsleyJS Example

The Server can initialize the Validation with HTML data Attributes.

  <form data-validate="parsley">
      <input type="text" name="email" data-type="email" />
  </form>

* Define foreach field a data-type attribute
* Define form data-validate="parsley", this will initiate the validation automatically


