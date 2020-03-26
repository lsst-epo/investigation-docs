Note: `Filename` is page title so should be something like `Widget Name`

## General
First and foremost this is the place to describe what this widget is.  How are we using it?  What kind of experience does it offer the user? What scientific concepts, tools, or graphs does it relate to?  How accurate is it?  What investigations is it used in?  Is it used differently in different investigations? What kind of data is it visualizing?

All Widgets stare a similar file structure: a collection of `components` wrapped in a `container`.  The `container` is responsible for initial setup, data fetching, storing state shared across children, and "communication" between children (mainly via callbacks that are class methods on the `container`).  This is a common separation of concerns and likely goes without saying.  What should be included in this section is any abnormal patterns, file structures, dependencies (like D3 or eCharts), or other exceptional-isms.  

This is also a good place for a screenshot, GIF, or short video that gives a clear visual indication of what widget this is.

## Page Data
This is the highest level information that defines Widget behavior/Appearance.

It is JSON that informs the component itself, not it's layout on the page.  Two fields that will likely be shared across any/all components are `type` and `source` as `type` tells our React app to put it on the page in the first place, and `source` provides a file path for the data the widget uses, and the lion's share of our widgets are data-driven.  In most cases these fields are fairly self-descriptive, however 

The most influential and unique data fields are the `options`, however, this is probably not the place to call out what each and every `option` does.  Rather, this is a good place to callout which options are used, and how they related to props on the widget component.  If there are options used that do not map 1:1 to props, this **is** the place to callout what they do.

Examples of these blocks of JSON can be elucidating, however any specific fields called out should be laid out in a clear, identifiable way.  I like tables, but headings + paragraphs, or other demarcation/whitespace do just as good of a job.

| Field Name | Type | Description |
| ---        | ---    | ---       |
| type       | string | `WidgetBlock.jsx` maps each `type` to the Class name of an available Component |
| source     | string | Each Component uses `source` in an http request to `GET` data; Conventionally  |

## Container
Any general info about the container goes here.  This is a good place for a screenshot, GIF, or short video if there are variants, behaviors, or unique visual qualities defined at the level of the container.

#### Props
Any info specific to the container's `props` goes here.

| Prop Name | Type | Description |
| ---        | ---    | ---       |
| name       | type (+ any internal data structure) | what it does, how its used, variants, is it required, does it get passed through to child components, etc.   |

#### Special Methods
Any info about Class methods, callbacks, etc. that play a vital role in the behavior/appearance of this widget, and/or deserve demystifying.  This might include, but is not limited to methods manipulating the DOM, D3, other external libraries, or local/global state.

## Component(s)
Any general info about the component goes here.  This is a good place for a screenshot, GIF, or short video if there are variants, behaviors, or unique visual qualities defined at the level of the component.

#### Props
Any info specific to the component's `props` goes here.  If the `container` wraps several components, each component gets its own section in **Props**

| Prop Name | Type | Description |
| ---        | ---    | ---       |
| name       | type (+ any internal data structure) | what it does, how its used, variants, is it required, does it get passed through to child components, etc.   |

#### Special Methods
Any info about Class methods, callbacks, etc. that play a vital role in the behavior/appearance of this widget, and/or deserve demystifying.  This might include, but is not limited to methods manipulating the DOM, D3, other external libraries, or local/global state.

#### Known Issues
Any info about stuff that is broken, does not behave how a typical user/dev would expect, or other weirdness.  In particular call out any issues we know we intend to fix.

## Examples
Code examples and descriptions of what the yield on the frontend (another good place for a screenshot, GIF, or short video); Deep dives into gotchas, tricky state management, overrides on `react-md` components, UI/UX, etc. Each example should have its own h4 heading. 

