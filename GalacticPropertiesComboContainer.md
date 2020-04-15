# Galactic Properties Combo Container

## General

The use of this widget is to display both Color vs Distance and Brightness vs Distance in the same space as a comparison of one another.
The use of a basic plotter helps to better differentiate the fact that although the object being viewed may be brighter does not necessarily mean the object is closer to us, but the color of the object also defines the distance. This widgets is currently only used in the Exploring the Observable Universe Investigation.


[[/images/galacticPropertiesComboContainer.gif|Galactic Properties Combo Container Widget]]

## Page Data

| Field name |  Type  | Description                                                                    |
| ---------- | :----: | ------------------------------------------------------------------------------ |
| type       | string | `WidgetBlock.jsx` maps each `type` to the Class name of an available Component |
| source     | string | Each Component uses `source` in an http request to get data; Conventionally    |

## Container

Some general information about this container that makes it unique to it's container counterparts.

#### Props

| Prop name |  Type  | Description                                                                                                                          |
| --------- | :----: | ------------------------------------------------------------------------------------------------------------------------------------ |
| data      | object | Currently, does not seem to have a use in this case as the component is externally fetching the json data needed for this component. |
| options   | object | The `options` property defined in the `widget` field in the data structure                                                           |
| widget    | object | The 'raw' `widget` data defined in the json structure.                                                                               |

## Components

This container uses a few components in it's final render method. These components are as defined below:

### NavDrawer

#### Props

| Prop Name           |  Type  | Description                                                                                                         |
| ------------------- | :----: | ------------------------------------------------------------------------------------------------------------------- |
| interactableToolbar |  bool  | If prop is present, value is true, else value will be accepted as false.                                            |
| cardClasses         | string | ClassName that is directly imported from `galactic-properties.module.scss`                                          |
| contentClasses      | string | ClassName that directly imported from `galactic-properties.module.scss`                                             |
| navItems            | array  | An array of custom navigation links used in the NavDrawer that are typically used to switch views of the container. |
| toolbarTitle        | string | The title to display in the Toolbar                                                                                 |

### GalacticProperties

#### Props

| Prop Name         |   Type   | Description                                                                                                                                                                  |
| ----------------- | :------: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| className         |  string  | ClassName provided to the component. Within this container the class name is statically set to "color-brightness-vs-distance-combo"                                          |
| options           |  object  | `options` defined in the json data                                                                                                                                           |
| data              |  array   | An array of point information that will be plotted                                                                                                                           |
| xAxisLabel        |  string  | The label of the `x` axis                                                                                                                                                    |
| yAxisLabel        |  string  | The label of the `y` axis                                                                                                                                                    |
| xValueAccessor    |  string  | The accessor of the `x` axis                                                                                                                                                 |
| yValueAccessor    |  string  | The accessor of the `y` axis                                                                                                                                                 |
| tooltipAccessors  |  array   | An array of accessors to be utilized in the tooltip                                                                                                                          |
| tooltipLabels     |  array   | An array of labels that will be rendered in the tooltip                                                                                                                      |
| xDomain           |  array   | An array of number ranges for the `x` axis                                                                                                                                   |
| yDomain           |  array   | An array of number ranges for the `y` axis                                                                                                                                   |
| selectionCallback | function | Callback from this component to `GalacticPropertiesComboContainer` component (parent) _or_ how the _child_ (this component) passes information back to the parent container. |
