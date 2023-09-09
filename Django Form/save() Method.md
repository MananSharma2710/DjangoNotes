## save() Method

**`save (commit-False/True)` Method** 
* This method creates and saves a database object from the data bound to the form.
* A subclass of ModelForm can accept an existing model instance as the keyword argument instance, if this is supplied, *save()* will update that instance.
* If it's not supplied, *save()* will create a new instance of the specified model. If the form hasn't been validated, calling *save()* will do so by checking *form.errors*. 

**Syntax**: 
`save (commit-False/True)`

* If *commit-False*, then it will return an object that hasn't yet been saved to the database.
* This is useful if we want to do custom processing on the object before saving it, or if we want to use one of the specialized model saving options.
* If our model has a many-to-many relation and we specify *commit-False* when we save a form, Django cannot immediately save the form data for the many-to-many relation.
* This is because it isn't possible to save many-to-many data for an instance until the instance exists in the database.