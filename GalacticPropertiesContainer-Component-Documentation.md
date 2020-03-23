# GalacticPropertiesContainer Component

### Data structure to render this Component

```json

      "type": "GalacticProperties",
      "source": "/data/galaxies/hsc/hsc_sub01.json",
      "layout": {
        "col": "right",
        "row": "top"
      },
      "options": {
```

#### `options` for **Brightness vs Distance** plot

```json
      "options": {
        "title": "Brightness Vs Distance",
        "xAxisLabel": "Distance (Billion Ly)",
        "yAxisLabel": "Total Brightness",
        "xValueAccessor": "distance",
        "yValueAccessor": "brightness",
        "tooltipAccessors": ["distance", "brightness"],
        "tooltipUnits": ["Billion Ly"],
        "tooltipLabels": ["Distance", "Brightness"],
        "domain": [[0, 28], [0, 200]]
      }
```

#### `options` for **Color vs Distance** plot

```json
      "options": {
        "title": "Color Vs Distance",
        "xAxisLabel": "Distance (Billion Ly)",
        "yAxisLabel": "Flux ratio i/z (color)",
        "xValueAccessor": "distance",
        "yValueAccessor": "color",
        "tooltipAccessors": ["distance", "color"],
        "tooltipUnits": ["Billion Ly", "Flux ratio"],
        "tooltipLabels": ["Distance", "Color"],
        "domain": [[0, 16], [0, 2]]
      }
```

The `domain` field above is the range provied for the `tick` marks in the plot. The `[0]` index of `domain` refers to the _x-axis_ and the `[1]` index refers to the _y-axis_.

### Understanding its container and methods

These are the imports in the constructor to start the file.

```javascript
import React from 'react';
import PropTypes from 'prop-types';
import isArray from 'lodash/isArray';
import API from '../lib/API.js';
import GalacticProperties from '../components/charts/galacticProperties/index.jsx';
```

The `constructor` takes in `props` as its only argument. The `this.state` is then initialized with a `data: null` object.

```javascript
constructor(props) {
  super(props);

  this.state = {
    data: null,
  };
}

componentDidMount() {
  const {
    widget: { source, options },
  } = this.props;
  const { multiple } = options || {};
```

The `componentDidMount()` fetchs the needed data via from the `source` (extracted from the `options` in `this.props`) and massages it down via the `this.getDataObjects(data, multiple)` method in order to store that result in the `data` object in `this.state`.

```javascript
  API.get(source).then(response => {
    const { data } = response;
    const responseData = this.getDataObjects(data, multiple);

    this.setState(prevState => ({
      ...prevState,
      data: responseData,
    }));
  });
}
```

This function checks first to see if the `multiple` flag is `true` and if so, runs a map function to return just the `object` array from each of the objects in the array.

```javascript
getDataObjects = (data, multiple) => {
  if (multiple) {
    return data.map(targetData => {
      if (!targetData.objects) return null;
      return targetData.objects;
    });
  }
```

Otherwise just returns the `objects` array if it exists. Else, it returns an empty array.

```javascript
  return isArray(data.objects) ? data.objects : [];
};
```

This next method is used to handle any responses or interactions from the child. This method is fired from the `selectionCallback` property on the `GalacticProperties` component.

```javascript
userGalacticPropertiesCallback = data => {
    console.log({ data }); // eslint-disable-line no-console
};
```

Coming down into the `render()` method, we deconstruct all necessary variables stored/updated in `this.state` and `this.props` to bind into our `GalacticSelector` component.

```javascript
  render() {
    const { data } = this.state;
    const { options } = this.props;
    const {
      title,
      xAxisLabel,
      yAxisLabel,
      xValueAccessor,
      yValueAccessor,
      tooltipAccessors,
      tooltipUnits,
      tooltipLabels,
    } = options || {};

    return (
      <>
        <h2 className="space-bottom">{title || 'Brightness Vs Distance'}</h2>
        <GalacticProperties
          className="brightness-vs-distance"
```

In the `<GalacticProperties>` component are explicitly inject the lables, accessors, and units, respectively. Additionally, the callback function `this.userGalacticPropertiesCallback` is bound into the `selectionCallback` prop.

```javascript
          {...{
            data,
            options,
            xAxisLabel,
            yAxisLabel,
            xValueAccessor,
            yValueAccessor,
            tooltipAccessors,
            tooltipUnits,
            tooltipLabels,
          }}
```

Additionally, the callback function `this.userGalacticPropertiesCallback` is bound into the `selectionCallback` prop.

```javascript
          selectionCallback={this.userGalacticPropertiesCallback}
        />
      </>
    );
  }
}
```

Declaring the props that will be injected into this component is essential as this is how the file is _type scripted_ / _type decalared_.

```javascript
GalacticPropertiesContainer.propTypes = {
    data: PropTypes.object,
    options: PropTypes.object,
    widget: PropTypes.object,
};

export default GalacticPropertiesContainer;
```
