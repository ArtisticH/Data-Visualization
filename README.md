# D3.js

## 3. Work with Data in D3
```
<body>
  <ul></ul>
  <script>
    const dataset = ["a", "b", "c"];
    d3.select("ul").selectAll("li")
      .data(dataset)
      .enter()
      .append("li")
      .text("New item");
  </script>
</body>
```
`selectAll()`은 빈 배열을 반환하고, `data()`는 인수인 dataset의 개수만큼 다음 코드를 반복한다. (once for each item in the array.)
`data()` 메서드를 사용하여 선택한 요소와 데이터셋을 연결한다. 데이터셋의 각 항목이 연결된 요소와 매핑됩니다.
`enter()`는 `li`를 dataset의 갯수만큼 생성한다. (누락된 요소 생성)

## 4. Work with Dynamic Data in D3
```
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];

    d3.select("body").selectAll("h2")
      .data(dataset)
      .enter()
      .append("h2")
      .text((d) => `${d} USD`);
  </script>
</body>
```
`selection.text((d) => d)` 처럼 text 메서드는 인수로 string이나 콜백 함수를 받을 수 있고, 콜백 함수에서 매개변수 d는 refers to a single entry in the dataset that a selection is bound to.
 you have made use of the data that is bound to each of the h2 elements.
 
 ## 5. Add Inline Styling to Elements
 ```
 <body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];

    d3.select("body").selectAll("h2")
      .data(dataset)
      .enter()
      .append("h2")
      .text((d) => (d + " USD"))
      .style('font-family', 'verdana')
  </script>
</body>
 ```
 
## 6. Change Styles Based on Data
```
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];

    d3.select("body").selectAll("h2")
      .data(dataset)
      .enter()
      .append("h2")
      .text((d) => (d + " USD"))
      .style('color', (d) => {
        if (d < 20) {
          return 'red';
        } else {
          return 'green'
        }
      });
  </script>
</body>
```

## 7. Add Classes with D3
```
<style>
  .bar {
    width: 25px;
    height: 100px;
    display: inline-block;
    background-color: blue;
  }
</style>
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];

    d3.select("body").selectAll("div")
      .data(dataset)
      .enter()
      .append("div")
      .attr('class', 'bar');
  </script>
</body>
```

## 8. Update the Height of an Element Dynamically
```
<style>
  .bar {
    width: 25px;
    height: 100px;
    display: inline-block;
    background-color: blue;
  }
</style>
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];

    d3.select("body").selectAll("div")
      .data(dataset)
      .enter()
      .append("div")
      .attr("class", "bar")
      // Add your code below this line
      .style('height', (d) => d);
      // Add your code above this line
  </script>
</body>
```

## 9. Change the Presentation of a Bar Chart
```
<style>
  .bar {
    width: 25px;
    height: 100px;
    /* Add your code below this line */
    margin: 2px;
    /* Add your code above this line */
    display: inline-block;
    background-color: blue;
  }
</style>
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];

    d3.select("body").selectAll("div")
      .data(dataset)
      .enter()
      .append("div")
      .attr("class", "bar")
      .style("height", (d) => (d*10 + "px")) // Change this line
  </script>
</body>
```

## 10. Learn About SVG in D3
SVG stands for Scalable Vector Graphics.
Here "scalable" means that, if you zoom in or out on an object, it would not appear pixelated. 
It scales with the display system, whether it's on a small mobile screen or a large TV monitor.
SVG is used to make common geometric shapes. Since D3 maps data into a visual representation, it uses SVG to create the shapes for the visualization. 
SVG shapes for a web page must go within an HTML svg tag.
CSS can be scalable when styles use relative units (such as vh, vw, or percentages), but using SVG is more flexible to build data visualizations.

```
<style>
  svg {
    background-color: pink;
  }
</style>
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];

    const w = 500;
    const h = 100;

    const svg = d3.select("body")
                  // Add your code below this line
                  .append('svg')
                  .attr('width', `${w}`)
                  .attr('height', `${h}`)
                  // Add your code above this line
  </script>
</body>
```

This challenge created an svg element with a given width and height, which was visible because it had a background-color applied to it in the style tag. 
The code made space for the given width and height.

## 11. Display Shapes with SVG

```
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];

    const w = 500;
    const h = 100;

    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h)
                  // Add your code below this line
                  .append('rect')
                  .attr('width', '25')
                  .attr('height', '100')
                  .attr('x', '0')
                  .attr('y', '0')
                  // Add your code above this line
  </script>
</body>
```

