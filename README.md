# DateStructure package

The package allows to store a complex date structure in template fields.
The package includes the following pages:

* `Form:Date` - a partial form to be transcluded into other forms
* `Template:Date` - a template that renders a single date item
* `Template:DateFormatDate` - a template that formats a date

The `Date` partial form includes the following fields:

* `Present` - The flag idicates the date is present date
* `Date` - The date, can be a partial date like Year only, or month & year only
* `Circa` - Boolean to indicate that date may be fuzzy
* `Concurrence` - Can be set to: Exact, Before, After
* `Questionable` - Can be checked to mark the date as questionable

# Demo pages

The package also includes sample `SampleDateTemplate` and `SampleDateForm` as
a usage examples. You can import the package and navigate to `SampleDate1`
to test it right away.

# Usage examples

The form is to be transcluded into other forms directly via `{{Form:Date}}` like below:

```
...
{{{for template|MyTemplate}}}
{|
| Creation date
| {{Form:Date|Prefix=Creation}}
|-
| Publication date
| {{Form:Date|Prefix=Publication}}
|-
|}
{{{end template}}}
...
```

And in the resulting `MyTemplate` the fields need to be processed via `Date` template like below:


```
; Creation date
: {{Date
  |Creation
  |Present={{{Creation Present|}}}
  |Date={{{Creation Date|}}}
  |Circa={{{Creation Circa|}}}
  |Concurrence={{{Creation Concurrence}}}
  |Questionable={{{Creation Questionable}}}
  |EndPresent={{{Creation Present End|}}}
  |EndDate={{{Creation Date End|}}}
  |EndCirca={{{Creation Circa End|}}}
  |EndConcurrence={{{Creation Concurrence End|}}}
  |EndQuestionable={{{Creation Questionable End|}}}
}}
; Publication date
: {{Date
  |Publication
  |Present={{{Publication Present|}}}
  |Date={{{Publication Date|}}}
  |Circa={{{Publication Circa|}}}
  |Concurrence={{{Publication Concurrence}}}
  |Questionable={{{Publication Questionable}}}
  |EndPresent={{{Publication Present End|}}}
  |EndDate={{{Publication Date End|}}}
  |EndCirca={{{Publication Circa End|}}}
  |EndConcurrence={{{Publication Concurrence End|}}}
  |EndQuestionable={{{Publication Questionable End|}}}
}}
```

Each date has optional end date value, this is controlled by the `Has end date?` checkbox.
When ticket it will reveal a set of fields for the end date to be entered. The fieldset is similar
for the start date.

If the end date is set on the form the resulting template will render two dates in the following format:

```
date1(non-breaking space)(dash)(space)date2
```

the template will also pass this data to the subobject as the following properties:

* `Present`
* `Date`
* `Circa`
* `Concurrence`
* `Questionable`
* `EndDate`
* `EndDateCirca`
* `EndDateConcurrence`
* `EndDateQuestionable`

please note: that in all cases both start and end date fields are filled with values, even if the date
has no `Has end date?` checkbox ticked the `End` prefixed properties will receive a values from the original
date, in other words if no end date is added the end date matched the start date

# Requirements

* MediaWiki 1.30+
* PageForms
* PageExchange
* SemanticMediawiki

# Setup

* Add the following line to your LocalSettings.php `$wgPageExchangePackageFiles[] = 'https://raw.githubusercontent.com/NationalGalleryOfArt/mediawiki-pages-Dates/main/page-exchange.json';`
* Navigate to `Special:Packages` and install the package

# Styling

The `Form:Date` wraps the date inputs into the following markup:

* `div.dates-input-block` - wraps the whole set if inputs for a single field
* `div.dates-input-block--date` - wraps a single date input (either start or end date)
* `div.dates-input-block--start` - wraps start date block only
* `div.dates-input-block--end` - wraps end date block only
* `div.dates-input-block--date-title` - wraps block title ("Start date", "End date") visible when ranged date is enabled

You can style these by altering the selectors above
