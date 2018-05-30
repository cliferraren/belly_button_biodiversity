# Belly Button Biodiversity

![Bacteria by filterforge.com](Images/bacteria_by_filterforgedotcom.jpg)

In this assignment, I built an interactive dashboard to explore the [Belly Button Biodiversity DataSet](http://robdunnlab.com/projects/belly-button-biodiversity/).

## Step 1 - Flask API

I used Flask to design an API for the sample dataset and to serve the HTML and JavaScript that are required for my dashboard page. I used also SQLite for my database file and SQLAlchemy inside my Flask application.

* First, I created a template called `index.html` for my dashboard landing page using bootstrap.

* Here is the sample API.

```python
@app.route("/")
    """Return the dashboard homepage."""
```
```python
@app.route('/names')
    """List of sample names.

    Returns a list of sample names in the format
    [
        "BB_940",
        "BB_941",
        "BB_943",
        "BB_944",
        "BB_945",
        "BB_946",
        "BB_947",
        ...
    ]

    """
```
```python
@app.route('/otu')
    """List of OTU descriptions.

    Returns a list of OTU descriptions in the following format

    [
        "Archaea;Euryarchaeota;Halobacteria;Halobacteriales;Halobacteriaceae;Halococcus",
        "Archaea;Euryarchaeota;Halobacteria;Halobacteriales;Halobacteriaceae;Halococcus",
        "Bacteria",
        "Bacteria",
        "Bacteria",
        ...
    ]
    """
```
```python
@app.route('/metadata/<sample>')
    """MetaData for a given sample.

    Args: Sample in the format: `BB_940`

    Returns a json dictionary of sample metadata in the format

    {
        AGE: 24,
        BBTYPE: "I",
        ETHNICITY: "Caucasian",
        GENDER: "F",
        LOCATION: "Beaufort/NC",
        SAMPLEID: 940
    }
    """
```
```python
@app.route('/wfreq/<sample>')
    """Weekly Washing Frequency as a number.

    Args: Sample in the format: `BB_940`

    Returns an integer value for the weekly washing frequency `WFREQ`
    """
```
```python
@app.route('/samples/<sample>')
    """OTU IDs and Sample Values for a given sample.

    Sort your Pandas DataFrame (OTU ID and Sample Value)
    in Descending Order by Sample Value

    Return a list of dictionaries containing sorted lists  for `otu_ids`
    and `sample_values`

    [
        {
            otu_ids: [
                1166,
                2858,
                481,
                ...
            ],
            sample_values: [
                163,
                126,
                113,
                ...
            ]
        }
    ]
    """
```

---

## Step 2 - Plotly.js

I used plotly.js to build interactive charts for my dashboard.

* Use the route `/names` to populate a dropdown select element with the list of sample names.

  * Use `document.getElementById`, `document.createElement` and `append` to populate the create option elements and append them to the dropdown selector.

  * Use the following HTML tag for the dropdown selector

  ```html
  <select id="selDataset" onchange="optionChanged(this.value)"></select>
  ```
  ![dropdown](Images/dropdown.png)

* Create a PIE chart that uses data from your routes `/samples/<sample>` and `/otu` to display the top 10 samples.

  ![PIE Chart](Images/pie_chart.png)

* Create a Bubble Chart that uses data from your routes `/samples/<sample>` and `/otu` to plot the __Sample Value__ vs the __OTU ID__ for the selected sample.

  ![Bubble Chart](Images/bubble_chart.png)

* Display each key/value pair from the metadata JSON object from the route `/metadata/<sample>`

---

## Optional Challenge

To complete, I create a Gauge chart to ccount for values ranging from 0 - 9 using `Plotly.restyle` to update the chart whenever a new sample is selected.

![Weekly Washing Frequency Gauge](Images/gauge.png)

---
