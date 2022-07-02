# Plotly
## Belly Button Biodiversity
Using Plotly to make interactive charts

### Tools: Javascript, Plotly, D3, html/css

## Overview
The purpose of this analysis was to create a dashboard to display interactive charts with Plotly that change with the selection of a different volunteer ID in a dropdown menu. Using D3 to import data from an external 'samples.json' the code builds charts after initializing the first ID (in this case 940) to display charts associated with the first ID on the page.

## Results
![Screen Shot 2022-07-02 at 11 38 19 AM](https://user-images.githubusercontent.com/99676466/177010758-ecbb7394-2148-45bc-a190-ee28ebba1d38.png)

The page begins by an init function as shown in the following code:
~~~
function init() {
  // Grab a reference to the dropdown select element
  var selector = d3.select("#selDataset");

  // Use the list of sample names to populate the select options
  d3.json("samples.json").then((data) => {
    var sampleNames = data.names;

    sampleNames.forEach((sample) => {
      selector
        .append("option")
        .text(sample)
        .property("value", sample);
    });

    // Use the first sample from the list to build the initial plots
    var firstSample = sampleNames[0];
    buildCharts(firstSample);
    buildMetadata(firstSample);
  });
}

// Initialize the dashboard
init();

function optionChanged(newSample) {
  // Fetch new data each time a new sample is selected
  buildMetadata(newSample);
  buildCharts(newSample);
}
~~~
This is displayed and linked to a change which is a selDataset. The change then builds new metadata and charts based on the selector in the dropdown. There is a demographics panel associated with the ID of the subject. Then there are three charts created: a bar chart with the ten bacteria associated by an OTU id and OTU label(which is shown in the graphs by hovering over the bar or bubble), a bubble chart, and a gauge chart. The bar chart:

![newplot (3)](https://user-images.githubusercontent.com/99676466/177010911-650ea497-37c2-4ebb-ba0b-8232cd6aa3c1.png)

Where the trace for the chart contains the following:
* The y values are the otu_ids in descending order
* The x values are the sample_values in descending order
* The hover text is the otu_labels in descending order.
And the data in the dashboard has the following:
* The top 10 sample_values are sorted in descending order
* The top 10 sample_values as values
* The otu_ids as the labels

The bubble chart shows the bubble sizes based on sample values, and bubble coors based on labels or bacterium based on the selected individual. 
* The otu_ids as the x-axis values.
* The sample_values as the y-axis values.
* The sample_values as the marker size.
* The otu_ids as the marker colors.
* The otu_labels as the hover-text values.

![newplot (4)](https://user-images.githubusercontent.com/99676466/177011024-3919eef8-2772-4aee-afa1-859f2c22116e.png)

And the gauge show the frequency at which the selected individual's belly button is washed: 

![newplot (5)](https://user-images.githubusercontent.com/99676466/177011165-23b91bc1-1ebd-4487-abe1-2dc0c4ffa04c.png)

## Summary
The dashboard is customized with Boostrap and HTML and the following three customizations:
* Add an image to the jumbotron.
* Add background color or a variety of compatible colors to the webpage.
* Use a custom font with contrast for the colors.

The dashboard is displayed on [Github Pages](https://emaynard10.github.io/Plotly_bbBiodiversity/)

 
