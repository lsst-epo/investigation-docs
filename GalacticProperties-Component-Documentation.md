# GalacticProperties Component

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
The `domain` field above is the range provied for the `tick` marks in the plot. The `[0]` index of `domain` refers to the *x-axis* and the `[1]`  index refers to the *y-axis*.
### Understanding its container and methods

#### Constructor
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