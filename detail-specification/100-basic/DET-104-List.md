# Lists


##Editable Lists

Lists can be editable with following restrictions:
- when the users edits a field the row is saved when the row loses the focus
- local validation is only displayed when an error occurs
- validation can be locally (e.g. for format related issues) and will display error but no success
- validation can be in interaction with the server (e.g. uniqueness) will display error or success 
- the progress of save action will be displayed with a loading icon at the end of the changed row
