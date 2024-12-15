# About axes
Much like d3 ```scales``` d3 ```axes``` are also *functions* whose parameters you define. Unlike scales, when called, instead of returning values, it generates the visual elements of the axis including line, labels and ticks.

Note that axis functions are SVG-specific, as they generate SVG elements. Also axes are intended for use with quantitative scales (not ordinal or categorical values)

There are four different axis function constructors

- ```d3.axisTop``` to generate ticks and labels on the top
- ```d3.axisBottom`` to generate ticks and lables in the bottom
- ```d3.axisLeft``` ticks and labels on the left
- ```d3.axisRight``` ticks and lables on the right


To generate axis function

```javascript
const xAxis = d3.axisBottom()
```

At a minimum each axis needs to be told on what scale to operate.

```javascript
xAxis.scale(xScale)
```

You could be concise by chaining scale at the initialization

```javascript
const xAxis = d3.axisBotton().scale(xScale)
```

You could actually simply pass scale as argument

```javascript
const xAxis = d3.axisBottom(xScale)
```

And just like scale we have to actually call axis function to generate lines, labels and ticks.

We usually call them at the end of the script.

```javascript
svg.append("g").call(xAxis)
```

