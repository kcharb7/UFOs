# UFOs
## Overview
### *Purpose*
Dana, a Data Journalist, would like to write about UFO sightings in her hometown McMinnville, Oregon. She possessed a JavaScript file containing data on UFO sightings and would like to use JavaScript to display the data as a table with filters and display all the information on a HTML page. 

## Build Dynamic Table
In my repository, I created a new file named “app.js”. Within this file, I imported the UFO data:
```
// Import the data from data.js
const tableData = data;
```
Then, I referenced the tbody HTML tag using D3 to signify that the data will be stored in a table:
```
// Reference the HTML table using d3
var tbody = d3.select("tbody");
```
To begin building the table, I created a function called “buildTable” with the arguments “data”:
```
// Create function to build table
function buildTable(data) {

}
```
Next, I used code to clear existing data to create a fresh table for inserting the data:
```
// Create function to build table
function buildTable(data) {
    tbody.html("");
}
```
Within the “buildTable” function, I chained a forEach loop to the data to iterate through the array. I additionally created a variable to append a row to the table body:
```
// Create function to build table
function buildTable(data) {
    tbody.html("");
    data.forEach((dataRow) => {
        let row = tbody.append("tr");
    });
}
```
Below the line to append the rows, I set up another function to loop through each field in the dataRow argument. Then, I created two lines of code to append each value of the object to a cell in the table:
```
        Object.values(dataRow).forEach((val) => {
            let cell = row.append("td");
            cell.text(val);
```
After building the function, I added comments throughout to identify what the code is doing:
```
// Create function to build table
function buildTable(data) {
    // First, clear out any existing data
    tbody.html("");

    // Next, loop through each object in the data
    // and append a row and cells for each value in the row
    data.forEach((dataRow) => {
        let row = tbody.append("tr");

        // Loop through each field in the dataRow and add
        // each value as a table cell (td)
        Object.values(dataRow).forEach((val) => {
            let cell = row.append("td");
            cell.text(val);
        });
    });
};
```
Given the large amount of data on UFO sightings, I created a new function “handleClick” that used D3 to filter the table by date:
```
function handleClick() {
    let date = d3.select("#datetime").property("value");
    let filteredData = tableData;
}
```
Within the “handleClick” function, I additionally added an if statement so that the data was only filtered if a date was present:
```
function handleClick() {
    let date = d3.select("#datetime").property("value");
    let filteredData = tableData;
    if (date) {
        filteredData = filteredData.filter(row => row.datetime === date);
    }
}
```
To build a filtered table, I included the “buildTable” function under the if statement and used the “filteredData” variable as the argument within the function. The full “handleClick” function looked as follows:
```
// Create a function to filter the table
function handleClick() {
    // Grab the datetime value from the filter
    let date = d3.select("#datetime").property("value");
    let filteredData = tableData;

    // Check to see if a date was entered and filter the data using that date
    if (date) {
        // Apply 'filter' to the table data to only keep the
        // rows where the 'datetime' values match the filter value
        filteredData = filteredData.filter(row => row.datetime === date);
    };

    //Rebuild the table using the filtered data
    // @Note: If no date was entered, then the filteredData will
    // just be the original tableData
    buildTable(filteredData);
};
```
Under the “handleClick” function, I used another aspect of D3.js so that the code would listen for a button click:
```
// Attach an event to listen for the form button
d3.selectAll("#filter-btn").on("click", handleClick);
```
Finally, at the end of the code, I called the “buildTable” function once more using the original data so that the table loaded as soon as the page did:
```
// Build the table when the page loads
buildTable(tableData);
```

