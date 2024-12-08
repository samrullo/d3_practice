# What are scales?

From **input domain** to **output range**.

Imagine you have dataset of apple sales where each month 100 more apples are sold.
This is great. But if we tried to display apple sales as bar chard where bar height is linked to sales number
we easily run out of monitor size.
We need a way to translate apple sales to numbers that is suitable to represent bar heights in the graph.

# Domains and Ranges

A _scale's_ input domain is the range of possible input values.
For instance _input domain_ for the volume of equities traded daily could 0 and 100 bln.

A _scale's output range_ is the range possible output values.
For equities daily traded volume we could specify it between 0 and 100

# Normalization

D3 is just normalizing data from _input domain_ to values between 0 and 1 and then translating it to _output range_.
A simple normalization technique is `(x - x_min)/(x_max - x_min)`. This formula will normalize data between 0 and 1.
Then you can translate normalized `x` values to _output range_ with formula `x * (x_out_max - x_out_min) + x_out_min`

# How to use scaler

You can initialize a linear scaler using code below

```javascript
const scale = d3.scaleLinear();
```

We can set _input doman_ and _output range_ as below

```javascript
scale.domain([100, 500]);
scale.range([10, 350]);
```

Above steps can be chained together when initializing a scaler.

```javascript
const scale = d3.scaleLinear().domain([100, 500]).range([10, 350]);
```

# Let's scale our data for scatterplot

Remember that data to draw a scatterplot was an array of arrays. Each item in the array was was a two item array,
namely representing x and y coordinates.
Instead of hard coding _input domain_ and _output range_ by meticulously observing our data, we could leverage `d3.min()` and `d3.max()` functions to specify the ranges.
By default these two functions operate on a flat array and return minimum and maximum values from the array correspondingly.
But when working with an array of arrays, we can pass a function to them to explixitly tell what value of inner arrays to operate on.

```javascript
let risk_returns = [
  [20, 30],
  [24, 12],
  [10, 13],
  [34, 43],
  [78, 21],
  [3, 4],
  [12, 13],
  [14, 15],
  [16, 17],
];
let risk_min = d3.min(risk_returns, (d) => {
  return d[0];
});
let risk_max = d3.max(risk_returns, (d) => {
  return d[0];
});

let return_min = d3.min(risk_returns, (d) => {
  return d[1];
});
let return_max = d3.max(risk_returns, (d) => {
  return d[1];
});
```

Now for our scatterplot we can define _scales_ using above functions.
Below code assumes height and width variables are predefined.

```javascript
let risk_returns = [
  [20, 30],
  [24, 12],
  [10, 13],
  [34, 43],
  [78, 21],
  [3, 4],
  [12, 13],
  [14, 15],
  [16, 17],
];

const xScale = d3
  .scaleLinear()
  .domain([
    0,
    d3.max(risk_returns, (d) => {
      return d[0];
    }),
  ])
  .range([0, width]);
const yScale = d3
  .scaleLinear()
  .domain([
    0,
    d3.max(risk_returns, (d) => {
      return d[1];
    }),
  ])
  .range(0, height);
```

When you render above scatterplot, you will notice that lower y values appear at the top.
We can easily fix that by changing ```.range([0, height])``` to ```.range([height, 0])```

You will see some circles are disappearing beyond borders.
We can fix that by introducing padding and then settings ranges as ```.range([padding, w-padding])```
But even after introducing padding text labels still get cut off on the right side.
To fix that we can double padding for the right edge of the range ```.range([padding, w - 2*padding])```
