# Ionic Form w/ Validation
- two-way data binding
- change gtracking
- validation
- error handling
- Finally, users are able to sending data through the API

## Angular Reactive Forms vs Template Driven Forms
- These two belong to the @angular/forms library 
- The big differences are programming style and technique, and philosophy.
- While Reactive forms are synchronous, Template-driven forms are asynchronous.

### Angular Reactive Forms
- Explicit data management flowing between non-UI data models( typically retrieved from a server) and a UI-orinted form model that keeps the states and values of HTML conrtorls on the app screen.
- Avoid directives like ngModel, NgForm, required and such
- One of the advantages of working directly with form control objects is that value and validity updates are always synchronous and under your control. You won’t find the timing issues that sometimes affect a template-driven form

### Angular Template driven  forms
- By using such ngModel directives, we are able to control forms( such as input or select ) and bind them to data model properties in the component.
- Angular handles pushing and pulling data values for us through the ngModel directive and update the mutable data model according to user changes as they happen.
- By specifying directives such as ngModel, required, and minlength to bind our models, values, validations and more,we are letting the template do all the work on the background.
- Less code in the component class


## Angular forms basics: FormGroup, FormControl and FormBuilder

- FormControl: it tracks the value and validity status of an angular form control. It matches to a HTML form control such as an input or a selector.
- FormControl for the name property which should not be empty.

```
// form.ts
this.name = new FormControl('Dayana', Validators.required)

// form.html
<ion-input type="text" formControlName="name"></ion-input>

```

- FormGroup: it tracks the value and validity state of a FormBuilder instance group. It aggregates the values of each child FormControl into one object, with each form control name as the key. It calculates its status by reducing the statuses of its children. For example, if one of the controls in a group is invalid, the entire group becomes invalid. For example:

```
// form.ts
this.user = new FormGroup({
   name: new FormControl('Dayana', Validators.required),
   country: new FormControl('Uruguay', Validators.required)
});
```

- FormBuilder: is a helper class that creates FormGroup, FormControl and FormArray instances for us. It basically reduces the repetition and clutter by handling details of form control creation for you.

```
this.validations_form = this.formBuilder.group({
	name: new FormControl('', Validators.required),
	email: new FormControl('', Validators.compose([
		Validators.required,
		Validators.pattern('^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+.[a-zA-Z0-9-.]+$')
	]))
});
```
- All of them should be imported from the @angular/forms module.

```
import { Validators, FormBuilder, FormGroup, FormControl } from '@angular/forms';
```