The next step is to create a shape to put in the svg area.
There are a number of supported shapes in SVG, such as rectangles and circles. 
They are used to display data. For example, a rectangle (<rect>) SVG shape could create a bar in a bar chart.
  
## 12. Create a Bar for Each Data Point in the Set
  
A previous challenge showed the format for how to create and append a div for each item in dataset:
  
  
  ```
  d3.select("body").selectAll("div")
  .data(dataset)
  .enter()
  .append("div")
  ```
  
  There are a few differences working with rect elements instead of div elements. 
  The rect elements must be appended to an svg element, not directly to the body. 
  Also, you need to tell D3 where to place each rect within the svg area. 
  
  ```
  <body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];

    const w = 500;
    const h = 100;

    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);

    svg.selectAll("rect")
       // Add your code below this line
       .data(dataset)
       .enter()
       .append('rect')
       // Add your code above this line
       .attr("x", 0)
       .attr("y", 0)
       .attr("width", 25)
       .attr("height", 100);
  </script>
</body>
  ```
  
  ## 13. 
  ```
  <body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];

    const w = 500;
    const h = 100;

    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);

    svg.selectAll("rect")
       .data(dataset)
       .enter()
       .append("rect")
       .attr("x", (d, i) => {
         // Add your code below this line
          return i * 30
         // Add your code above this line
       })
       .attr("y", 0)
       .attr("width", 25)
       .attr("height", 100);
  </script>
</body>
  ```
  
  ## 14. Dynamically Change the Height of Each Bar
  ```
  <body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];

    const w = 500;
    const h = 100;

    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);

    svg.selectAll("rect")
       .data(dataset)
       .enter()
       .append("rect")
       .attr("x", (d, i) => i * 30)
       .attr("y", 0)
       .attr("width", 25)
       .attr("height", (d, i) => {
         // Add your code below this line
          return d * 3
         // Add your code above this line
       });
  </script>
  </body>
  ```
  
  ## 15. Invert SVG Elements
  
  ```
  <body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];

    const w = 500;
    const h = 100;

    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);

    svg.selectAll("rect")
       .data(dataset)
       .enter()
       .append("rect")
       .attr("x", (d, i) => i * 30)
       .attr("y", (d, i) => {
         // Add your code below this line
        return 100 - 3 * d;
         // Add your code above this line
       })
       .attr("width", 25)
       .attr("height", (d, i) => 3 * d);
  </script>
</body>
  ```
  
  ## 16. Change the Color of an SVG Element
  ```
  <body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];

    const w = 500;
    const h = 100;

    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);

    svg.selectAll("rect")
       .data(dataset)
       .enter()
       .append("rect")
       .attr("x", (d, i) => i * 30)
       .attr("y", (d, i) => h - 3 * d)
       .attr("width", 25)
       .attr("height", (d, i) => 3 * d)
       // Add your code below this line
      .attr('fill', 'navy')
       // Add your code above this line
  </script>
</body>
  ```
  
  ## 17. Add Labels to D3 Elements
  
  ```
  <body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];

    const w = 500;
    const h = 100;

    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);

    svg.selectAll("rect")
       .data(dataset)
       .enter()
       .append("rect")
       .attr("x", (d, i) => i * 30)
       .attr("y", (d, i) => h - 3 * d)
       .attr("width", 25)
       .attr("height", (d, i) => 3 * d)
       .attr("fill", "navy");

    svg.selectAll("text")
       .data(dataset)
       .enter()
       // Add your code below this line
        .append('text')
        .attr("x", (d, i) => i * 30)
        .attr("y", (d, i) => (h - 3 * d) - 3 )
        .text((d) => d)



       // Add your code above this line
  </script>
<body>
  ```
  
  ## 18. Style D3 Labels
  
  ```
  <body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];

    const w = 500;
    const h = 100;

    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);

    svg.selectAll("rect")
       .data(dataset)
       .enter()
       .append("rect")
       .attr("x", (d, i) => i * 30)
       .attr("y", (d, i) => h - 3 * d)
       .attr("width", 25)
       .attr("height", (d, i) => d * 3)
       .attr("fill", "navy");

    svg.selectAll("text")
       .data(dataset)
       .enter()
       .append("text")
       .text((d) => d)
       .attr("x", (d, i) => i * 30)
       .attr("y", (d, i) => h - (3 * d) - 3)
       // Add your code below this line



       // Add your code above this line
  </script>
</body>
  ```
  
  ## 19. Add a Hover Effect to a D3 Element
  
  
  
  
  


