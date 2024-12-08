# How do I get started with d3?

I downloaded the whole library from https://d3js.org/getting-started#d3-in-vanilla-html link.

# Tell me about data bindings

d3 binds data such as an array of numbers to DOM elements.

For instance the below example shows how we bind data to a paragraph

```javascript
let dataset = [5, 10, 15, 20, 25];
d3.select("body")
  .selectAll("p")
  .data(dataset)
  .enter()
  .append("p")
  .text("New paragraph!");
```

In above you select **body**, then you select all **p** elements, then you bind data from **dataset** to **p** elements.
Once you run **enter** and then **append**, d3 will append a paragraph for every item in the array.
You can specify the text of the paragraph with **text** attribute.
I would read above code as

- Select body
- Select all paragraphs within body
- bind dataset to paragraphs
- enter iteration process
- for every item in the dataset array append a paragraph into body
- set the text of each paragraph to "New text"

Now of course above code isn't doing much. We did data binding but we are not using data at all.
How about displaying data value in the text of the paragraph and setting the color of the text based on the value of data?
Below is how you can achieve it.

```javascript
let dataset = [1, 2, 3, 4, 5, 6, 7];
d3.select("body")
  .selectAll("p")
  .data(dataset)
  .enter()
  .append("p")
  .text((d) => {
    return "I count up to " + d;
  })
  .style("color", (d) => {
    if (d > 3) {
      return "red";
    } else {
      return "black";
    }
  });
```
