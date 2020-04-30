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
touching to much code

# Components
## text
### Variants
#### text input
##### common semantics
 - password
 - address
 - url
 - email
 - phone number
#### text area
## boolean
### Variants
#### checkbox
#### switch
## enum
### Variants
#### select
Possible features :
 - search
 - items icons
 - groups
#### treeselect
Possible features :
  - search
#### cascader
Possible features :
  - search
#### radio buttons
## Set(enum)
### Variants
#### multiselect
Possible features :
 - search
 - icons
 - groups
#### multitreeselect
Possible features :
 - search
 - groups
## number
### Variants
#### numeric input
##### Possible semantics
 - percent
 - money
 - temperature
 - any other unit
#### slider
#### rating
## color
### Variants
#### color picker
Possible features :
- palette
- different color formats
- list of last chosen colors
## day-month-year (alias 'date')
### Variants
#### datepicker
## seconds-minutes-hour-day-month-year (alias 'datetime')
### Variants
#### datetimepicker
## seconds-minutes-hour (alias 'time')
### Variants
#### timepicker
## week-month-year (alias 'weekdate')
### Variants
#### weekdatepicker
## month-year (alias 'monthdate')
### Variants
#### monthdatepicker
## year
### Variants
#### yearpicker
## day
### Variants
#### yearpicker
## week
### Variants
#### weekpicker
## month
### Variants
#### monthpicker
## duration
### Variants
#### durationpicker
## file
### Variants
#### filepicker
Possible features :
- filedrop
- uploaded image preview
