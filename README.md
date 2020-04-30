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
### text input
#### common semantics
 - password
 - address
 - url
 - email
 - phone number
#### text area
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
 - groups
## number
### numeric input
#### Possible semantics
 - percent
 - money
 - temperature
 - any other unit
### slider
### rating
## color
### color picker
Possible features :
- palette
- different color formats
- list of last chosen colors
## day-month-year (alias 'date')
### datepicker
## seconds-minutes-hour-day-month-year (alias 'datetime')
### datetimepicker
## seconds-minutes-hour (alias 'time')
### timepicker
## week-month-year (alias 'weekdate')
### weekdatepicker
## month-year (alias 'monthdate')
### monthdatepicker
## year
### yearpicker
## day
### daypicker
## week
### weekpicker
## month
### monthpicker
## duration
### durationpicker
## file
### filepicker
Possible features :
- filedrop
- uploaded image preview
