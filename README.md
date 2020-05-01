# Building design system agnostic user interfaces with a design system API specification

# Abstract
There are plenty of design systems accross the web. While they are quite similar as they provide usually the same types of components, they are also quite different because each component has its own API when it comes to dealing with state managment in javascript. It is especially true with form components which highly rely on state managment.

Also, choosing a design system at the beginning of a project can be cumbersome sometimes because we need to browse all of its components and make sure there is everything we need for the project.

We need a way to standardize design systems so that we can easily know if one would fit our needs or not when beginning a project. We also need a common state management API for each component so that we don't have to bother with the variaty of similar but not identical property names that each component exposes in a given design system.

In this document, we provide essentially : 
- A listing of all common design system components and how this listing was made
- A code architecture for creating design system agnostic user interfaces
- A proposition of a standard for common design system components and features with different levels of completeness, design system creators can choose which level of completeness to follow
- A React standard design system API for each component of the standard list

# Part 1 : Overview
## Basic code architecture
## Design system implementation bridges
## Design tokens

# Part 2 : Listing and organizing common design systems components
# List of input components
Inputs components are meant to provide user input to the frontend code. They are ordered below by data type.

## string
- text input
- password input
- url input
- email input
- phone input
## boolean
- checkbox
- switch
## enumeration
- select
- treeselect
- cascader
- radio buttons
## Set(enumeration)
- multiselect
- multitreeselect
## number
- numeric input
- slider
- rating
## number range
- range slider
## color
- color picker
## date
- date picker
## date range
- date range picker
## datetime
- datetime picker
## datetime range
- datetime range picker
## time
- time picker
## time range
- time range picker
## duration
- duration picker
## duration range
- duration range picker

# Part 3 : Creating a React API for each component

## Javascript frameworks
As of 2020, most used Javascript frameworks are React, Vue and Angular. They are similar but also quite different in the way they handle state managment with properties. For example, in React, one would make a controlled component using two props ```value``` and ```onChange```, whereas in Vue, usually a single property like ```value``` is needed. This means that we can't have a Javascript framework agnostic API. Ideally, we need to create one API for each Javascript framework, but of course they would be quite similar.

# General principles
- **Controlled components** : Each component must be able to be fully controlled from its parent component. This allows to implement specific behaviours in the parent component in a design system agnostic way.
- **No properties propagation** : Due to the wide variety of implementations, some components may not use the same HTML elements with different design systems. For example, a ```<Select/>``` component in a design system doesn't always use an HTML ```<select/>``` under the hood. Thus, we can't really make a generic property progragation specification.
- **Minimalist API** : If some features can be done with a small set of props, there's no need to provide additional props to realize that feature. For example, many components in design systems use a ```defaultValue``` prop, but the default value feature can be realized with ```value``` and ```onChange``` props, so we don't provide ```defaultValue``` props. 

# Form inputs components React API
## Common API

For all components : 

Features : 
 - validation status apprearance
 - success, warning and error messages
 - disabled state
 - focusable
 - autofocus

| prop               | type                                                   | default value | description                                     |
| ------------------ | ------------------------------------------------------ | ------------- | ----------------------------------------------- |
| validatationStatus | 'success' \| 'warning' \| 'error' \| 'loading' \| null | null          | Validation status appearance                    |
| successMessages    | [string]                                               | []            | List of success messages                        |
| warningMessages    | [string]                                               | []            | List of warning messages                        |
| errorMessages      | [string]                                               | []            | List of error messages                          |
| disabled           | boolean                                                | false         | Disables the component                          |
| value              | depends                                                | depends       | The value hold                                  |
| onChange           | (newValue) => {}                                       |               | Callback called when the user changes the value |

For textual inputs only :  

Features : 
 - constrained
 - mask
 - placeholder

