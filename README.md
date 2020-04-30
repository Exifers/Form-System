# Abstract
There are plenty of design systems accross the web. While they are quite similar as they provide usually the same types
of components, they are also quite different because each component has its own API when it comes to dealing with state
managment in javascript, whether you use React, Vue, Angular or another javascript framework. It is especially true with
form components which highly rely on state managment.

Also, choosing a design system can be cumbersome sometimes because you need to browse all of its components and make sure
there is everything you need for your project.

This document aims at :
- providing a list of most commonly used components in design systems so that it can act as a guideline for design system creators
- define an API for each component so that design systems following this API could be switched from one to another without
touching too much code

# Form inputs components
## Common API

| prop               | type                                                               | default value | description                |
| ------------------ | ------------------------------------------------------------------ | ------------- | -------------------------- |
| validatationStatus | 'success' \| 'warning' \| 'error' \| 'loading' \| 'none' \| 'auto' | 'auto'        | Validate status appearance |
| successMessages    | [String]                                                           | []            | List of success messages   |
| warningMessages    | [String]                                                           | []            | List of warning messages   |
| errorMessages      | [String]                                                           | []            | List of error messages     |


## text
### text input
A canonical component to input textual data.
```jsx=
<input/>
<input type='text'/>
```
Props are populated into the internal ```<input/>``` element.

Returned value : a string representing the content of the text input.

### password input
A semantic variant of the text input.
```jsx=
<input type='password'/>
```
Additional features :
 - visibility toggle

| prop             | type    | default value | description                        |
| ---------------- | ------- | ------------- | ---------------------------------- |
| visibilityToggle | Boolean | true          | Shows a toggle visibility button   |

Returned value : a string representing the content of the password input.

### address input
A separable component, semantic variant of the text input.
```jsx=
<input type='address'/>
```
Additional features :
 - international

| prop      | type    | default value | description              |
| --------- | ------- | ------------- | ------------------------ |
| separated | Boolean | true          | Use multiple form inputs |

Returned value :
```javascript=
{
  addressLine1: String,
  addressLine2: String,
  city: String,
  stateOrProvince: String,
  country: <country code>,
  zipOrPostalCode: String
}
```
based on [this article](https://ux.shopify.com/designing-address-forms-for-everyone-everywhere-f481f6baf513).

### url input
A semantic variant of the text input.
```jsx=
<input type='url'/>
```

Returned value : a string representing the content of the url input.

### email input
A separable component, semantic variant of the text input.
```jsx=
<input type='email'/>
```

| prop      | type    | default value | description                                 |
| --------- | ------- | ------------- | ------------------------------------------- |
| separated | Boolean | true          | Use two text inputs (local part and domain) |

Returned value : a string representing the content of the email input.

### phone number
A semantic variant of the text input.
```jsx=
<input type='phone'/>
```

Additional features : 
  - international

| prop      | type                      | default value | description                                   |
| --------- | ------------------------- | ------------- | --------------------------------------------- |
| countries | [<country_code>] \| 'all' | 'all'         | Countries for which auto format is supported. |

Returned value : a string representing the content of the email input.

### text area
A resizable text input.
```jsx=
<textarea/>
```

Returned value : a string representing the content of the text area.

## boolean
### checkbox
### switch
## enum
### select
Possible features :
 - search
 - items icons
 - groups
### treeselect
Possible features :
  - search
### cascader
Possible features :
  - search
### radio buttons
## Set(enum)
### multiselect
Possible features :
 - search
 - icons
 - groups
### multitreeselect
Possible features :
 - search
## number
- comparable
### numeric input
#### Possible semantics
 - percent
 - money
 - temperature
 - any other unit
### slider
### rating
## color
- separable
### color picker
Possible features :
- palette
- different color formats
- list of last chosen colors
## day-month-year (alias 'date')
- separable
- comparable
### datepicker
## seconds-minutes-hour-day-month-year (alias 'datetime')
- separable
- comparable
### datetimepicker
## seconds-minutes-hour (alias 'time')
- separable
- comparable
### timepicker
## week-month-year (alias 'weekdate')
- separable
- comparable
### weekdatepicker
## month-year (alias 'monthdate')
- separable
- comparable
### monthdatepicker
## year
- comparable
### yearpicker
## day
### daypicker
## week
### weekpicker
## month
### monthpicker
## duration
- separable
- comparable
### durationpicker
## file
### filepicker
Possible features :
- filedrop
- uploaded image preview