## Build the HTML
I used the exclamation mark shortcut to autofill the basic HTML layout in my index.html file. Then, I changed the title of the document to “UFO Finder”. Under the title of the document, I added a link to Bootstrap’s content delivery network, as well as a link to my stylesheet:
```
    <title>UFO Finder</title>
    <link
      rel="stylesheet"
      href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css"
      integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm"
      crossorigin="anonymous"
    />
    <link rel="stylesheet" href="static/css/style.css">
```
Within the body tags, I added a div tag with a class of “wrapper”:
```
<body>
    <div class="wrapper">

    </div>  
</body>
```
Within the wrapper I added a nav tag with a class of “navbar navbar-expand-lg”:
```
    <div class="wrapper">
        <nav class="navbar navbar-expand-lg">

        </nav>
    </div>  
```
I added functionality to the navbar to reset the webpage after a filter has been applied to the table:
```
        <nav class="navbar navbar-expand-lg">
            <a class="navbar-brand" href="index.html">UFO Sightings</a>
        </nav>
```
Under the navbar, I set up the jumbotron by adding div tags, the class “jumbotron”, and a header that read “The Truth Is Out There”:
```
    <div class="jumbotron">
        <h1>The Truth Is Out There</h1>
    </div>
```
To add the article title and paragraph, I created a div with a class of “container-fluid” and nested a row within it:
```
    <div class="container-fluid">
        <div class="row">
        </div>
    </div>
```
Within the above div, I assigned four columns to the article title and the reaming eight to the paragraph:
```
    <div class="container-fluid">
        <div class="row">
            <div class="col-md-4">

            </div>
            <div class="col-md-8">
  
            </div>
        </div>
    </div>
```
Then, I nested the article title using an h3 tag in the first column:
```
            <div class="col-md-4">
                <h3>UFO Sightings: Fact or Fancy? <small>Ufologists Weigh In</small></h3>
            </div>
```
In the second div that used 8 columns, I added Dana’s article paragraph:
```
          <div class="col-md-8">
            <p>
              Are we alone in the universe? For millennia, humans have turned to the sky to answer this question. Now, thanks to research generously funded by W. Avy, a UFO-enthusiast and amateur ufologist, we can supplement our sky-searching with data analysis.<br><br>"The release of this analysis is well-timed: It coincides with the celebration of World UFO Day, which is a moment for ufologists around the world to connect, relax, and sample a range of UFO-themed snacks," said Dr. Ursula F. Olivier, the world's preeminent expert on circular sightings. "Citizen-scientists can be especially helpful in both cataloguing sightings—which is hugely helpful for us in our search for aliens—and in helping us celebrate the work that has already been done, such as this data visualization project, which will help us raise awareness of the ubiquity of sightings!"<br><br>Not everyone is ready to celebrate, however. Local CEO and vocal anti-alien activist V. Isualize reached out to our reporters to go on record as firmly opposed to any attempts to provide access to this data. "If there are aliens, they certainly would like to be left alone," she stated, before directing us to the Leave Aliens Alone (LAA) community engagement initiative she founded and funds.<br><br>So what do YOU think? Are we alone in the universe? Are aliens trying to contact us, or do they want to be left alone? Dig through the data yourself, and let us know what you see.

            </p>
          </div>
```
To create the table filter, I set up another fluid container with a row nested inside it. Then, I created a div with space for three columns and a dive covering nine columns for the table:
```
    <div class="container-fluid">
        <div class="row">
          <div class="col-md-3">

          </div>
          <div class="col-md-9">

          </div>
        </div>
    </div>
```
Next, within the first div, I added a form tag with a p tag within that had the text “Filter Search”:
```
          <div class="col-md-3">
            <form>
                <p>Filter Search</p>
            </form>
          </div>
```
To add the input box for a date and a button, I created an unordered list with the class “list-group” and two list items: one for the input and one for the button. Each li tag had a class of “list-group item”:
```
            <ul class="list-group">
                <li class="list-group-item">

                </li>
                <li class="list-group-item">
                
                </li>
            </ul>
```
Within the first li tag, I added a label tag to prompt users to input the data and the date input field where users could complete the input:
```
                <li class="list-group-item">
                    <label for="date">Enter Date</label>
                    <input type="text" placeholder="1/10/2010" id="datetime" />
                </li>
```
In the next li tag, I added a button tag with the id defined in my JavaScript code (#filter-btn), the attribute type=“button”, and the attribute class=“btn btn-default”:
```
                <li class="list-group-item">
                    <button id="filter-btn" type="button" class="btn btn-default">Filter Table</button>
                </li>
```
Next, I constructed the nested tags for the table:
```
          <div class="col-md-9">
            <table class="table table-striped">
              <thead>
                <tr>
                  <th></th>
                </tr>
              </thead>
              <tbody></tbody>
            </table>
          </div>
```
Once the table outline was complete, I added the tags for each table header using the keys in the object as the headers:
```
                    <th>Date</th>
                    <th>City</th>
                    <th>State</th>
                    <th>Country</th>
                    <th>Shape</th>
                    <th>Duration</th>
                    <th>Comments</th>
```
After adding the headers, I worked on adding the data to the index.html file. At the bottom of the page, under the last div tag, I added my scripts for the link to a D3.js CDN, the file path to data.js, and the file path to app.js:
```
    <script src="https://cdnjs.cloudflare.com/ajax/libs/d3/4.11.0/d3.js"></script>
    <script src="static/js/data.js"></script>
    <script src="static/js/app.js"></script>
```
With the data added, I worked on customizing the page with CSS. In my style.css file, I applied a light font colour to the webpage using the following syntax:
```
body {

    color: #f7f7f7;
  }
```
In my index.html file, I updated the opening body tag with the following to apply a dark background to the entire page:
```
<body class="bg-dark">
```
To additionally apply a dark background and light lettering to the navbar, I added “navbar-dark bg-dark” to the navbar classes:
```
<nav class="navbar navbar-dark bg-dark navbar-expand-lg">
```
To customize the font style and size of the jumbotron, I added a Bootstrap class called “display-4” to the h1 element inside the jumbotron:
```
    <div class="jumbotron">
        <h1 class="display-4">The Truth is Out There</h1>
    </div>
```
I additionally styled the jumbotron with a background image by adding the following code to my style.css file:
```
.jumbotron {
  background-image: url("../images/nasa.jpg");
  background-size: 100% 100%;
  text-align: center;
}
```
To match the dark theme, I added the class “bg-dark” to the opening form, ul, and li tags. The button element was updated to use a class of “btn-dark” instead of “btn-default”:
```
            <form class="bg-dark">
                <p>Filter Search</p>
                <ul class="list-group bg-dark">
                    <li class="list-group-item bg-dark">
                        <label for="date">Enter Date</label>
                        <input type="text" placeholder="1/10/2010" id="datetime" />
                    </li>
                    <li class="list-group-item bg-dark">
                        <button id="filter-btn" type="button" class="btn btn-dark">Filter Table</button>
                    </li>
                </ul>
            </form>
```

# Challenge
## Overview
### *Purpose*
After reviewing the webpage, Dana requested additional table filters for the city, state, country, and shape to allow users to filter for multiple criteria at the same time and conduct a more in-depth analysis of UFO sightings.

## Filter UFO Sightings on Multiple Criteria
To start, I removed the list element that created the button from the index.html file. Then, I created four more list elements: city, state, country, and shape:
```
                <ul class="list-group bg-dark">
                    <li class="list-group-item bg-dark">
                        <label for="date">Enter Date</label>
                        <input type="text" placeholder="1/10/2010" id="datetime" />
                    </li>
                    <li class="list-group-item bg-dark">
                        <label for="city">Enter City</label>
                        <input type="text" placeholder="benton" id="city" />
                    </li>
                    <li class="list-group-item bg-dark">
                        <label for="state">Enter State</label>
                        <input type="text" placeholder="ar" id="state" />
                    </li>
                    <li class="list-group-item bg-dark">
                        <label for="country">Enter Country</label>
                        <input type="text" placeholder="us" id="country" />
                    </li>
                    <li class="list-group-item bg-dark">
                        <label for="shape">Enter Shape</label>
                        <input type="text" placeholder="circle" id="shape" />
                    </li>
                </ul>
```
In my app.js file, I created an empty “filters” variable to keep track of all the elements that change when a search is entered:
```
// Create a variable to keep track of all the filters as an object.
var filters = {};
```
Located before the buildTable(tableData) function at the end of the starter code, I modified the event listener to detect a change on each input element and call the “updateFilters” function:
```
  // Attach an event to listen for changes to each filter
  d3.selectAll("input").on("change", updateFilters);
```
I replaced the “handleClick” function with the “updateFilters” function and created a variable that saved each element that was changed using d3.select(): 
```
    // Save the element that was changed as a variable.
    let changedElement = d3.select(this);
```
Then, I created a variable that saved the value of the changed element’s property:
```
    // Save the value that was changed as a variable.
    let elementValue = changedElement.property("value");
    console.log(elementValue);
```
An additional variable was created that saved the attribute of the changed element’s id:
```
    // Save the id of the filter that was changed as a variable.
    let filterId = changedElement.attr("id");
    console.log(filterId);
```
Next, I wrote an if-else statement that checked if a value was changed by the user and if so, added the element’s id as the property and the value that was changed to the “filters” variable. If a value was not entered, the element id was cleared from the “filters” variable:
```
    // If a filter value was entered then add that filterId and value
    // to the filters list. Otherwise, clear that filter from the filters object.
    if (elementValue) {
      filters[filterId] = elementValue;
    }
    else {
      delete filters[filterId];
    }
```
Inside the “updateFilters” function, I called the “filterTable” function:
```
    // Call function to apply all filters and rebuild the table
    filterTable();
```
A function called “filterTable” was created to filter the table based on the user input stored in the “filters” variable:
```
  // Use this function to filter the table when data is entered.
  function filterTable() {
```
Within the “filterTable” function, I created a variable for the filtered data that was equal to the variable that builds the table:
```
    // Set the filtered data to the tableData.
    let filteredData = tableData;
```
Then, I created a for loop to loop through the “filters” object and store the data that matched the filter values in the “filteredData” variable:
```
    // Loop through all of the filters and keep any data that
    // matches the filter values
    Object.entries(filters).forEach(([filterId, elementValue]) => {
      filteredData = filteredData.filter(row => row[filterId] === elementValue);
  });
```
Finally, I rebuilt the table with the filtered data by passing the “filteredData” variable in the “buildTable” function:
```
    // Finally, rebuild the table using the filtered data
    buildTable(filteredData);
  };
```

## Results
With the extra filters added, a user is able to filter the data beyond just the date to find UFO sightings in certain cities, states, or countries. The data can additionally be filtered based on the shape of UFO seen. Each filter option can be used alone or in tandem with other filter options, though, input values must be in lower cases. For instance, if a user wanted to know more information on sightings of UFOs that were triangle shaped, they would navigate to “Enter Shape” under the “Filter Search” section towards the bottom of the web page, type “triangle”, and press enter.

![filter_triangle.png](filter_triange.png)

If they wished to view triangle UFO sightings in a particular state, they could additionally type the acronym for their desired state, such as “ca” for California, in the “Enter State” bar and press enter. This would further refine the triangle UFO sightings to those seen in California. 

![filter_ca.png](https://github.com/kcharb7/UFOs/blob/main/static/images/filter_ca.png)

Furthermore, as shown in the image above, there were several triangle UFO sightings in California and so using the “Enter City” input option, the user can further refine the results to show only those in a particular city, such as “el cajon”.

![filter_el_cajon.png](https://github.com/kcharb7/UFOs/blob/main/static/images/filter_el_cajon.png)

The table of UFO sightings can also be filtered based on the country of interest. For example, if a user wishes to see only UFO sightings in Canada, they can type “ca” into the “Enter Country” input box. Doing so returns two UFO sightings.

![filter_canada.png](https://github.com/kcharb7/UFOs/blob/main/static/images/filter_canada.png)


## Summary 
With the search bars created, this webpage provides an interactive environment where UFO enthusiasts can filter and view data on UFO sightings based on their desired interests. However, one big drawback to this webpage is that the data included is for sightings in January 2010 and thus provides limited data for users to view and filter. Thus, one of my recommendations to further improve the web page would be to have more data on UFO sightings in other months within the year 2010, as well as other years, so users can create more definitive conclusions on UFO sightings. Another recommendation would be to add more data from different countries, as the current data was predominantly sightings within the United States, with only two sightings listed within Canada. Having more countries would appeal to more users.