| prop         | type     | default value | description                                                                   |
| ------------ | -------- | ------------- | ----------------------------------------------------------------------------- |
| constrained  | boolean  | true          | Wether the user can type any character or only the relevant ones are accepted |
| mask         | string   | ''            | Mask for masked text inputs                                                   |
| placeholder  | string   | ''            | Placeholder                                                                   |
| onPressEnter | () => {} |               | The callback function that is trigger when the 'Enter' key is pressed         |

## text
### text input
A canonical component to input textual data.
```jsx=
<Input/>
<Input type='text'/>
```

Features : 
 - placeholder
 - visibility toggle

**value** : a string representing the content of the text input.

### password input
A semantic variant of the text input.
```jsx=
<Input type='password'/>
```
Features : 
 - placeholder
 - visibility toggle

| prop             | type    | default value | description                        |
| ---------------- | ------- | ------------- | ---------------------------------- |
| visibilityToggle | boolean | true          | Shows a toggle visibility button   |

**value** : a string representing the content of the password input.

### url input
A semantic variant of the text input.
```jsx=
<Input type='url'/>
```

**value** : a string representing the content of the url input.

### email input
A separable component, semantic variant of the text input.
```jsx=
<Input type='email'/>
```

**value** : a string representing the content of the email input.

### phone number input
A semantic variant of the text input.
```jsx=
<Input type='phone'/>
```

Features : 
  - international
  - country select

| prop                 | type                      | default value        | description                                  |
| -------------------- | ------------------------- | -------------------- | -------------------------------------------- |
| countries            | [<country_code>] \| 'all' | 'all'                | Countries for which auto format is supported |
| countryValue              | <country_code>            | <first of countries> | The selected country                         |
| onCountryChange      | (newCountry) => {}        | () => {}             | Callback for country changes                 |
| disableCountrySelect | boolean                   | false                | Disable the country select                   |

Additional props are populated into the internal ```<input/>``` element.

**Output value** : a string representing the content of the email input.

### text area
A resizable text input.
```jsx=
<Textarea/>
```
Props are populated into the internal ```<textarea/>``` element.

**Output value** : a string representing the content of the text area.

## boolean
### checkbox
A canonical component to input boolean data.
```jsx=
<Input type='checkbox'>
```

Additional features : 
  - label

| prop  | type           | default value | description                     |
| ----- | -------------- | ------------- | ------------------------------- |
| label | string \| null | null          | The label next to the checkbox. |

Additional props are populated into the internal ```<input type='checkbox'/>``` element.

**Output value** : a boolean representing the state of the checkbox.

### switch
A canonical component to input boolean data, alternative to the checkbox.
```jsx
<Switch/>
```
Since internal implementation of the switch differs according to the design
system, additional props are not populated into a specific internal element.

Instead we provide a complete API to interact with the component and/or a ref of this component.

Additional features : 
  - label

| prop      | type               | default value | description                                 |
| --------- | ------------------ | ------------- | ------------------------------------------- |
| label     | string \| null     | null          | The label next to the checkbox              |
| checked   | boolean            | false         | Wether the toggle is on or off              |
| name      | string             | ''            | The value for form submission               |
| onChange  | (newChecked) => {} | () => {}      | Callback for checked changes                |
| onBlur    | () => {}           | () => {}      | Callback called when leaving the component  |
| onFocus   | () => {}           | () => {}      | Callback called when entering the component |
| autoFocus | boolean            | false         | Focus on component on page load             |

Ref functions : 
| name  | description         |
| ----- | ------------------- |
| blur  | Blur the component  |
| focus | Focus the component |

**Output value** : a boolean representing the state of the checkbox.

## enum
### select
A canonical component to input enumeration data.
```jsx=
<Select />
```
Props are populated into the internal ```<select></select>``` element.

