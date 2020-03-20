# GalacticProperties Component

#### Example Data structure for **Brightness vs Distance** plot
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

#### Example Data structure for **Color vs Distance** plot
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