**Input value** : 
```javascript=
[
  {
    name: string,
    displayName: string,
    icon: () => {},
    disabled: boolean
  },
  {
    name: string,
    displayName: string,
    icon: () => {},
    disabled: boolean
  }
]
```
**Input value (using groups)** : 
```javascript=
{
  groupName: [
    {
      name: string,
      displayName: string,
      icon: () => {},
      disabled: boolean
    },
    {
      name: string,
      displayName: string,
      icon: () => {},
      disabled: boolean
    }
  ],
  groupName2: [
    {
      name: string,
      displayName: string,
      icon: () => {},
      disabled: boolean
    },
    {
      name: string,
      displayName: string,
      icon: () => {},
      disabled: boolean
    }
  ],
}
```

**Ouput value** : the name of the select option.

Additional features :
 - search
 - clearable
 - items icons
 - groups
 - disabled option
 - (TODO) server side data loading

| prop      | type    | default value | description                 |
| --------- | ------- | ------------- | --------------------------- |
| search    | boolean | false         | Enable search functionality |
| clearable | boolean | true          | Enable clear functionality  |

### treeselect
A component to input enumeration data, variant of the select.
```jsx=
<TreeSelect/>
```
Since internal implementation of the treeselect differs according to the design
system, additional props are not populated into a specific internal element.

Instead we provide a complete API to interact with the component and/or a ref of this component.

**Input value** : 
```javascript=
{
  name: string,
  displayName: string,
  disabled: boolean,
  children: [
    {
      name: string,
      displayName: string,  
      disabled: boolean,
      children: []
    }
  ]
}
```

**Output value** : a list of ```name``` values representing the path from root to the selected node.

Additional features :
  - search
  - non terminal node selection

| prop      | type             | default value | description                                 |
| --------- | ---------------- | ------------- | ------------------------------------------- |
| search    | boolean          | false         | Enable search functionality                 |
| selection | 'leaf' \| 'any'  | 'leaf'        | Which type of node can be selected          |
| value     | String           | ''            | Name of the selected node.                  |
| onChange  | (newValue) => {} | () => {}      | Callback for value changes                  |
| onBlur    | () => {}         | () => {}      | Callback called when leaving the component  |
| onFocus   | () => {}         | () => {}      | Callback called when entering the component |
| autoFocus | boolean          | false         | Focus on component on page load             |

Ref functions : 
| name  | description         |
| ----- | ------------------- |
| blur  | Blur the component  |
| focus | Focus the component |

### cascader
A component to input enumeration data, variant of the select.
```jsx=
<Cascader/>
```

Since internal implementation of the cascader differs according to the design
system, additional props are not populated into a specific internal element.

Instead we provide a complete API to interact with the component and/or a ref of this component.

**Input value** : 
```javascript=
{
  name: string,
  displayName: string,
  disabled: boolean,
  children: [
    {
      name: string,
      displayName: string,  
      disabled: boolean,
      children: []
    }
  ]
}
```

**Output value** : a list of ```name``` values representing the path from root to the selected node.

Additional features :
  - search

| prop      | type             | default value | description                                 |
| --------- | ---------------- | ------------- | ------------------------------------------- |
| search    | boolean          | false         | Enable search functionality                 |
| value     | String           | ''            | Name of the selected node.                  |
| onChange  | (newValue) => {} | () => {}      | Callback for value changes                  |
| onBlur    | () => {}         | () => {}      | Callback called when leaving the component  |
| onFocus   | () => {}         | () => {}      | Callback called when entering the component |
| autoFocus | boolean          | false         | Focus on component on page load             |

Ref functions : 
| name  | description         |
| ----- | ------------------- |
| blur  | Blur the component  |
| focus | Focus the component |


### radio buttons
A canonical component to input enumeration data.
```jsx=
<input type='radio'/>
```

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

# Part 4
Other components not handled by this specification : 
- transfer
- sortable
- rich text input

# Glossary
**semantic variant** : 
**composable data type** : 
**variant** : 
**semantic variant** : 
**canonical component** : 
**property** : 
**component feature** : 

