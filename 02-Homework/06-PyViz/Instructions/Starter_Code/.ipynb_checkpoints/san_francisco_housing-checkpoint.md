##### ![pricing-info-by-neighborhood.png](attachment:d49686d1-56fd-4527-a4e2-e8c71d59d661.png)# Housing Rental Analysis for San Francisco

In this challenge, your job is to use your data visualization skills, including aggregation, interactive visualizations, and geospatial analysis, to find properties in the San Francisco market that are viable investment opportunities.

## Instructions

Use the `san_francisco_housing.ipynb` notebook to visualize and analyze the real-estate data.

Note that this assignment requires you to create a visualization by using hvPlot and GeoViews. Additionally, you need to read the `sfo_neighborhoods_census_data.csv` file from the `Resources` folder into the notebook and create the DataFrame that you’ll use in the analysis.

The main task in this Challenge is to visualize and analyze the real-estate data in your Jupyter notebook. Use the `san_francisco_housing.ipynb` notebook to complete the following tasks:

* Calculate and plot the housing units per year.


* Calculate and plot the average prices per square foot.

* Compare the average prices by neighborhood.

* Build an interactive neighborhood map.

* Compose your data story.

### Calculate and Plot the Housing Units per Year

For this part of the assignment, use numerical and visual aggregation to calculate the number of housing units per year, and then visualize the results as a bar chart. To do so, complete the following steps:

1. Use the `groupby` function to group the data by year. Aggregate the results by the `mean` of the groups.

2. Use the `hvplot` function to plot the `housing_units_by_year` DataFrame as a bar chart. Make the x-axis represent the `year` and the y-axis represent the `housing_units`.

3. Style and format the line plot to ensure a professionally styled visualization.

4. Note that your resulting plot should appear similar to the following image:

![A screenshot depicts an example of the resulting bar chart.](Images/zoomed-housing-units-by-year.png)

5. Answer the following question:

    * What’s the overall trend in housing units over the period that you’re analyzing?

### Calculate and Plot the Average Sale Prices per Square Foot

For this part of the assignment, use numerical and visual aggregation to calculate the average prices per square foot, and then visualize the results as a bar chart. To do so, complete the following steps:

1. Group the data by year, and then average the results. What’s the lowest gross rent that’s reported for the years that the DataFrame includes?

2. Create a new DataFrame named `prices_square_foot_by_year` by filtering out the “housing_units” column. The new DataFrame should include the averages per year for only the sale price per square foot and the gross rent.

3. Use hvPlot to plot the `prices_square_foot_by_year` DataFrame as a line plot.

    > **Hint** This single plot will include lines for both `sale_price_sqr_foot` and `gross_rent`.

4. Style and format the line plot to ensure a professionally styled visualization.

5. Note that your resulting plot should appear similar to the following image:

![A screenshot depicts an example of the resulting plot.](Images/avg-sale-px-sq-foot-gross-rent.png)

6. Use both the `prices_square_foot_by_year` DataFrame and interactive plots to answer the following questions:

    * Did any year experience a drop in the average sale price per square foot compared to the previous year?

    * If so, did the gross rent increase or decrease during that year?

### Compare the Average Sale Prices by Neighborhood

For this part of the assignment, use interactive visualizations and widgets to explore the average sale price per square foot by neighborhood. To do so, complete the following steps:

1. Create a new DataFrame that groups the original DataFrame by year and neighborhood. Aggregate the results by the `mean` of the groups.

2. Filter out the “housing_units” column to create a DataFrame that includes only the `sale_price_sqr_foot` and `gross_rent` averages per year.

3. Create an interactive line plot with hvPlot that visualizes both `sale_price_sqr_foot` and `gross_rent`. Set the x-axis parameter to the year (`x="year"`). Use the `groupby` parameter to create an interactive widget for `neighborhood`.

4. Style and format the line plot to ensure a professionally styled visualization.

5. Note that your resulting plot should appear similar to the following image:

![A screenshot depicts an example of the resulting plot.](Images/pricing-info-by-neighborhood.png)

6. Use the interactive visualization to answer the following question:

    * For the Anza Vista neighborhood, is the average sale price per square foot for 2016 more or less than the price that’s listed for 2012? 

### Build an Interactive Neighborhood Map

For this part of the assignment, explore the geospatial relationships in the data by using interactive visualizations with hvPlot and GeoViews. To build your map, use the `sfo_data_df` DataFrame (created during the initial import), which includes the neighborhood location data with the average prices. To do all this, complete the following steps:

1. Read the `neighborhood_coordinates.csv` file from the `Resources` folder into the notebook, and create a DataFrame named `neighborhood_locations_df`. Be sure to set the `index_col` of the DataFrame as “Neighborhood”.

2. Using the original `sfo_data_df` Dataframe, create a DataFrame named `all_neighborhood_info_df` that groups the data by neighborhood. Aggregate the results by the `mean` of the group.

3. Review the two code cells that concatenate the `neighborhood_locations_df` DataFrame with the `all_neighborhood_info_df` DataFrame. Note that the first cell uses the [Pandas concat function](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.concat.html) to create a DataFrame named `all_neighborhoods_df`. The second cell cleans the data and sets the “Neighborhood” column. Be sure to run these cells to create the `all_neighborhoods_df` DataFrame, which you’ll need to create the geospatial visualization.

4. Using hvPlot with GeoViews enabled, create a `points` plot for the `all_neighborhoods_df` DataFrame. Be sure to do the following:

    * Set the `geo` parameter to True.
    * Set the `size` parameter to “sale_price_sqr_foot”.
    * Set the `color` parameter to “gross_rent”.
    * Set the `frame_width` parameter to 700.
    * Set the `frame_height` parameter to 500.
    * Include a descriptive title.

Note that your resulting plot should appear similar to the following image:

![A screenshot depicts an example of a scatter plot created with hvPlot and GeoViews.](Images/6-4-geoviews-plot.png)

5. Use the interactive map to answer the following question:

    * Which neighborhood has the highest gross rent, and which has the highest sale price per square foot?

### Compose Your Data Story

Based on the visualizations that you created, answer the following questions:

* How does the trend in rental income growth compare to the trend in sales prices? Does this same trend hold true for all the neighborhoods across San Francisco?

* What insights can you share with your company about the potential one-click, buy-and-rent strategy that they're pursuing? Do neighborhoods exist that you would suggest for investment, and why?


```python
# Import the required libraries and dependencies
import pandas as pd
import hvplot.pandas
from pathlib import Path
```









## Import the data 


```python
housing_per_year_df = Path("Starter_Code/Resources/housing_per_year.csv")
#housing_per_year_df = pd.read_csv(housing_per_year, index_col="year", parse_dates=True, infer_datetime_format=True)
# Review the first and last five rows of the DataFrame
#sfo_data_dataframe.head(1)
#housing_data_df.tail()
```


```python
# Using the read_csv function and Path module, create a DataFrame 
# by importing the sfo_neighborhoods_census_data.csv file from the Resources folder
sfo_data_df = Path("Resources/sfo_neighborhoods_census_data.csv")
sfo_dataframe = pd.read_csv(sfo_data_df, index_col="year", parse_dates=True, infer_datetime_format=True)
# Review the first and last five rows of the DataFrame
#sfo_data_dataframe.head(1)
sfo_dataframe.tail()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>neighborhood</th>
      <th>sale_price_sqr_foot</th>
      <th>housing_units</th>
      <th>gross_rent</th>
    </tr>
    <tr>
      <th>year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2016-01-01</th>
      <td>Telegraph Hill</td>
      <td>903.049771</td>
      <td>384242</td>
      <td>4390</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>Twin Peaks</td>
      <td>970.085470</td>
      <td>384242</td>
      <td>4390</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>Van Ness/ Civic Center</td>
      <td>552.602567</td>
      <td>384242</td>
      <td>4390</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>Visitacion Valley</td>
      <td>328.319007</td>
      <td>384242</td>
      <td>4390</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>Westwood Park</td>
      <td>631.195426</td>
      <td>384242</td>
      <td>4390</td>
    </tr>
  </tbody>
</table>
</div>




```python

```

---

## Calculate and Plot the Housing Units per Year

For this part of the assignment, use numerical and visual aggregation to calculate the number of housing units per year, and then visualize the results as a bar chart. To do so, complete the following steps:

1. Use the `groupby` function to group the data by year. Aggregate the results by the `mean` of the groups.

2. Use the `hvplot` function to plot the `housing_units_by_year` DataFrame as a bar chart. Make the x-axis represent the `year` and the y-axis represent the `housing_units`.

3. Style and format the line plot to ensure a professionally styled visualization.

4. Note that your resulting plot should appear similar to the following image:

![A screenshot depicts an example of the resulting bar chart.](Images/zoomed-housing-units-by-year.png)

5. Answer the following question:

    * What’s the overall trend in housing units over the period that you’re analyzing?



### Step 1: Use the `groupby` function to group the data by year. Aggregate the results by the `mean` of the groups.


```python
#Create a numerical aggregation that groups the data by the year and then averages the results.
housing_units_by_year = sfo_dataframe.groupby('year').mean()

 
    


# Review the DataFrame
housing_units_by_year 
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sale_price_sqr_foot</th>
      <th>housing_units</th>
      <th>gross_rent</th>
    </tr>
    <tr>
      <th>year</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2010-01-01</th>
      <td>369.344353</td>
      <td>372560.0</td>
      <td>1239.0</td>
    </tr>
    <tr>
      <th>2011-01-01</th>
      <td>341.903429</td>
      <td>374507.0</td>
      <td>1530.0</td>
    </tr>
    <tr>
      <th>2012-01-01</th>
      <td>399.389968</td>
      <td>376454.0</td>
      <td>2324.0</td>
    </tr>
    <tr>
      <th>2013-01-01</th>
      <td>483.600304</td>
      <td>378401.0</td>
      <td>2971.0</td>
    </tr>
    <tr>
      <th>2014-01-01</th>
      <td>556.277273</td>
      <td>380348.0</td>
      <td>3528.0</td>
    </tr>
    <tr>
      <th>2015-01-01</th>
      <td>632.540352</td>
      <td>382295.0</td>
      <td>3739.0</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>697.643709</td>
      <td>384242.0</td>
      <td>4390.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Using the read_csv function and Path module, create a DataFrame 
# by importing the sfo_neighborhoods_census_data.csv file from the Resources folder
sfo_data_df = Path("Resources/sfo_neighborhoods_census_data.csv")
sfo_dataframe = pd.read_csv(sfo_data_df, index_col="year", parse_dates=True, infer_datetime_format=True)
# Review the first and last five rows of the DataFrame
sfo_dataframe.head(10)


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>neighborhood</th>
      <th>sale_price_sqr_foot</th>
      <th>housing_units</th>
      <th>gross_rent</th>
    </tr>
    <tr>
      <th>year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2010-01-01</th>
      <td>Alamo Square</td>
      <td>291.182945</td>
      <td>372560</td>
      <td>1239</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>Anza Vista</td>
      <td>267.932583</td>
      <td>372560</td>
      <td>1239</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>Bayview</td>
      <td>170.098665</td>
      <td>372560</td>
      <td>1239</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>Buena Vista Park</td>
      <td>347.394919</td>
      <td>372560</td>
      <td>1239</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>Central Richmond</td>
      <td>319.027623</td>
      <td>372560</td>
      <td>1239</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>Central Sunset</td>
      <td>418.172493</td>
      <td>372560</td>
      <td>1239</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>Corona Heights</td>
      <td>369.359338</td>
      <td>372560</td>
      <td>1239</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>Cow Hollow</td>
      <td>569.379968</td>
      <td>372560</td>
      <td>1239</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>Croker Amazon</td>
      <td>165.645730</td>
      <td>372560</td>
      <td>1239</td>
    </tr>
    <tr>
      <th>2010-01-01</th>
      <td>Diamond Heights</td>
      <td>456.930822</td>
      <td>372560</td>
      <td>1239</td>
    </tr>
  </tbody>
</table>
</div>




```python
sfo_dataframe.tail(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>neighborhood</th>
      <th>sale_price_sqr_foot</th>
      <th>housing_units</th>
      <th>gross_rent</th>
    </tr>
    <tr>
      <th>year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2016-01-01</th>
      <td>Telegraph Hill</td>
      <td>903.049771</td>
      <td>384242</td>
      <td>4390</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>Twin Peaks</td>
      <td>970.085470</td>
      <td>384242</td>
      <td>4390</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>Van Ness/ Civic Center</td>
      <td>552.602567</td>
      <td>384242</td>
      <td>4390</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>Visitacion Valley</td>
      <td>328.319007</td>
      <td>384242</td>
      <td>4390</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>Westwood Park</td>
      <td>631.195426</td>
      <td>384242</td>
      <td>4390</td>
    </tr>
  </tbody>
</table>
</div>




```python
### Step 2: Use the `hvplot` function to plot the `housing_units_by_year` DataFrame as a bar chart. Make the x-axis represent the `year` and the y-axis represent the `housing_units`.
    
housing_units_by_year.hvplot.bar(label='housing units by year',
     x='year',
     y='housing_units')
  
                        


```






<div id='1002'>





  <div class="bk-root" id="edc11058-587a-4d28-8b91-205239a01bfa" data-root-id="1002"></div>
</div>
<script type="application/javascript">(function(root) {
  function embed_document(root) {
    var docs_json = {"1b873a45-8cfe-454b-bb9a-538d8a3d82dc":{"defs":[{"extends":null,"module":null,"name":"ReactiveHTML1","overrides":[],"properties":[]},{"extends":null,"module":null,"name":"FlexBox1","overrides":[],"properties":[{"default":"flex-start","kind":null,"name":"align_content"},{"default":"flex-start","kind":null,"name":"align_items"},{"default":"row","kind":null,"name":"flex_direction"},{"default":"wrap","kind":null,"name":"flex_wrap"},{"default":"flex-start","kind":null,"name":"justify_content"}]},{"extends":null,"module":null,"name":"TemplateActions1","overrides":[],"properties":[{"default":0,"kind":null,"name":"open_modal"},{"default":0,"kind":null,"name":"close_modal"}]},{"extends":null,"module":null,"name":"MaterialTemplateActions1","overrides":[],"properties":[{"default":0,"kind":null,"name":"open_modal"},{"default":0,"kind":null,"name":"close_modal"}]}],"roots":{"references":[{"attributes":{},"id":"1014","type":"LinearScale"},{"attributes":{"margin":[5,5,5,5],"name":"HSpacer01633","sizing_mode":"stretch_width"},"id":"1071","type":"Spacer"},{"attributes":{},"id":"1017","type":"CategoricalTicker"},{"attributes":{},"id":"1047","type":"AllLabels"},{"attributes":{"axis_label":"housing_units","coordinates":null,"formatter":{"id":"1049"},"group":null,"major_label_policy":{"id":"1050"},"ticker":{"id":"1020"}},"id":"1019","type":"LinearAxis"},{"attributes":{"axis":{"id":"1019"},"coordinates":null,"dimension":1,"grid_line_color":null,"group":null,"ticker":null},"id":"1022","type":"Grid"},{"attributes":{"fill_alpha":{"value":0.1},"fill_color":{"value":"#30a2da"},"hatch_alpha":{"value":0.1},"hatch_color":{"value":"#30a2da"},"line_alpha":{"value":0.1},"top":{"field":"housing_units"},"width":{"value":0.8},"x":{"field":"year"}},"id":"1040","type":"VBar"},{"attributes":{},"id":"1046","type":"CategoricalTickFormatter"},{"attributes":{},"id":"1012","type":"CategoricalScale"},{"attributes":{"bottom":{"value":0},"fill_alpha":{"value":1.0},"fill_color":{"value":"#30a2da"},"hatch_alpha":{"value":1.0},"hatch_color":{"value":"#30a2da"},"hatch_scale":{"value":12.0},"hatch_weight":{"value":1.0},"line_alpha":{"value":1.0},"line_cap":{"value":"butt"},"line_color":{"value":"black"},"line_dash":{"value":[]},"line_dash_offset":{"value":0},"line_join":{"value":"bevel"},"line_width":{"value":1},"top":{"field":"housing_units"},"width":{"value":0.8},"x":{"field":"year"}},"id":"1044","type":"VBar"},{"attributes":{"end":385410.2,"reset_end":385410.2,"reset_start":0.0,"tags":[[["housing_units","housing_units",null]]]},"id":"1005","type":"Range1d"},{"attributes":{"source":{"id":"1036"}},"id":"1043","type":"CDSView"},{"attributes":{},"id":"1058","type":"UnionRenderers"},{"attributes":{"tools":[{"id":"1006"},{"id":"1023"},{"id":"1024"},{"id":"1025"},{"id":"1026"},{"id":"1027"}]},"id":"1029","type":"Toolbar"},{"attributes":{"factors":["2010-01-01 00:00:00","2011-01-01 00:00:00","2012-01-01 00:00:00","2013-01-01 00:00:00","2014-01-01 00:00:00","2015-01-01 00:00:00","2016-01-01 00:00:00"],"tags":[[["year","year",null]]]},"id":"1004","type":"FactorRange"},{"attributes":{},"id":"1023","type":"SaveTool"},{"attributes":{},"id":"1024","type":"PanTool"},{"attributes":{"margin":[5,5,5,5],"name":"HSpacer01632","sizing_mode":"stretch_width"},"id":"1003","type":"Spacer"},{"attributes":{"callback":null,"renderers":[{"id":"1042"}],"tags":["hv_created"],"tooltips":[["year","@{year}"],["housing_units","@{housing_units}"]]},"id":"1006","type":"HoverTool"},{"attributes":{},"id":"1027","type":"ResetTool"},{"attributes":{},"id":"1049","type":"BasicTickFormatter"},{"attributes":{},"id":"1025","type":"WheelZoomTool"},{"attributes":{"fill_alpha":{"value":0.2},"fill_color":{"value":"#30a2da"},"hatch_alpha":{"value":0.2},"hatch_color":{"value":"#30a2da"},"line_alpha":{"value":0.2},"top":{"field":"housing_units"},"width":{"value":0.8},"x":{"field":"year"}},"id":"1041","type":"VBar"},{"attributes":{"children":[{"id":"1003"},{"id":"1007"},{"id":"1071"}],"margin":[0,0,0,0],"name":"Row01628","tags":["embedded"]},"id":"1002","type":"Row"},{"attributes":{"overlay":{"id":"1028"}},"id":"1026","type":"BoxZoomTool"},{"attributes":{},"id":"1020","type":"BasicTicker"},{"attributes":{},"id":"1050","type":"AllLabels"},{"attributes":{"axis_label":"year","coordinates":null,"formatter":{"id":"1046"},"group":null,"major_label_policy":{"id":"1047"},"ticker":{"id":"1017"}},"id":"1016","type":"CategoricalAxis"},{"attributes":{"axis":{"id":"1016"},"coordinates":null,"grid_line_color":null,"group":null,"ticker":null},"id":"1018","type":"Grid"},{"attributes":{"below":[{"id":"1016"}],"center":[{"id":"1018"},{"id":"1022"}],"height":300,"left":[{"id":"1019"}],"margin":[5,5,5,5],"min_border_bottom":10,"min_border_left":10,"min_border_right":10,"min_border_top":10,"renderers":[{"id":"1042"}],"sizing_mode":"fixed","title":{"id":"1008"},"toolbar":{"id":"1029"},"width":700,"x_range":{"id":"1004"},"x_scale":{"id":"1012"},"y_range":{"id":"1005"},"y_scale":{"id":"1014"}},"id":"1007","subtype":"Figure","type":"Plot"},{"attributes":{"bottom_units":"screen","coordinates":null,"fill_alpha":0.5,"fill_color":"lightgrey","group":null,"left_units":"screen","level":"overlay","line_alpha":1.0,"line_color":"black","line_dash":[4,4],"line_width":2,"right_units":"screen","syncable":false,"top_units":"screen"},"id":"1028","type":"BoxAnnotation"},{"attributes":{"coordinates":null,"group":null,"text":"housing units by year","text_color":"black","text_font_size":"12pt"},"id":"1008","type":"Title"},{"attributes":{"coordinates":null,"data_source":{"id":"1036"},"glyph":{"id":"1039"},"group":null,"hover_glyph":null,"muted_glyph":{"id":"1041"},"nonselection_glyph":{"id":"1040"},"selection_glyph":{"id":"1044"},"view":{"id":"1043"}},"id":"1042","type":"GlyphRenderer"},{"attributes":{},"id":"1037","type":"Selection"},{"attributes":{"data":{"housing_units":{"__ndarray__":"AAAAAEC9FkEAAAAArNsWQQAAAAAY+hZBAAAAAIQYF0EAAAAA8DYXQQAAAABcVRdBAAAAAMhzF0E=","dtype":"float64","order":"little","shape":[7]},"year":["2010-01-01 00:00:00","2011-01-01 00:00:00","2012-01-01 00:00:00","2013-01-01 00:00:00","2014-01-01 00:00:00","2015-01-01 00:00:00","2016-01-01 00:00:00"]},"selected":{"id":"1037"},"selection_policy":{"id":"1058"}},"id":"1036","type":"ColumnDataSource"},{"attributes":{"fill_color":{"value":"#30a2da"},"hatch_color":{"value":"#30a2da"},"top":{"field":"housing_units"},"width":{"value":0.8},"x":{"field":"year"}},"id":"1039","type":"VBar"}],"root_ids":["1002"]},"title":"Bokeh Application","version":"2.4.1"}};
    var render_items = [{"docid":"1b873a45-8cfe-454b-bb9a-538d8a3d82dc","root_ids":["1002"],"roots":{"1002":"edc11058-587a-4d28-8b91-205239a01bfa"}}];
    root.Bokeh.embed.embed_items_notebook(docs_json, render_items);
  }
  if (root.Bokeh !== undefined && root.Bokeh.Panel !== undefined) {
    embed_document(root);
  } else {
    var attempts = 0;
    var timer = setInterval(function(root) {
      if (root.Bokeh !== undefined && root.Bokeh.Panel !== undefined) {
        clearInterval(timer);
        embed_document(root);
      } else if (document.readyState == "complete") {
        attempts++;
        if (attempts > 200) {
          clearInterval(timer);
          console.log("Bokeh: ERROR: Unable to run BokehJS code because BokehJS library is missing");
        }
      }
    }, 25, root)
  }
})(window);</script>




```python
### Step 3: Style and format the line plot to ensure a professionally styled visualization.

housing_units_by_year.hvplot.line(label='housing units by year',
     x='year',
     y='housing_units',
).opts(
    yformatter='%.0f',
    line_color='blue',
    hover_line_color='yellow'
    
)
```






<div id='1123'>





  <div class="bk-root" id="a029f3eb-ae8f-4c82-a0e9-90e68b939d30" data-root-id="1123"></div>
</div>
<script type="application/javascript">(function(root) {
  function embed_document(root) {
    var docs_json = {"5cf450b3-f8f2-4934-88ac-cfd53e7400e0":{"defs":[{"extends":null,"module":null,"name":"ReactiveHTML1","overrides":[],"properties":[]},{"extends":null,"module":null,"name":"FlexBox1","overrides":[],"properties":[{"default":"flex-start","kind":null,"name":"align_content"},{"default":"flex-start","kind":null,"name":"align_items"},{"default":"row","kind":null,"name":"flex_direction"},{"default":"wrap","kind":null,"name":"flex_wrap"},{"default":"flex-start","kind":null,"name":"justify_content"}]},{"extends":null,"module":null,"name":"TemplateActions1","overrides":[],"properties":[{"default":0,"kind":null,"name":"open_modal"},{"default":0,"kind":null,"name":"close_modal"}]},{"extends":null,"module":null,"name":"MaterialTemplateActions1","overrides":[],"properties":[{"default":0,"kind":null,"name":"open_modal"},{"default":0,"kind":null,"name":"close_modal"}]}],"roots":{"references":[{"attributes":{"axis":{"id":"1141"},"coordinates":null,"dimension":1,"grid_line_color":null,"group":null,"ticker":null},"id":"1144","type":"Grid"},{"attributes":{},"id":"1142","type":"BasicTicker"},{"attributes":{},"id":"1170","type":"DatetimeTickFormatter"},{"attributes":{"months":[0,1,2,3,4,5,6,7,8,9,10,11]},"id":"1193","type":"MonthsTicker"},{"attributes":{"months":[0,2,4,6,8,10]},"id":"1194","type":"MonthsTicker"},{"attributes":{"line_color":"yellow","line_width":2,"x":{"field":"year"},"y":{"field":"housing_units"}},"id":"1163","type":"Line"},{"attributes":{},"id":"1174","type":"AllLabels"},{"attributes":{},"id":"1171","type":"AllLabels"},{"attributes":{"line_color":"blue","line_width":2,"x":{"field":"year"},"y":{"field":"housing_units"}},"id":"1161","type":"Line"},{"attributes":{"line_alpha":0.2,"line_color":"blue","line_width":2,"x":{"field":"year"},"y":{"field":"housing_units"}},"id":"1164","type":"Line"},{"attributes":{"months":[0,6]},"id":"1196","type":"MonthsTicker"},{"attributes":{"line_alpha":0.1,"line_color":"blue","line_width":2,"x":{"field":"year"},"y":{"field":"housing_units"}},"id":"1162","type":"Line"},{"attributes":{"format":"%.0f"},"id":"1168","type":"PrintfTickFormatter"},{"attributes":{"line_color":"blue","line_width":2,"x":{"field":"year"},"y":{"field":"housing_units"}},"id":"1167","type":"Line"},{"attributes":{"end":1451606400000.0,"reset_end":1451606400000.0,"reset_start":1262304000000.0,"start":1262304000000.0,"tags":[[["year","year",null]]]},"id":"1125","type":"Range1d"},{"attributes":{"tools":[{"id":"1127"},{"id":"1145"},{"id":"1146"},{"id":"1147"},{"id":"1148"},{"id":"1149"}]},"id":"1151","type":"Toolbar"},{"attributes":{},"id":"1133","type":"LinearScale"},{"attributes":{"callback":null,"formatters":{"@{year}":"datetime"},"renderers":[{"id":"1165"}],"tags":["hv_created"],"tooltips":[["year","@{year}{%F %T}"],["housing_units","@{housing_units}"]]},"id":"1127","type":"HoverTool"},{"attributes":{"bottom_units":"screen","coordinates":null,"fill_alpha":0.5,"fill_color":"lightgrey","group":null,"left_units":"screen","level":"overlay","line_alpha":1.0,"line_color":"black","line_dash":[4,4],"line_width":2,"right_units":"screen","syncable":false,"top_units":"screen"},"id":"1150","type":"BoxAnnotation"},{"attributes":{"months":[0,4,8]},"id":"1195","type":"MonthsTicker"},{"attributes":{"end":385410.2,"reset_end":385410.2,"reset_start":371391.8,"start":371391.8,"tags":[[["housing_units","housing_units",null]]]},"id":"1126","type":"Range1d"},{"attributes":{},"id":"1145","type":"SaveTool"},{"attributes":{},"id":"1146","type":"PanTool"},{"attributes":{"days":[1,15]},"id":"1192","type":"DaysTicker"},{"attributes":{},"id":"1197","type":"YearsTicker"},{"attributes":{"margin":[5,5,5,5],"name":"HSpacer01828","sizing_mode":"stretch_width"},"id":"1219","type":"Spacer"},{"attributes":{"coordinates":null,"data_source":{"id":"1158"},"glyph":{"id":"1161"},"group":null,"hover_glyph":{"id":"1163"},"muted_glyph":{"id":"1164"},"nonselection_glyph":{"id":"1162"},"selection_glyph":{"id":"1167"},"view":{"id":"1166"}},"id":"1165","type":"GlyphRenderer"},{"attributes":{},"id":"1149","type":"ResetTool"},{"attributes":{},"id":"1147","type":"WheelZoomTool"},{"attributes":{"days":[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31]},"id":"1189","type":"DaysTicker"},{"attributes":{},"id":"1183","type":"UnionRenderers"},{"attributes":{"overlay":{"id":"1150"}},"id":"1148","type":"BoxZoomTool"},{"attributes":{"base":60,"mantissas":[1,2,5,10,15,20,30],"max_interval":1800000.0,"min_interval":1000.0,"num_minor_ticks":0},"id":"1187","type":"AdaptiveTicker"},{"attributes":{"coordinates":null,"group":null,"text":"housing units by year","text_color":"black","text_font_size":"12pt"},"id":"1129","type":"Title"},{"attributes":{},"id":"1159","type":"Selection"},{"attributes":{"axis_label":"year","coordinates":null,"formatter":{"id":"1170"},"group":null,"major_label_policy":{"id":"1171"},"ticker":{"id":"1138"}},"id":"1137","type":"DatetimeAxis"},{"attributes":{"mantissas":[1,2,5],"max_interval":500.0,"num_minor_ticks":0},"id":"1186","type":"AdaptiveTicker"},{"attributes":{"children":[{"id":"1124"},{"id":"1128"},{"id":"1219"}],"margin":[0,0,0,0],"name":"Row01823","tags":["embedded"]},"id":"1123","type":"Row"},{"attributes":{"base":24,"mantissas":[1,2,4,6,8,12],"max_interval":43200000.0,"min_interval":3600000.0,"num_minor_ticks":0},"id":"1188","type":"AdaptiveTicker"},{"attributes":{"num_minor_ticks":5,"tickers":[{"id":"1186"},{"id":"1187"},{"id":"1188"},{"id":"1189"},{"id":"1190"},{"id":"1191"},{"id":"1192"},{"id":"1193"},{"id":"1194"},{"id":"1195"},{"id":"1196"},{"id":"1197"}]},"id":"1138","type":"DatetimeTicker"},{"attributes":{"days":[1,4,7,10,13,16,19,22,25,28]},"id":"1190","type":"DaysTicker"},{"attributes":{},"id":"1135","type":"LinearScale"},{"attributes":{"source":{"id":"1158"}},"id":"1166","type":"CDSView"},{"attributes":{"axis_label":"housing_units","coordinates":null,"formatter":{"id":"1168"},"group":null,"major_label_policy":{"id":"1174"},"ticker":{"id":"1142"}},"id":"1141","type":"LinearAxis"},{"attributes":{"axis":{"id":"1137"},"coordinates":null,"grid_line_color":null,"group":null,"ticker":null},"id":"1140","type":"Grid"},{"attributes":{"below":[{"id":"1137"}],"center":[{"id":"1140"},{"id":"1144"}],"height":300,"left":[{"id":"1141"}],"margin":[5,5,5,5],"min_border_bottom":10,"min_border_left":10,"min_border_right":10,"min_border_top":10,"renderers":[{"id":"1165"}],"sizing_mode":"fixed","title":{"id":"1129"},"toolbar":{"id":"1151"},"width":700,"x_range":{"id":"1125"},"x_scale":{"id":"1133"},"y_range":{"id":"1126"},"y_scale":{"id":"1135"}},"id":"1128","subtype":"Figure","type":"Plot"},{"attributes":{"days":[1,8,15,22]},"id":"1191","type":"DaysTicker"},{"attributes":{"margin":[5,5,5,5],"name":"HSpacer01827","sizing_mode":"stretch_width"},"id":"1124","type":"Spacer"},{"attributes":{"data":{"housing_units":{"__ndarray__":"AAAAAEC9FkEAAAAArNsWQQAAAAAY+hZBAAAAAIQYF0EAAAAA8DYXQQAAAABcVRdBAAAAAMhzF0E=","dtype":"float64","order":"little","shape":[7]},"year":{"__ndarray__":"AACA53JeckIAAED67dNyQgAAAA1pSXNCAACAhTa/c0IAAECYsTR0QgAAAKssqnRCAADAvacfdUI=","dtype":"float64","order":"little","shape":[7]}},"selected":{"id":"1159"},"selection_policy":{"id":"1183"}},"id":"1158","type":"ColumnDataSource"}],"root_ids":["1123"]},"title":"Bokeh Application","version":"2.4.1"}};
    var render_items = [{"docid":"5cf450b3-f8f2-4934-88ac-cfd53e7400e0","root_ids":["1123"],"roots":{"1123":"a029f3eb-ae8f-4c82-a0e9-90e68b939d30"}}];
    root.Bokeh.embed.embed_items_notebook(docs_json, render_items);
  }
  if (root.Bokeh !== undefined && root.Bokeh.Panel !== undefined) {
    embed_document(root);
  } else {
    var attempts = 0;
    var timer = setInterval(function(root) {
      if (root.Bokeh !== undefined && root.Bokeh.Panel !== undefined) {
        clearInterval(timer);
        embed_document(root);
      } else if (document.readyState == "complete") {
        attempts++;
        if (attempts > 200) {
          clearInterval(timer);
          console.log("Bokeh: ERROR: Unable to run BokehJS code because BokehJS library is missing");
        }
      }
    }, 25, root)
  }
})(window);</script>




```python
# Create a visual aggregation explore the housing units by year
housing_units_by_year.groupby(['year']).mean().hvplot()
```






<div id='1326'>





  <div class="bk-root" id="01c090cd-c57c-457f-8d5e-1016a13f8f67" data-root-id="1326"></div>
</div>
<script type="application/javascript">(function(root) {
  function embed_document(root) {
    var docs_json = {"bfeed9d5-8222-4b4c-814d-10116da30916":{"defs":[{"extends":null,"module":null,"name":"ReactiveHTML1","overrides":[],"properties":[]},{"extends":null,"module":null,"name":"FlexBox1","overrides":[],"properties":[{"default":"flex-start","kind":null,"name":"align_content"},{"default":"flex-start","kind":null,"name":"align_items"},{"default":"row","kind":null,"name":"flex_direction"},{"default":"wrap","kind":null,"name":"flex_wrap"},{"default":"flex-start","kind":null,"name":"justify_content"}]},{"extends":null,"module":null,"name":"TemplateActions1","overrides":[],"properties":[{"default":0,"kind":null,"name":"open_modal"},{"default":0,"kind":null,"name":"close_modal"}]},{"extends":null,"module":null,"name":"MaterialTemplateActions1","overrides":[],"properties":[{"default":0,"kind":null,"name":"open_modal"},{"default":0,"kind":null,"name":"close_modal"}]}],"roots":{"references":[{"attributes":{},"id":"1352","type":"WheelZoomTool"},{"attributes":{},"id":"1354","type":"ResetTool"},{"attributes":{"overlay":{"id":"1355"}},"id":"1353","type":"BoxZoomTool"},{"attributes":{"callback":null,"formatters":{"@{year}":"datetime"},"renderers":[{"id":"1375"},{"id":"1408"},{"id":"1442"}],"tags":["hv_created"],"tooltips":[["Variable","@{Variable}"],["year","@{year}{%F %T}"],["value","@{value}"]]},"id":"1330","type":"HoverTool"},{"attributes":{"coordinates":null,"group":null,"text_color":"black","text_font_size":"12pt"},"id":"1334","type":"Title"},{"attributes":{"coordinates":null,"data_source":{"id":"1436"},"glyph":{"id":"1439"},"group":null,"hover_glyph":null,"muted_glyph":{"id":"1441"},"nonselection_glyph":{"id":"1440"},"selection_glyph":{"id":"1471"},"view":{"id":"1443"}},"id":"1442","type":"GlyphRenderer"},{"attributes":{"line_color":"#30a2da","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"1401","type":"Line"},{"attributes":{"coordinates":null,"data_source":{"id":"1402"},"glyph":{"id":"1405"},"group":null,"hover_glyph":null,"muted_glyph":{"id":"1407"},"nonselection_glyph":{"id":"1406"},"selection_glyph":{"id":"1435"},"view":{"id":"1409"}},"id":"1408","type":"GlyphRenderer"},{"attributes":{},"id":"1455","type":"UnionRenderers"},{"attributes":{},"id":"1403","type":"Selection"},{"attributes":{"days":[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31]},"id":"1390","type":"DaysTicker"},{"attributes":{"end":1451606400000.0,"reset_end":1451606400000.0,"reset_start":1262304000000.0,"start":1262304000000.0,"tags":[[["year","year",null]]]},"id":"1328","type":"Range1d"},{"attributes":{"tools":[{"id":"1330"},{"id":"1350"},{"id":"1351"},{"id":"1352"},{"id":"1353"},{"id":"1354"}]},"id":"1356","type":"Toolbar"},{"attributes":{},"id":"1419","type":"UnionRenderers"},{"attributes":{"months":[0,1,2,3,4,5,6,7,8,9,10,11]},"id":"1394","type":"MonthsTicker"},{"attributes":{"base":24,"mantissas":[1,2,4,6,8,12],"max_interval":43200000.0,"min_interval":3600000.0,"num_minor_ticks":0},"id":"1389","type":"AdaptiveTicker"},{"attributes":{"bottom_units":"screen","coordinates":null,"fill_alpha":0.5,"fill_color":"lightgrey","group":null,"left_units":"screen","level":"overlay","line_alpha":1.0,"line_color":"black","line_dash":[4,4],"line_width":2,"right_units":"screen","syncable":false,"top_units":"screen"},"id":"1355","type":"BoxAnnotation"},{"attributes":{"line_color":"#fc4f30","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"1405","type":"Line"},{"attributes":{"line_color":"#e5ae38","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"1439","type":"Line"},{"attributes":{"source":{"id":"1402"}},"id":"1409","type":"CDSView"},{"attributes":{"source":{"id":"1436"}},"id":"1443","type":"CDSView"},{"attributes":{"line_alpha":0.2,"line_color":"#fc4f30","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"1407","type":"Line"},{"attributes":{"below":[{"id":"1342"}],"center":[{"id":"1345"},{"id":"1349"}],"height":300,"left":[{"id":"1346"}],"margin":[5,5,5,5],"min_border_bottom":10,"min_border_left":10,"min_border_right":10,"min_border_top":10,"renderers":[{"id":"1375"},{"id":"1408"},{"id":"1442"}],"right":[{"id":"1399"}],"sizing_mode":"fixed","title":{"id":"1334"},"toolbar":{"id":"1356"},"width":700,"x_range":{"id":"1328"},"x_scale":{"id":"1338"},"y_range":{"id":"1329"},"y_scale":{"id":"1340"}},"id":"1333","subtype":"Figure","type":"Plot"},{"attributes":{"label":{"value":"gross_rent"},"renderers":[{"id":"1442"}]},"id":"1470","type":"LegendItem"},{"attributes":{"line_alpha":0.2,"line_color":"#e5ae38","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"1441","type":"Line"},{"attributes":{},"id":"1370","type":"Selection"},{"attributes":{"days":[1,4,7,10,13,16,19,22,25,28]},"id":"1391","type":"DaysTicker"},{"attributes":{},"id":"1367","type":"BasicTickFormatter"},{"attributes":{},"id":"1364","type":"DatetimeTickFormatter"},{"attributes":{},"id":"1347","type":"BasicTicker"},{"attributes":{},"id":"1351","type":"PanTool"},{"attributes":{"axis_label":"year","coordinates":null,"formatter":{"id":"1364"},"group":null,"major_label_policy":{"id":"1365"},"ticker":{"id":"1343"}},"id":"1342","type":"DatetimeAxis"},{"attributes":{},"id":"1338","type":"LinearScale"},{"attributes":{"line_color":"#e5ae38","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"1471","type":"Line"},{"attributes":{"days":[1,8,15,22]},"id":"1392","type":"DaysTicker"},{"attributes":{"days":[1,15]},"id":"1393","type":"DaysTicker"},{"attributes":{"label":{"value":"housing_units"},"renderers":[{"id":"1408"}]},"id":"1434","type":"LegendItem"},{"attributes":{"line_alpha":0.1,"line_color":"#30a2da","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"1373","type":"Line"},{"attributes":{"num_minor_ticks":5,"tickers":[{"id":"1387"},{"id":"1388"},{"id":"1389"},{"id":"1390"},{"id":"1391"},{"id":"1392"},{"id":"1393"},{"id":"1394"},{"id":"1395"},{"id":"1396"},{"id":"1397"},{"id":"1398"}]},"id":"1343","type":"DatetimeTicker"},{"attributes":{"children":[{"id":"1327"},{"id":"1333"},{"id":"1706"}],"margin":[0,0,0,0],"name":"Row02047","tags":["embedded"]},"id":"1326","type":"Row"},{"attributes":{"line_color":"#30a2da","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"1372","type":"Line"},{"attributes":{"months":[0,2,4,6,8,10]},"id":"1395","type":"MonthsTicker"},{"attributes":{},"id":"1340","type":"LinearScale"},{"attributes":{"axis_label":"","coordinates":null,"formatter":{"id":"1367"},"group":null,"major_label_policy":{"id":"1368"},"ticker":{"id":"1347"}},"id":"1346","type":"LinearAxis"},{"attributes":{"source":{"id":"1369"}},"id":"1376","type":"CDSView"},{"attributes":{"coordinates":null,"data_source":{"id":"1369"},"glyph":{"id":"1372"},"group":null,"hover_glyph":null,"muted_glyph":{"id":"1374"},"nonselection_glyph":{"id":"1373"},"selection_glyph":{"id":"1401"},"view":{"id":"1376"}},"id":"1375","type":"GlyphRenderer"},{"attributes":{"axis":{"id":"1342"},"coordinates":null,"grid_line_color":null,"group":null,"ticker":null},"id":"1345","type":"Grid"},{"attributes":{"months":[0,4,8]},"id":"1396","type":"MonthsTicker"},{"attributes":{"data":{"Variable":["sale_price_sqr_foot","sale_price_sqr_foot","sale_price_sqr_foot","sale_price_sqr_foot","sale_price_sqr_foot","sale_price_sqr_foot","sale_price_sqr_foot"],"value":{"__ndarray__":"tgKjeIIVd0Dn7CdydF51QGhijk899nhAZhKk2Jo5fkDGKCTbN2KBQPMTFqRSxINATx33UCbNhUA=","dtype":"float64","order":"little","shape":[7]},"year":{"__ndarray__":"AACA53JeckIAAED67dNyQgAAAA1pSXNCAACAhTa/c0IAAECYsTR0QgAAAKssqnRCAADAvacfdUI=","dtype":"float64","order":"little","shape":[7]}},"selected":{"id":"1370"},"selection_policy":{"id":"1384"}},"id":"1369","type":"ColumnDataSource"},{"attributes":{"base":60,"mantissas":[1,2,5,10,15,20,30],"max_interval":1800000.0,"min_interval":1000.0,"num_minor_ticks":0},"id":"1388","type":"AdaptiveTicker"},{"attributes":{"line_alpha":0.1,"line_color":"#e5ae38","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"1440","type":"Line"},{"attributes":{"months":[0,6]},"id":"1397","type":"MonthsTicker"},{"attributes":{"margin":[5,5,5,5],"name":"HSpacer02051","sizing_mode":"stretch_width"},"id":"1327","type":"Spacer"},{"attributes":{"axis":{"id":"1346"},"coordinates":null,"dimension":1,"grid_line_color":null,"group":null,"ticker":null},"id":"1349","type":"Grid"},{"attributes":{"line_alpha":0.1,"line_color":"#fc4f30","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"1406","type":"Line"},{"attributes":{"line_alpha":0.2,"line_color":"#30a2da","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"1374","type":"Line"},{"attributes":{},"id":"1398","type":"YearsTicker"},{"attributes":{"click_policy":"mute","coordinates":null,"group":null,"items":[{"id":"1400"},{"id":"1434"},{"id":"1470"}],"location":[0,0],"title":"Variable"},"id":"1399","type":"Legend"},{"attributes":{"data":{"Variable":["housing_units","housing_units","housing_units","housing_units","housing_units","housing_units","housing_units"],"value":{"__ndarray__":"AAAAAEC9FkEAAAAArNsWQQAAAAAY+hZBAAAAAIQYF0EAAAAA8DYXQQAAAABcVRdBAAAAAMhzF0E=","dtype":"float64","order":"little","shape":[7]},"year":{"__ndarray__":"AACA53JeckIAAED67dNyQgAAAA1pSXNCAACAhTa/c0IAAECYsTR0QgAAAKssqnRCAADAvacfdUI=","dtype":"float64","order":"little","shape":[7]}},"selected":{"id":"1403"},"selection_policy":{"id":"1419"}},"id":"1402","type":"ColumnDataSource"},{"attributes":{"end":422632.009657082,"reset_end":422632.009657082,"reset_start":-38048.10622790189,"start":-38048.10622790189,"tags":[[["value","value",null]]]},"id":"1329","type":"Range1d"},{"attributes":{"data":{"Variable":["gross_rent","gross_rent","gross_rent","gross_rent","gross_rent","gross_rent","gross_rent"],"value":{"__ndarray__":"AAAAAABck0AAAAAAAOiXQAAAAAAAKKJAAAAAAAA2p0AAAAAAAJCrQAAAAAAANq1AAAAAAAAmsUA=","dtype":"float64","order":"little","shape":[7]},"year":{"__ndarray__":"AACA53JeckIAAED67dNyQgAAAA1pSXNCAACAhTa/c0IAAECYsTR0QgAAAKssqnRCAADAvacfdUI=","dtype":"float64","order":"little","shape":[7]}},"selected":{"id":"1437"},"selection_policy":{"id":"1455"}},"id":"1436","type":"ColumnDataSource"},{"attributes":{},"id":"1368","type":"AllLabels"},{"attributes":{},"id":"1365","type":"AllLabels"},{"attributes":{"mantissas":[1,2,5],"max_interval":500.0,"num_minor_ticks":0},"id":"1387","type":"AdaptiveTicker"},{"attributes":{},"id":"1437","type":"Selection"},{"attributes":{"margin":[5,5,5,5],"name":"HSpacer02052","sizing_mode":"stretch_width"},"id":"1706","type":"Spacer"},{"attributes":{"line_color":"#fc4f30","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"1435","type":"Line"},{"attributes":{},"id":"1350","type":"SaveTool"},{"attributes":{"label":{"value":"sale_price_sqr_foot"},"renderers":[{"id":"1375"}]},"id":"1400","type":"LegendItem"},{"attributes":{},"id":"1384","type":"UnionRenderers"}],"root_ids":["1326"]},"title":"Bokeh Application","version":"2.4.1"}};
    var render_items = [{"docid":"bfeed9d5-8222-4b4c-814d-10116da30916","root_ids":["1326"],"roots":{"1326":"01c090cd-c57c-457f-8d5e-1016a13f8f67"}}];
    root.Bokeh.embed.embed_items_notebook(docs_json, render_items);
  }
  if (root.Bokeh !== undefined && root.Bokeh.Panel !== undefined) {
    embed_document(root);
  } else {
    var attempts = 0;
    var timer = setInterval(function(root) {
      if (root.Bokeh !== undefined && root.Bokeh.Panel !== undefined) {
        clearInterval(timer);
        embed_document(root);
      } else if (document.readyState == "complete") {
        attempts++;
        if (attempts > 200) {
          clearInterval(timer);
          console.log("Bokeh: ERROR: Unable to run BokehJS code because BokehJS library is missing");
        }
      }
    }, 25, root)
  }
})(window);</script>



### Step 5: Answer the following question:

**Question:** What is the overall trend in housing_units over the period being analyzed?

**Answer:** #That housing prices are increasing at a rate of 2% each year.

---

### Step 1: Group the data by year, and then average the results.


```python
# Create a numerical aggregation by grouping the data by year and averaging the results
prices_square_foot_by_year = housing_units_by_year.groupby(['sale_price_sqr_foot']).mean()





# Review the resulting DataFrame
prices_square_foot_by_year
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>housing_units</th>
      <th>gross_rent</th>
    </tr>
    <tr>
      <th>sale_price_sqr_foot</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>341.903429</th>
      <td>374507.0</td>
      <td>1530.0</td>
    </tr>
    <tr>
      <th>369.344353</th>
      <td>372560.0</td>
      <td>1239.0</td>
    </tr>
    <tr>
      <th>399.389968</th>
      <td>376454.0</td>
      <td>2324.0</td>
    </tr>
    <tr>
      <th>483.600304</th>
      <td>378401.0</td>
      <td>2971.0</td>
    </tr>
    <tr>
      <th>556.277273</th>
      <td>380348.0</td>
      <td>3528.0</td>
    </tr>
    <tr>
      <th>632.540352</th>
      <td>382295.0</td>
      <td>3739.0</td>
    </tr>
    <tr>
      <th>697.643709</th>
      <td>384242.0</td>
      <td>4390.0</td>
    </tr>
  </tbody>
</table>
</div>



**Question:** What is the lowest gross rent reported for the years included in the DataFrame?

**Answer:** # 1239

### Step 2: Create a new DataFrame named `prices_square_foot_by_year` by filtering out the “housing_units” column. The new DataFrame should include the averages per year for only the sale price per square foot and the gross rent.


```python
# Filter out the housing_units column, creating a new DataFrame 
# Keep only sale_price_sqr_foot and gross_rent averages per year

prices_square_foot_by_year.drop(columns=['housing_units'])



# Review the DataFrame
prices_square_foot_by_year.drop(columns=['housing_units'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>gross_rent</th>
    </tr>
    <tr>
      <th>sale_price_sqr_foot</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>341.903429</th>
      <td>1530.0</td>
    </tr>
    <tr>
      <th>369.344353</th>
      <td>1239.0</td>
    </tr>
    <tr>
      <th>399.389968</th>
      <td>2324.0</td>
    </tr>
    <tr>
      <th>483.600304</th>
      <td>2971.0</td>
    </tr>
    <tr>
      <th>556.277273</th>
      <td>3528.0</td>
    </tr>
    <tr>
      <th>632.540352</th>
      <td>3739.0</td>
    </tr>
    <tr>
      <th>697.643709</th>
      <td>4390.0</td>
    </tr>
  </tbody>
</table>
</div>



### Step 3: Use hvPlot to plot the `prices_square_foot_by_year` DataFrame as a line plot.

> **Hint** This single plot will include lines for both `sale_price_sqr_foot` and `gross_rent`

### Step 4: Style and format the line plot to ensure a professionally styled visualization.



```python
# Plot prices_square_foot_by_year. 
# Inclued labels for the x- and y-axes, and a title.

prices_square_foot_by_year.hvplot.line(
    xlabel = "housing_units",
    ylabel = "sale_price_sqr_foot	 / gross_rent",
    width=700, 
    height=300,
    title = "Sale Price Per Sqr FT and Avr Gross Rent 2010 thru 2016 in San Francisco"
)
```






<div id='2093'>





  <div class="bk-root" id="a4433b42-19ee-49aa-8c2d-8e16d88d05e2" data-root-id="2093"></div>
</div>
<script type="application/javascript">(function(root) {
  function embed_document(root) {
    var docs_json = {"85cde6f0-b510-4a43-94a1-bcdd09e2bf12":{"defs":[{"extends":null,"module":null,"name":"ReactiveHTML1","overrides":[],"properties":[]},{"extends":null,"module":null,"name":"FlexBox1","overrides":[],"properties":[{"default":"flex-start","kind":null,"name":"align_content"},{"default":"flex-start","kind":null,"name":"align_items"},{"default":"row","kind":null,"name":"flex_direction"},{"default":"wrap","kind":null,"name":"flex_wrap"},{"default":"flex-start","kind":null,"name":"justify_content"}]},{"extends":null,"module":null,"name":"TemplateActions1","overrides":[],"properties":[{"default":0,"kind":null,"name":"open_modal"},{"default":0,"kind":null,"name":"close_modal"}]},{"extends":null,"module":null,"name":"MaterialTemplateActions1","overrides":[],"properties":[{"default":0,"kind":null,"name":"open_modal"},{"default":0,"kind":null,"name":"close_modal"}]}],"roots":{"references":[{"attributes":{"coordinates":null,"group":null,"text":"Sale Price Per Sqr FT and Avr Gross Rent 2010 thru 2016 in San Francisco","text_color":"black","text_font_size":"12pt"},"id":"2100","type":"Title"},{"attributes":{"line_alpha":0.2,"line_color":"#30a2da","line_width":2,"x":{"field":"sale_price_sqr_foot"},"y":{"field":"value"}},"id":"2140","type":"Line"},{"attributes":{"line_alpha":0.2,"line_color":"#fc4f30","line_width":2,"x":{"field":"sale_price_sqr_foot"},"y":{"field":"value"}},"id":"2161","type":"Line"},{"attributes":{},"id":"2131","type":"AllLabels"},{"attributes":{},"id":"2120","type":"ResetTool"},{"attributes":{},"id":"2136","type":"Selection"},{"attributes":{"line_color":"#fc4f30","line_width":2,"x":{"field":"sale_price_sqr_foot"},"y":{"field":"value"}},"id":"2159","type":"Line"},{"attributes":{},"id":"2133","type":"BasicTickFormatter"},{"attributes":{"tools":[{"id":"2097"},{"id":"2116"},{"id":"2117"},{"id":"2118"},{"id":"2119"},{"id":"2120"}]},"id":"2122","type":"Toolbar"},{"attributes":{},"id":"2106","type":"LinearScale"},{"attributes":{},"id":"2104","type":"LinearScale"},{"attributes":{"axis_label":"sale_price_sqr_foot\t / gross_rent","coordinates":null,"formatter":{"id":"2133"},"group":null,"major_label_policy":{"id":"2134"},"ticker":{"id":"2113"}},"id":"2112","type":"LinearAxis"},{"attributes":{"below":[{"id":"2108"}],"center":[{"id":"2111"},{"id":"2115"}],"height":300,"left":[{"id":"2112"}],"margin":[5,5,5,5],"min_border_bottom":10,"min_border_left":10,"min_border_right":10,"min_border_top":10,"renderers":[{"id":"2141"},{"id":"2162"}],"right":[{"id":"2153"}],"sizing_mode":"fixed","title":{"id":"2100"},"toolbar":{"id":"2122"},"width":700,"x_range":{"id":"2095"},"x_scale":{"id":"2104"},"y_range":{"id":"2096"},"y_scale":{"id":"2106"}},"id":"2099","subtype":"Figure","type":"Plot"},{"attributes":{"line_color":"#30a2da","line_width":2,"x":{"field":"sale_price_sqr_foot"},"y":{"field":"value"}},"id":"2138","type":"Line"},{"attributes":{"axis_label":"housing_units","coordinates":null,"formatter":{"id":"2130"},"group":null,"major_label_policy":{"id":"2131"},"ticker":{"id":"2109"}},"id":"2108","type":"LinearAxis"},{"attributes":{"bottom_units":"screen","coordinates":null,"fill_alpha":0.5,"fill_color":"lightgrey","group":null,"left_units":"screen","level":"overlay","line_alpha":1.0,"line_color":"black","line_dash":[4,4],"line_width":2,"right_units":"screen","syncable":false,"top_units":"screen"},"id":"2121","type":"BoxAnnotation"},{"attributes":{"source":{"id":"2135"}},"id":"2142","type":"CDSView"},{"attributes":{"end":422542.3,"reset_end":422542.3,"reset_start":-37061.3,"start":-37061.3,"tags":[[["value","value",null]]]},"id":"2096","type":"Range1d"},{"attributes":{"line_color":"#30a2da","line_width":2,"x":{"field":"sale_price_sqr_foot"},"y":{"field":"value"}},"id":"2155","type":"Line"},{"attributes":{"axis":{"id":"2112"},"coordinates":null,"dimension":1,"grid_line_color":null,"group":null,"ticker":null},"id":"2115","type":"Grid"},{"attributes":{"label":{"value":"gross_rent"},"renderers":[{"id":"2162"}]},"id":"2176","type":"LegendItem"},{"attributes":{},"id":"2109","type":"BasicTicker"},{"attributes":{},"id":"2150","type":"UnionRenderers"},{"attributes":{"coordinates":null,"data_source":{"id":"2135"},"glyph":{"id":"2138"},"group":null,"hover_glyph":null,"muted_glyph":{"id":"2140"},"nonselection_glyph":{"id":"2139"},"selection_glyph":{"id":"2155"},"view":{"id":"2142"}},"id":"2141","type":"GlyphRenderer"},{"attributes":{"coordinates":null,"data_source":{"id":"2156"},"glyph":{"id":"2159"},"group":null,"hover_glyph":null,"muted_glyph":{"id":"2161"},"nonselection_glyph":{"id":"2160"},"selection_glyph":{"id":"2177"},"view":{"id":"2163"}},"id":"2162","type":"GlyphRenderer"},{"attributes":{"data":{"Variable":["gross_rent","gross_rent","gross_rent","gross_rent","gross_rent","gross_rent","gross_rent"],"sale_price_sqr_foot":{"__ndarray__":"5+wncnRedUC2AqN4ghV3QGhijk899nhAZhKk2Jo5fkDGKCTbN2KBQPMTFqRSxINATx33UCbNhUA=","dtype":"float64","order":"little","shape":[7]},"value":{"__ndarray__":"AAAAAADol0AAAAAAAFyTQAAAAAAAKKJAAAAAAAA2p0AAAAAAAJCrQAAAAAAANq1AAAAAAAAmsUA=","dtype":"float64","order":"little","shape":[7]}},"selected":{"id":"2157"},"selection_policy":{"id":"2173"}},"id":"2156","type":"ColumnDataSource"},{"attributes":{"children":[{"id":"2094"},{"id":"2099"},{"id":"2286"}],"margin":[0,0,0,0],"name":"Row03070","tags":["embedded"]},"id":"2093","type":"Row"},{"attributes":{"end":697.643709116537,"reset_end":697.643709116537,"reset_start":341.9034291801058,"start":341.9034291801058,"tags":[[["sale_price_sqr_foot","sale_price_sqr_foot",null]]]},"id":"2095","type":"Range1d"},{"attributes":{"line_color":"#fc4f30","line_width":2,"x":{"field":"sale_price_sqr_foot"},"y":{"field":"value"}},"id":"2177","type":"Line"},{"attributes":{"callback":null,"renderers":[{"id":"2141"},{"id":"2162"}],"tags":["hv_created"],"tooltips":[["Variable","@{Variable}"],["sale_price_sqr_foot","@{sale_price_sqr_foot}"],["value","@{value}"]]},"id":"2097","type":"HoverTool"},{"attributes":{"margin":[5,5,5,5],"name":"HSpacer03075","sizing_mode":"stretch_width"},"id":"2286","type":"Spacer"},{"attributes":{},"id":"2134","type":"AllLabels"},{"attributes":{"label":{"value":"housing_units"},"renderers":[{"id":"2141"}]},"id":"2154","type":"LegendItem"},{"attributes":{"margin":[5,5,5,5],"name":"HSpacer03074","sizing_mode":"stretch_width"},"id":"2094","type":"Spacer"},{"attributes":{"axis":{"id":"2108"},"coordinates":null,"grid_line_color":null,"group":null,"ticker":null},"id":"2111","type":"Grid"},{"attributes":{},"id":"2173","type":"UnionRenderers"},{"attributes":{},"id":"2116","type":"SaveTool"},{"attributes":{},"id":"2117","type":"PanTool"},{"attributes":{},"id":"2130","type":"BasicTickFormatter"},{"attributes":{"click_policy":"mute","coordinates":null,"group":null,"items":[{"id":"2154"},{"id":"2176"}],"location":[0,0],"title":"Variable"},"id":"2153","type":"Legend"},{"attributes":{},"id":"2118","type":"WheelZoomTool"},{"attributes":{"data":{"Variable":["housing_units","housing_units","housing_units","housing_units","housing_units","housing_units","housing_units"],"sale_price_sqr_foot":{"__ndarray__":"5+wncnRedUC2AqN4ghV3QGhijk899nhAZhKk2Jo5fkDGKCTbN2KBQPMTFqRSxINATx33UCbNhUA=","dtype":"float64","order":"little","shape":[7]},"value":{"__ndarray__":"AAAAAKzbFkEAAAAAQL0WQQAAAAAY+hZBAAAAAIQYF0EAAAAA8DYXQQAAAABcVRdBAAAAAMhzF0E=","dtype":"float64","order":"little","shape":[7]}},"selected":{"id":"2136"},"selection_policy":{"id":"2150"}},"id":"2135","type":"ColumnDataSource"},{"attributes":{"source":{"id":"2156"}},"id":"2163","type":"CDSView"},{"attributes":{"line_alpha":0.1,"line_color":"#fc4f30","line_width":2,"x":{"field":"sale_price_sqr_foot"},"y":{"field":"value"}},"id":"2160","type":"Line"},{"attributes":{"overlay":{"id":"2121"}},"id":"2119","type":"BoxZoomTool"},{"attributes":{},"id":"2113","type":"BasicTicker"},{"attributes":{},"id":"2157","type":"Selection"},{"attributes":{"line_alpha":0.1,"line_color":"#30a2da","line_width":2,"x":{"field":"sale_price_sqr_foot"},"y":{"field":"value"}},"id":"2139","type":"Line"}],"root_ids":["2093"]},"title":"Bokeh Application","version":"2.4.1"}};
    var render_items = [{"docid":"85cde6f0-b510-4a43-94a1-bcdd09e2bf12","root_ids":["2093"],"roots":{"2093":"a4433b42-19ee-49aa-8c2d-8e16d88d05e2"}}];
    root.Bokeh.embed.embed_items_notebook(docs_json, render_items);
  }
  if (root.Bokeh !== undefined && root.Bokeh.Panel !== undefined) {
    embed_document(root);
  } else {
    var attempts = 0;
    var timer = setInterval(function(root) {
      if (root.Bokeh !== undefined && root.Bokeh.Panel !== undefined) {
        clearInterval(timer);
        embed_document(root);
      } else if (document.readyState == "complete") {
        attempts++;
        if (attempts > 200) {
          clearInterval(timer);
          console.log("Bokeh: ERROR: Unable to run BokehJS code because BokehJS library is missing");
        }
      }
    }, 25, root)
  }
})(window);</script>



### Step 6: Use both the `prices_square_foot_by_year` DataFrame and interactive plots to answer the following questions:

**Question:** Did any year experience a drop in the average sale price per square foot compared to the previous year?

**Answer:** # Saw decreases between the end of 2010-2011, 2012-2013, 2013-2014


```python

```

**Question:** If so, did the gross rent increase or decrease during that year?

**Answer:** # The gross rent both increased and decreased during those years. 

---


```python
## Compare the Average Sale Prices by Neighborhood

For this part of the assignment, use interactive visualizations and widgets to explore the average sale price per square foot by neighborhood. To do so, complete the following steps:

1. Create a new DataFrame that groups the original DataFrame by year and neighborhood. Aggregate the results by the `mean` of the groups.

2. Filter out the “housing_units” column to create a DataFrame that includes only the `sale_price_sqr_foot` and `gross_rent` averages per year.

3. Create an interactive line plot with hvPlot that visualizes both `sale_price_sqr_foot` and `gross_rent`. Set the x-axis parameter to the year (`x="year"`). Use the `groupby` parameter to create an interactive widget for `neighborhood`.

4. Style and format the line plot to ensure a professionally styled visualization.

5. Note that your resulting plot should appear similar to the following image:

![A screenshot depicts an example of the resulting plot.](Images/pricing-info-by-neighborhood.png)

6. Use the interactive visualization to answer the following question:

    * For the Anza Vista neighborhood, is the average sale price per square foot for 2016 more or less than the price that’s listed for 2012? 

```

### Step 1: Create a new DataFrame that groups the original DataFrame by year and neighborhood. Aggregate the results by the `mean` of the groups.


```python
# Group by year and neighborhood and then create a new dataframe of the mean values
#prices_by_year_by_neighborhood = 

df_prices_by_year_by_neighborhood = sfo_dataframe.groupby(["year", "neighborhood"]).mean()




```


```python
# Review the DataFrame
df_prices_by_year_by_neighborhood.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>sale_price_sqr_foot</th>
      <th>housing_units</th>
      <th>gross_rent</th>
    </tr>
    <tr>
      <th>year</th>
      <th>neighborhood</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">2010-01-01</th>
      <th>Alamo Square</th>
      <td>291.182945</td>
      <td>372560.0</td>
      <td>1239.0</td>
    </tr>
    <tr>
      <th>Anza Vista</th>
      <td>267.932583</td>
      <td>372560.0</td>
      <td>1239.0</td>
    </tr>
    <tr>
      <th>Bayview</th>
      <td>170.098665</td>
      <td>372560.0</td>
      <td>1239.0</td>
    </tr>
    <tr>
      <th>Buena Vista Park</th>
      <td>347.394919</td>
      <td>372560.0</td>
      <td>1239.0</td>
    </tr>
    <tr>
      <th>Central Richmond</th>
      <td>319.027623</td>
      <td>372560.0</td>
      <td>1239.0</td>
    </tr>
  </tbody>
</table>
</div>



### Step 2: Filter out the “housing_units” column to create a DataFrame that includes only the `sale_price_sqr_foot` and `gross_rent` averages per year.


```python
# Filter out the housing_units
prices_by_year_by_neighborhood = df_prices_by_year_by_neighborhood.drop(columns=['housing_units'])

# Review the first and last five rows of the DataFrame
prices_by_year_by_neighborhood.head(5)
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>sale_price_sqr_foot</th>
      <th>gross_rent</th>
    </tr>
    <tr>
      <th>year</th>
      <th>neighborhood</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">2010-01-01</th>
      <th>Alamo Square</th>
      <td>291.182945</td>
      <td>1239.0</td>
    </tr>
    <tr>
      <th>Anza Vista</th>
      <td>267.932583</td>
      <td>1239.0</td>
    </tr>
    <tr>
      <th>Bayview</th>
      <td>170.098665</td>
      <td>1239.0</td>
    </tr>
    <tr>
      <th>Buena Vista Park</th>
      <td>347.394919</td>
      <td>1239.0</td>
    </tr>
    <tr>
      <th>Central Richmond</th>
      <td>319.027623</td>
      <td>1239.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# YOUR CODE HERE
prices_by_year_by_neighborhood.tail(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>sale_price_sqr_foot</th>
      <th>gross_rent</th>
    </tr>
    <tr>
      <th>year</th>
      <th>neighborhood</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">2016-01-01</th>
      <th>Telegraph Hill</th>
      <td>903.049771</td>
      <td>4390.0</td>
    </tr>
    <tr>
      <th>Twin Peaks</th>
      <td>970.085470</td>
      <td>4390.0</td>
    </tr>
    <tr>
      <th>Van Ness/ Civic Center</th>
      <td>552.602567</td>
      <td>4390.0</td>
    </tr>
    <tr>
      <th>Visitacion Valley</th>
      <td>328.319007</td>
      <td>4390.0</td>
    </tr>
    <tr>
      <th>Westwood Park</th>
      <td>631.195426</td>
      <td>4390.0</td>
    </tr>
  </tbody>
</table>
</div>



### Step 3: Create an interactive line plot with hvPlot that visualizes both `sale_price_sqr_foot` and `gross_rent`. Set the x-axis parameter to the year (`x="year"`). Use the `groupby` parameter to create an interactive widget for `neighborhood`.

### Step 4: Style and format the line plot to ensure a professionally styled visualization.


```python
# Use hvplot to create an interactive line plot of the average price per square foot

# The plot should have a dropdown selector for the neighborhood
prices_by_year_by_neighborhood.hvplot.line(
    x = "year",
    xlabel = "Year",
    ylabel = "Gross Rent / Sale Price Per Square Foot",
    width=700, 
    height=300,
    groupby = "neighborhood",
    title = "Sale Price Per Square Foot and Average Gross Rent - 2010-2016 - San Francisco"
)
```






<div id='2348'>





  <div class="bk-root" id="2fa754a4-dcab-44b4-b500-d58c83a2c407" data-root-id="2348"></div>
</div>
<script type="application/javascript">(function(root) {
  function embed_document(root) {
    var docs_json = {"372bafe6-45e1-440b-a592-c8b82dc827e7":{"defs":[{"extends":null,"module":null,"name":"ReactiveHTML1","overrides":[],"properties":[]},{"extends":null,"module":null,"name":"FlexBox1","overrides":[],"properties":[{"default":"flex-start","kind":null,"name":"align_content"},{"default":"flex-start","kind":null,"name":"align_items"},{"default":"row","kind":null,"name":"flex_direction"},{"default":"wrap","kind":null,"name":"flex_wrap"},{"default":"flex-start","kind":null,"name":"justify_content"}]},{"extends":null,"module":null,"name":"TemplateActions1","overrides":[],"properties":[{"default":0,"kind":null,"name":"open_modal"},{"default":0,"kind":null,"name":"close_modal"}]},{"extends":null,"module":null,"name":"MaterialTemplateActions1","overrides":[],"properties":[{"default":0,"kind":null,"name":"open_modal"},{"default":0,"kind":null,"name":"close_modal"}]}],"roots":{"references":[{"attributes":{},"id":"2371","type":"SaveTool"},{"attributes":{"margin":[20,20,20,20],"min_width":250,"options":["Alamo Square","Anza Vista","Bayview","Buena Vista Park","Central Richmond","Central Sunset","Corona Heights","Cow Hollow","Croker Amazon","Diamond Heights","Downtown ","Eureka Valley/Dolores Heights","Excelsior","Financial District North","Financial District South","Forest Knolls","Glen Park","Golden Gate Heights","Haight Ashbury","Hayes Valley","Hunters Point","Ingleside ","Inner Mission","Inner Parkside","Inner Richmond","Inner Sunset","Jordan Park/Laurel Heights","Lake --The Presidio","Lone Mountain","Lower Pacific Heights","Marina","Miraloma Park","Mission Bay","Mission Dolores","Mission Terrace","Nob Hill","Noe Valley","Oceanview","Outer Parkside","Outer Richmond ","Outer Sunset","Pacific Heights","Park North","Parkside","Parnassus/Ashbury Heights","Portola","Potrero Hill","Presidio Heights","Russian Hill","South Beach","South of Market","Sunnyside","Telegraph Hill","Twin Peaks","Union Square District","Van Ness/ Civic Center","West Portal","Western Addition","Yerba Buena","Bernal Heights ","Clarendon Heights","Duboce Triangle","Ingleside Heights","North Beach","North Waterfront","Outer Mission","Westwood Highlands","Merced Heights","Midtown Terrace","Visitacion Valley","Silver Terrace","Westwood Park","Bayview Heights"],"title":"neighborhood","value":"Alamo Square","width":250},"id":"2683","type":"Select"},{"attributes":{},"id":"2372","type":"PanTool"},{"attributes":{"children":[{"id":"2349"},{"id":"2354"},{"id":"2679"},{"id":"2680"}],"margin":[0,0,0,0],"name":"Row03442"},"id":"2348","type":"Row"},{"attributes":{},"id":"2375","type":"ResetTool"},{"attributes":{"mantissas":[1,2,5],"max_interval":500.0,"num_minor_ticks":0},"id":"2408","type":"AdaptiveTicker"},{"attributes":{},"id":"2373","type":"WheelZoomTool"},{"attributes":{"below":[{"id":"2363"}],"center":[{"id":"2366"},{"id":"2370"}],"height":300,"left":[{"id":"2367"}],"margin":[5,5,5,5],"min_border_bottom":10,"min_border_left":10,"min_border_right":10,"min_border_top":10,"renderers":[{"id":"2396"},{"id":"2429"}],"right":[{"id":"2420"}],"sizing_mode":"fixed","title":{"id":"2355"},"toolbar":{"id":"2377"},"width":700,"x_range":{"id":"2350"},"x_scale":{"id":"2359"},"y_range":{"id":"2351"},"y_scale":{"id":"2361"}},"id":"2354","subtype":"Figure","type":"Plot"},{"attributes":{"overlay":{"id":"2376"}},"id":"2374","type":"BoxZoomTool"},{"attributes":{"line_color":"#fc4f30","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"2456","type":"Line"},{"attributes":{"margin":[5,5,5,5],"name":"VSpacer03448","sizing_mode":"stretch_height"},"id":"2681","type":"Spacer"},{"attributes":{"end":4810.690068306854,"reset_end":4810.690068306854,"reset_start":-237.59075137539725,"start":-237.59075137539725,"tags":[[["value","value",null]]]},"id":"2351","type":"Range1d"},{"attributes":{"days":[1,4,7,10,13,16,19,22,25,28]},"id":"2412","type":"DaysTicker"},{"attributes":{"tools":[{"id":"2352"},{"id":"2371"},{"id":"2372"},{"id":"2373"},{"id":"2374"},{"id":"2375"}]},"id":"2377","type":"Toolbar"},{"attributes":{"days":[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31]},"id":"2411","type":"DaysTicker"},{"attributes":{"coordinates":null,"group":null,"text":"Sale Price Per Square Foot and Average Gross Rent - 2010-2016 - San Francisco","text_color":"black","text_font_size":"12pt"},"id":"2355","type":"Title"},{"attributes":{"axis_label":"Year","coordinates":null,"formatter":{"id":"2385"},"group":null,"major_label_policy":{"id":"2386"},"ticker":{"id":"2364"}},"id":"2363","type":"DatetimeAxis"},{"attributes":{"children":[{"id":"2683"}],"css_classes":["panel-widget-box"],"margin":[5,5,5,5],"name":"WidgetBox03443"},"id":"2682","type":"Column"},{"attributes":{"source":{"id":"2390"}},"id":"2397","type":"CDSView"},{"attributes":{"callback":null,"formatters":{"@{year}":"datetime"},"renderers":[{"id":"2396"},{"id":"2429"}],"tags":["hv_created"],"tooltips":[["Variable","@{Variable}"],["year","@{year}{%F %T}"],["value","@{value}"]]},"id":"2352","type":"HoverTool"},{"attributes":{"bottom_units":"screen","coordinates":null,"fill_alpha":0.5,"fill_color":"lightgrey","group":null,"left_units":"screen","level":"overlay","line_alpha":1.0,"line_color":"black","line_dash":[4,4],"line_width":2,"right_units":"screen","syncable":false,"top_units":"screen"},"id":"2376","type":"BoxAnnotation"},{"attributes":{"months":[0,1,2,3,4,5,6,7,8,9,10,11]},"id":"2415","type":"MonthsTicker"},{"attributes":{"days":[1,8,15,22]},"id":"2413","type":"DaysTicker"},{"attributes":{"days":[1,15]},"id":"2414","type":"DaysTicker"},{"attributes":{},"id":"2359","type":"LinearScale"},{"attributes":{"months":[0,2,4,6,8,10]},"id":"2416","type":"MonthsTicker"},{"attributes":{"months":[0,4,8]},"id":"2417","type":"MonthsTicker"},{"attributes":{"line_alpha":0.1,"line_color":"#30a2da","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"2394","type":"Line"},{"attributes":{},"id":"2391","type":"Selection"},{"attributes":{"base":24,"mantissas":[1,2,4,6,8,12],"max_interval":43200000.0,"min_interval":3600000.0,"num_minor_ticks":0},"id":"2410","type":"AdaptiveTicker"},{"attributes":{"base":60,"mantissas":[1,2,5,10,15,20,30],"max_interval":1800000.0,"min_interval":1000.0,"num_minor_ticks":0},"id":"2409","type":"AdaptiveTicker"},{"attributes":{},"id":"2388","type":"BasicTickFormatter"},{"attributes":{"months":[0,6]},"id":"2418","type":"MonthsTicker"},{"attributes":{"line_color":"#30a2da","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"2393","type":"Line"},{"attributes":{"margin":[5,5,5,5],"name":"HSpacer03452","sizing_mode":"stretch_width"},"id":"2679","type":"Spacer"},{"attributes":{"data":{"Variable":["sale_price_sqr_foot","sale_price_sqr_foot","sale_price_sqr_foot","sale_price_sqr_foot","sale_price_sqr_foot","sale_price_sqr_foot","sale_price_sqr_foot"],"value":{"__ndarray__":"DUc7WO0yckCafszcbwhxQIKRs5ot42ZAKDog0LQ8eEAVMinKGEd+QI4V5FDt0IJAVCHcmLVPdUA=","dtype":"float64","order":"little","shape":[7]},"year":{"__ndarray__":"AACA53JeckIAAED67dNyQgAAAA1pSXNCAACAhTa/c0IAAECYsTR0QgAAAKssqnRCAADAvacfdUI=","dtype":"float64","order":"little","shape":[7]}},"selected":{"id":"2391"},"selection_policy":{"id":"2405"}},"id":"2390","type":"ColumnDataSource"},{"attributes":{"source":{"id":"2423"}},"id":"2430","type":"CDSView"},{"attributes":{},"id":"2405","type":"UnionRenderers"},{"attributes":{},"id":"2419","type":"YearsTicker"},{"attributes":{"click_policy":"mute","coordinates":null,"group":null,"items":[{"id":"2421"},{"id":"2455"}],"location":[0,0],"title":"Variable"},"id":"2420","type":"Legend"},{"attributes":{"coordinates":null,"data_source":{"id":"2390"},"glyph":{"id":"2393"},"group":null,"hover_glyph":null,"muted_glyph":{"id":"2395"},"nonselection_glyph":{"id":"2394"},"selection_glyph":{"id":"2422"},"view":{"id":"2397"}},"id":"2396","type":"GlyphRenderer"},{"attributes":{"children":[{"id":"2681"},{"id":"2682"},{"id":"2684"}],"margin":[0,0,0,0],"name":"Column03450"},"id":"2680","type":"Column"},{"attributes":{"line_alpha":0.2,"line_color":"#30a2da","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"2395","type":"Line"},{"attributes":{"label":{"value":"sale_price_sqr_foot"},"renderers":[{"id":"2396"}]},"id":"2421","type":"LegendItem"},{"attributes":{"axis":{"id":"2367"},"coordinates":null,"dimension":1,"grid_line_color":null,"group":null,"ticker":null},"id":"2370","type":"Grid"},{"attributes":{"line_alpha":0.2,"line_color":"#fc4f30","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"2428","type":"Line"},{"attributes":{"data":{"Variable":["gross_rent","gross_rent","gross_rent","gross_rent","gross_rent","gross_rent","gross_rent"],"value":{"__ndarray__":"AAAAAABck0AAAAAAAOiXQAAAAAAAKKJAAAAAAAA2p0AAAAAAAJCrQAAAAAAANq1AAAAAAAAmsUA=","dtype":"float64","order":"little","shape":[7]},"year":{"__ndarray__":"AACA53JeckIAAED67dNyQgAAAA1pSXNCAACAhTa/c0IAAECYsTR0QgAAAKssqnRCAADAvacfdUI=","dtype":"float64","order":"little","shape":[7]}},"selected":{"id":"2424"},"selection_policy":{"id":"2440"}},"id":"2423","type":"ColumnDataSource"},{"attributes":{},"id":"2385","type":"DatetimeTickFormatter"},{"attributes":{},"id":"2424","type":"Selection"},{"attributes":{},"id":"2368","type":"BasicTicker"},{"attributes":{"client_comm_id":"be5a46c0bfe2462a90d9b4315f2816eb","comm_id":"4a963cec8c8d4b1f9618bbbb90c095b3","plot_id":"2348"},"id":"2757","type":"panel.models.comm_manager.CommManager"},{"attributes":{"end":1451606400000.0,"reset_end":1451606400000.0,"reset_start":1262304000000.0,"start":1262304000000.0,"tags":[[["year","year",null]]]},"id":"2350","type":"Range1d"},{"attributes":{"label":{"value":"gross_rent"},"renderers":[{"id":"2429"}]},"id":"2455","type":"LegendItem"},{"attributes":{"num_minor_ticks":5,"tickers":[{"id":"2408"},{"id":"2409"},{"id":"2410"},{"id":"2411"},{"id":"2412"},{"id":"2413"},{"id":"2414"},{"id":"2415"},{"id":"2416"},{"id":"2417"},{"id":"2418"},{"id":"2419"}]},"id":"2364","type":"DatetimeTicker"},{"attributes":{"axis":{"id":"2363"},"coordinates":null,"grid_line_color":null,"group":null,"ticker":null},"id":"2366","type":"Grid"},{"attributes":{},"id":"2361","type":"LinearScale"},{"attributes":{"line_color":"#30a2da","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"2422","type":"Line"},{"attributes":{"line_alpha":0.1,"line_color":"#fc4f30","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"2427","type":"Line"},{"attributes":{"axis_label":"Gross Rent / Sale Price Per Square Foot","coordinates":null,"formatter":{"id":"2388"},"group":null,"major_label_policy":{"id":"2389"},"ticker":{"id":"2368"}},"id":"2367","type":"LinearAxis"},{"attributes":{"margin":[5,5,5,5],"name":"VSpacer03449","sizing_mode":"stretch_height"},"id":"2684","type":"Spacer"},{"attributes":{"line_color":"#fc4f30","line_width":2,"x":{"field":"year"},"y":{"field":"value"}},"id":"2426","type":"Line"},{"attributes":{"coordinates":null,"data_source":{"id":"2423"},"glyph":{"id":"2426"},"group":null,"hover_glyph":null,"muted_glyph":{"id":"2428"},"nonselection_glyph":{"id":"2427"},"selection_glyph":{"id":"2456"},"view":{"id":"2430"}},"id":"2429","type":"GlyphRenderer"},{"attributes":{},"id":"2389","type":"AllLabels"},{"attributes":{},"id":"2386","type":"AllLabels"},{"attributes":{},"id":"2440","type":"UnionRenderers"},{"attributes":{"margin":[5,5,5,5],"name":"HSpacer03451","sizing_mode":"stretch_width"},"id":"2349","type":"Spacer"}],"root_ids":["2348","2757"]},"title":"Bokeh Application","version":"2.4.1"}};
    var render_items = [{"docid":"372bafe6-45e1-440b-a592-c8b82dc827e7","root_ids":["2348"],"roots":{"2348":"2fa754a4-dcab-44b4-b500-d58c83a2c407"}}];
    root.Bokeh.embed.embed_items_notebook(docs_json, render_items);
  }
  if (root.Bokeh !== undefined && root.Bokeh.Panel !== undefined) {
    embed_document(root);
  } else {
    var attempts = 0;
    var timer = setInterval(function(root) {
      if (root.Bokeh !== undefined && root.Bokeh.Panel !== undefined) {
        clearInterval(timer);
        embed_document(root);
      } else if (document.readyState == "complete") {
        attempts++;
        if (attempts > 200) {
          clearInterval(timer);
          console.log("Bokeh: ERROR: Unable to run BokehJS code because BokehJS library is missing");
        }
      }
    }, 25, root)
  }
})(window);</script>



### Step 6: Use the interactive visualization to answer the following question:

**Question:** For the Anza Vista neighborhood, is the average sale price per square foot for 2016 more or less than the price that’s listed for 2012? 

**Answer:** # Less

---

## Build an Interactive Neighborhood Map

For this part of the assignment, explore the geospatial relationships in the data by using interactive visualizations with hvPlot and GeoViews. To build your map, use the `sfo_data_df` DataFrame (created during the initial import), which includes the neighborhood location data with the average prices. To do all this, complete the following steps:

1. Read the `neighborhood_coordinates.csv` file from the `Resources` folder into the notebook, and create a DataFrame named `neighborhood_locations_df`. Be sure to set the `index_col` of the DataFrame as “Neighborhood”.

2. Using the original `sfo_data_df` Dataframe, create a DataFrame named `all_neighborhood_info_df` that groups the data by neighborhood. Aggregate the results by the `mean` of the group.

3. Review the two code cells that concatenate the `neighborhood_locations_df` DataFrame with the `all_neighborhood_info_df` DataFrame. Note that the first cell uses the [Pandas concat function](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.concat.html) to create a DataFrame named `all_neighborhoods_df`. The second cell cleans the data and sets the “Neighborhood” column. Be sure to run these cells to create the `all_neighborhoods_df` DataFrame, which you’ll need to create the geospatial visualization.

4. Using hvPlot with GeoViews enabled, create a `points` plot for the `all_neighborhoods_df` DataFrame. Be sure to do the following:

    * Set the `size` parameter to “sale_price_sqr_foot”.

    * Set the `color` parameter to “gross_rent”.

    * Set the `size_max` parameter to “25”.

    * Set the `zoom` parameter to “11”.

Note that your resulting plot should appear similar to the following image:

![A screenshot depicts an example of a scatter plot created with hvPlot and GeoViews.](Images/6-4-geoviews-plot.png)

5. Use the interactive map to answer the following question:

    * Which neighborhood has the highest gross rent, and which has the highest sale price per square foot?


### Step 1: Read the `neighborhood_coordinates.csv` file from the `Resources` folder into the notebook, and create a DataFrame named `neighborhood_locations_df`. Be sure to set the `index_col` of the DataFrame as “Neighborhood”.


```python
# Load neighborhoods coordinates data
neighborhood_locations_df = pd.read_csv(Path("Resources/neighborhoods_coordinates.csv"), index_col="Neighborhood")

# Review the DataFrame
neighborhood_locations_df.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Lat</th>
      <th>Lon</th>
    </tr>
    <tr>
      <th>Neighborhood</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alamo Square</th>
      <td>37.791012</td>
      <td>-122.402100</td>
    </tr>
    <tr>
      <th>Anza Vista</th>
      <td>37.779598</td>
      <td>-122.443451</td>
    </tr>
    <tr>
      <th>Bayview</th>
      <td>37.734670</td>
      <td>-122.401060</td>
    </tr>
    <tr>
      <th>Bayview Heights</th>
      <td>37.728740</td>
      <td>-122.410980</td>
    </tr>
    <tr>
      <th>Bernal Heights</th>
      <td>37.728630</td>
      <td>-122.443050</td>
    </tr>
  </tbody>
</table>
</div>



### Step 2: Using the original `sfo_data_df` Dataframe, create a DataFrame named `all_neighborhood_info_df` that groups the data by neighborhood. Aggregate the results by the `mean` of the group.


```python
# Calculate the mean values for each neighborhood
all_neighborhood_info_df =  sfo_dataframe.groupby("neighborhood").mean()

# Review the resulting DataFrame
all_neighborhood_info_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>sale_price_sqr_foot</th>
      <th>housing_units</th>
      <th>gross_rent</th>
    </tr>
    <tr>
      <th>neighborhood</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alamo Square</th>
      <td>366.020712</td>
      <td>378401.00</td>
      <td>2817.285714</td>
    </tr>
    <tr>
      <th>Anza Vista</th>
      <td>373.382198</td>
      <td>379050.00</td>
      <td>3031.833333</td>
    </tr>
    <tr>
      <th>Bayview</th>
      <td>204.588623</td>
      <td>376454.00</td>
      <td>2318.400000</td>
    </tr>
    <tr>
      <th>Bayview Heights</th>
      <td>590.792839</td>
      <td>382295.00</td>
      <td>3739.000000</td>
    </tr>
    <tr>
      <th>Bernal Heights</th>
      <td>576.746488</td>
      <td>379374.50</td>
      <td>3080.333333</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>West Portal</th>
      <td>498.488485</td>
      <td>376940.75</td>
      <td>2515.500000</td>
    </tr>
    <tr>
      <th>Western Addition</th>
      <td>307.562201</td>
      <td>377427.50</td>
      <td>2555.166667</td>
    </tr>
    <tr>
      <th>Westwood Highlands</th>
      <td>533.703935</td>
      <td>376454.00</td>
      <td>2250.500000</td>
    </tr>
    <tr>
      <th>Westwood Park</th>
      <td>687.087575</td>
      <td>382295.00</td>
      <td>3959.000000</td>
    </tr>
    <tr>
      <th>Yerba Buena</th>
      <td>576.709848</td>
      <td>377427.50</td>
      <td>2555.166667</td>
    </tr>
  </tbody>
</table>
<p>73 rows × 3 columns</p>
</div>



### Step 3: Review the two code cells that concatenate the `neighborhood_locations_df` DataFrame with the `all_neighborhood_info_df` DataFrame. 

Note that the first cell uses the [Pandas concat function](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.concat.html) to create a DataFrame named `all_neighborhoods_df`. 

The second cell cleans the data and sets the “Neighborhood” column. 

Be sure to run these cells to create the `all_neighborhoods_df` DataFrame, which you’ll need to create the geospatial visualization.


```python
# Using the Pandas `concat` function, join the 
# neighborhood_locations_df and the all_neighborhood_info_df DataFrame
# The axis of the concatenation is "columns".
# The concat function will automatially combine columns with
# identical information, while keeping the additional columns.
all_neighborhoods_df = pd.concat(
    [neighborhood_locations_df, all_neighborhood_info_df], 
    axis="columns",
    sort=False
)

# Review the resulting DataFrame
display(all_neighborhoods_df.head())
display(all_neighborhoods_df.tail())

```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Lat</th>
      <th>Lon</th>
      <th>sale_price_sqr_foot</th>
      <th>housing_units</th>
      <th>gross_rent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alamo Square</th>
      <td>37.791012</td>
      <td>-122.402100</td>
      <td>366.020712</td>
      <td>378401.0</td>
      <td>2817.285714</td>
    </tr>
    <tr>
      <th>Anza Vista</th>
      <td>37.779598</td>
      <td>-122.443451</td>
      <td>373.382198</td>
      <td>379050.0</td>
      <td>3031.833333</td>
    </tr>
    <tr>
      <th>Bayview</th>
      <td>37.734670</td>
      <td>-122.401060</td>
      <td>204.588623</td>
      <td>376454.0</td>
      <td>2318.400000</td>
    </tr>
    <tr>
      <th>Bayview Heights</th>
      <td>37.728740</td>
      <td>-122.410980</td>
      <td>590.792839</td>
      <td>382295.0</td>
      <td>3739.000000</td>
    </tr>
    <tr>
      <th>Bernal Heights</th>
      <td>37.728630</td>
      <td>-122.443050</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Lat</th>
      <th>Lon</th>
      <th>sale_price_sqr_foot</th>
      <th>housing_units</th>
      <th>gross_rent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Yerba Buena</th>
      <td>37.79298</td>
      <td>-122.39636</td>
      <td>576.709848</td>
      <td>377427.5</td>
      <td>2555.166667</td>
    </tr>
    <tr>
      <th>Bernal Heights</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>576.746488</td>
      <td>379374.5</td>
      <td>3080.333333</td>
    </tr>
    <tr>
      <th>Downtown</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>391.434378</td>
      <td>378401.0</td>
      <td>2817.285714</td>
    </tr>
    <tr>
      <th>Ingleside</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>367.895144</td>
      <td>377427.5</td>
      <td>2509.000000</td>
    </tr>
    <tr>
      <th>Outer Richmond</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>473.900773</td>
      <td>378401.0</td>
      <td>2817.285714</td>
    </tr>
  </tbody>
</table>
</div>



```python
# Call the dropna function to remove any neighborhoods that do not have data
all_neighborhoods_df = all_neighborhoods_df.reset_index().dropna()

# Rename the "index" column as "Neighborhood" for use in the Visualization
all_neighborhoods_df = all_neighborhoods_df.rename(columns={"index": "Neighborhood"})

# Review the resulting DataFrame
display(all_neighborhoods_df.head())
display(all_neighborhoods_df.tail())
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Neighborhood</th>
      <th>Lat</th>
      <th>Lon</th>
      <th>sale_price_sqr_foot</th>
      <th>housing_units</th>
      <th>gross_rent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alamo Square</td>
      <td>37.791012</td>
      <td>-122.402100</td>
      <td>366.020712</td>
      <td>378401.0</td>
      <td>2817.285714</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Anza Vista</td>
      <td>37.779598</td>
      <td>-122.443451</td>
      <td>373.382198</td>
      <td>379050.0</td>
      <td>3031.833333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bayview</td>
      <td>37.734670</td>
      <td>-122.401060</td>
      <td>204.588623</td>
      <td>376454.0</td>
      <td>2318.400000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bayview Heights</td>
      <td>37.728740</td>
      <td>-122.410980</td>
      <td>590.792839</td>
      <td>382295.0</td>
      <td>3739.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Buena Vista Park</td>
      <td>37.768160</td>
      <td>-122.439330</td>
      <td>452.680591</td>
      <td>378076.5</td>
      <td>2698.833333</td>
    </tr>
  </tbody>
</table>
</div>



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Neighborhood</th>
      <th>Lat</th>
      <th>Lon</th>
      <th>sale_price_sqr_foot</th>
      <th>housing_units</th>
      <th>gross_rent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>68</th>
      <td>West Portal</td>
      <td>37.74026</td>
      <td>-122.463880</td>
      <td>498.488485</td>
      <td>376940.75</td>
      <td>2515.500000</td>
    </tr>
    <tr>
      <th>69</th>
      <td>Western Addition</td>
      <td>37.79298</td>
      <td>-122.435790</td>
      <td>307.562201</td>
      <td>377427.50</td>
      <td>2555.166667</td>
    </tr>
    <tr>
      <th>70</th>
      <td>Westwood Highlands</td>
      <td>37.73470</td>
      <td>-122.456854</td>
      <td>533.703935</td>
      <td>376454.00</td>
      <td>2250.500000</td>
    </tr>
    <tr>
      <th>71</th>
      <td>Westwood Park</td>
      <td>37.73415</td>
      <td>-122.457000</td>
      <td>687.087575</td>
      <td>382295.00</td>
      <td>3959.000000</td>
    </tr>
    <tr>
      <th>72</th>
      <td>Yerba Buena</td>
      <td>37.79298</td>
      <td>-122.396360</td>
      <td>576.709848</td>
      <td>377427.50</td>
      <td>2555.166667</td>
    </tr>
  </tbody>
</table>
</div>


### Step 4: Using hvPlot with GeoViews enabled, create a `points` plot for the `all_neighborhoods_df` DataFrame. Be sure to do the following:

* Set the `geo` parameter to True.
* Set the `size` parameter to “sale_price_sqr_foot”.
* Set the `color` parameter to “gross_rent”.
* Set the `frame_width` parameter to 700.
* Set the `frame_height` parameter to 500.
* Include a descriptive title.


```python
# Create a plot to analyze neighborhood info
all_neighborhoods_df.hvplot.points(
    'Lon',
    'Lat',
    geo=True,
    size='sale_price_sqr_foot',
    color='gross_rent',
    frame_width=700,
    frame_height=500,
    title='San Fran Neighborhoods average prices.'
)    

    
```






<div id='3158'>





  <div class="bk-root" id="b6a073e6-44ba-4a02-a5a1-dc975557fa04" data-root-id="3158"></div>
</div>
<script type="application/javascript">(function(root) {
  function embed_document(root) {
    var docs_json = {"72b54df9-1edb-4348-acfb-a5f576f398a1":{"defs":[{"extends":null,"module":null,"name":"ReactiveHTML1","overrides":[],"properties":[]},{"extends":null,"module":null,"name":"FlexBox1","overrides":[],"properties":[{"default":"flex-start","kind":null,"name":"align_content"},{"default":"flex-start","kind":null,"name":"align_items"},{"default":"row","kind":null,"name":"flex_direction"},{"default":"wrap","kind":null,"name":"flex_wrap"},{"default":"flex-start","kind":null,"name":"justify_content"}]},{"extends":null,"module":null,"name":"TemplateActions1","overrides":[],"properties":[{"default":0,"kind":null,"name":"open_modal"},{"default":0,"kind":null,"name":"close_modal"}]},{"extends":null,"module":null,"name":"MaterialTemplateActions1","overrides":[],"properties":[{"default":0,"kind":null,"name":"open_modal"},{"default":0,"kind":null,"name":"close_modal"}]}],"roots":{"references":[{"attributes":{},"id":"3176","type":"LinearScale"},{"attributes":{"axis_label":"Lat","coordinates":null,"formatter":{"id":"3217"},"group":null,"major_label_policy":{"id":"3227"},"ticker":{"id":"3216"}},"id":"3182","type":"LinearAxis"},{"attributes":{"end":4552574.475709082,"min_interval":5,"reset_end":4552574.475709082,"reset_start":4538788.497756597,"start":4538788.497756597,"tags":[[["Lat","Lat",null]]]},"id":"3163","type":"Range1d"},{"attributes":{"axis_label":"Lon","coordinates":null,"formatter":{"id":"3215"},"group":null,"major_label_policy":{"id":"3220"},"ticker":{"id":"3214"}},"id":"3178","type":"LinearAxis"},{"attributes":{"high":3959.0,"low":1781.5,"palette":["#b3fef5","#b0fef5","#adfdf5","#a9fcf5","#a6fbf6","#a3faf6","#a0faf6","#9df9f6","#9af8f6","#97f7f6","#93f7f6","#90f6f6","#8df5f6","#8af4f7","#87f3f7","#83f2f7","#80f2f7","#7df1f7","#79f0f7","#76eff7","#73eef7","#6fedf8","#6cecf8","#68ecf8","#65ebf8","#61eaf8","#5ee9f8","#5ae8f8","#57e7f8","#53e6f8","#50e5f9","#4ce4f9","#49e3f9","#45e2f9","#42e1f9","#3ee0f9","#3bdff9","#38def9","#35ddf9","#32dcf9","#30dbfa","#2ed9fa","#2dd8fa","#2cd7fa","#2bd6fa","#2bd5fa","#2ad3fa","#2ad2fa","#29d1fa","#29d0fb","#29cffb","#28cdfb","#28ccfb","#28cbfb","#28cafb","#28c8fb","#28c7fb","#29c6fb","#29c5fb","#29c4fb","#29c2fb","#2ac1fb","#2ac0fb","#2bbffb","#2bbdfc","#2cbcfc","#2dbbfc","#2db9fc","#2eb8fc","#2fb7fc","#2fb6fc","#30b4fc","#31b3fc","#32b2fc","#32b0fc","#33affc","#33aefc","#34adfc","#34abfc","#34aafc","#35a9fc","#35a8fc","#35a6fc","#35a5fc","#35a4fc","#35a3fc","#35a1fc","#35a0fc","#359ffc","#359dfc","#359cfc","#359bfc","#349afd","#3498fd","#3497fd","#3396fd","#3395fd","#3293fd","#3292fd","#3191fd","#3090fd","#308ffd","#2f8dfd","#2f8cfd","#2e8bfd","#2e8afd","#2d88fd","#2d87fd","#2c86fd","#2c84fd","#2c83fd","#2c82fd","#2b81fd","#2b7ffd","#2b7efd","#2b7dfd","#2b7bfd","#2b7afd","#2b79fd","#2b77fd","#2b76fd","#2b75fd","#2b73fd","#2c72fd","#2c71fd","#2c6ffd","#2c6efd","#2d6cfd","#2d6bfd","#2d6afc","#2e68fc","#2e67fc","#2e65fc","#2e64fc","#2f62fc","#2f61fc","#2f5ffc","#2f5efc","#2f5dfc","#2f5bfc","#2f5afc","#2f58fb","#2f57fb","#2f55fb","#2f53fb","#2f52fb","#2f50fb","#2f4ffb","#2f4dfb","#2e4cfb","#2e4afb","#2e48fb","#2e47fa","#2d45fa","#2d43fa","#2d42fa","#2d40fa","#2c3efa","#2c3dfa","#2b3bf9","#2b39f9","#2a37f9","#2a36f8","#2934f8","#2832f7","#2831f7","#272ff6","#262ef5","#252cf5","#252af4","#2429f3","#2327f2","#2226f1","#2124f0","#2023ef","#1f22ee","#1e20ed","#1d1feb","#1c1eea","#1b1ce9","#1a1be7","#181ae6","#1719e5","#1618e3","#1417e1","#1316e0","#1215de","#1014dc","#0f13db","#0e12d9","#0d11d7","#0c10d5","#0b0fd3","#0a0ed1","#090dd0","#080dce","#080ccc","#070bca","#070ac8","#0709c6","#0708c4","#0707c2","#0707bf","#0806bd","#0806bb","#0905b9","#0904b7","#0a04b5","#0a04b2","#0b03b0","#0c03ae","#0d02ab","#0e02a9","#0e02a7","#0f02a4","#0f01a2","#1001a0","#10019d","#10019b","#100199","#100197","#100194","#0f0192","#0f0190","#0f018e","#0e018b","#0e0189","#0d0187","#0d0185","#0c0183","#0b0181","#0b017e","#0a017c","#09017a","#090178","#080276","#070274","#060272","#060270","#05026e","#04026c","#030269","#030267","#020265","#010263","#010261","#00025f","#00025d","#00025b","#000259","#000257","#000255","#000154","#000152","#000150","#00004e"]},"id":"3197","type":"LinearColorMapper"},{"attributes":{},"id":"3199","type":"Selection"},{"attributes":{"axis":{"id":"3182"},"coordinates":null,"dimension":1,"grid_line_color":null,"group":null,"ticker":null},"id":"3185","type":"Grid"},{"attributes":{"match_aspect":true,"overlay":{"id":"3189"}},"id":"3165","type":"BoxZoomTool"},{"attributes":{"fill_alpha":{"value":0.1},"fill_color":{"field":"color","transform":{"id":"3197"}},"hatch_alpha":{"value":0.1},"hatch_color":{"field":"color","transform":{"id":"3197"}},"line_alpha":{"value":0.1},"line_color":{"field":"color","transform":{"id":"3197"}},"size":{"field":"size"},"x":{"field":"Lon"},"y":{"field":"Lat"}},"id":"3202","type":"Scatter"},{"attributes":{"coordinates":null,"data_source":{"id":"3198"},"glyph":{"id":"3201"},"group":null,"hover_glyph":{"id":"3204"},"muted_glyph":{"id":"3205"},"nonselection_glyph":{"id":"3202"},"selection_glyph":{"id":"3203"},"view":{"id":"3207"}},"id":"3206","type":"GlyphRenderer"},{"attributes":{},"id":"3234","type":"NoOverlap"},{"attributes":{"code":"\n        var projections = Bokeh.require(\"core/util/projections\");\n        var x = special_vars.data_x\n        var y = special_vars.data_y\n        if (projections.wgs84_mercator.invert == null) {\n          var coords = projections.wgs84_mercator.inverse([x, y])\n        } else {\n          var coords = projections.wgs84_mercator.invert(x, y)\n        }\n        return \"\" + (coords[1]).toFixed(4)\n    "},"id":"3211","type":"CustomJSHover"},{"attributes":{"callback":null,"formatters":{"$x":{"id":"3210"},"$y":{"id":"3211"}},"renderers":[{"id":"3206"}],"tags":["hv_created"],"tooltips":[["Lon","$x{custom}"],["Lat","$y{custom}"],["gross_rent","@{gross_rent}"],["sale_price_sqr_foot","@{sale_price_sqr_foot}"]]},"id":"3166","type":"HoverTool"},{"attributes":{"margin":[5,5,5,5],"name":"HSpacer05851","sizing_mode":"stretch_width"},"id":"3159","type":"Spacer"},{"attributes":{"bar_line_color":"black","color_mapper":{"id":"3197"},"coordinates":null,"group":null,"label_standoff":8,"location":[0,0],"major_label_policy":{"id":"3234"},"major_tick_line_color":"black","ticker":{"id":"3208"}},"id":"3209","type":"ColorBar"},{"attributes":{"bottom_units":"screen","coordinates":null,"fill_alpha":0.5,"fill_color":"lightgrey","group":null,"left_units":"screen","level":"overlay","line_alpha":1.0,"line_color":"black","line_dash":[4,4],"line_width":2,"right_units":"screen","syncable":false,"top_units":"screen"},"id":"3189","type":"BoxAnnotation"},{"attributes":{"source":{"id":"3198"}},"id":"3207","type":"CDSView"},{"attributes":{"tools":[{"id":"3164"},{"id":"3165"},{"id":"3166"},{"id":"3186"},{"id":"3187"},{"id":"3188"}]},"id":"3190","type":"Toolbar"},{"attributes":{"fill_color":{"field":"color","transform":{"id":"3197"}},"hatch_color":{"field":"color","transform":{"id":"3197"}},"line_color":{"field":"color","transform":{"id":"3197"}},"size":{"field":"size"},"x":{"field":"Lon"},"y":{"field":"Lat"}},"id":"3201","type":"Scatter"},{"attributes":{"end":-13619293.591003094,"min_interval":5,"reset_end":-13619293.591003094,"reset_start":-13638593.960136574,"start":-13638593.960136574,"tags":[[["Lon","Lon",null]]]},"id":"3162","type":"Range1d"},{"attributes":{},"id":"3186","type":"SaveTool"},{"attributes":{},"id":"3187","type":"PanTool"},{"attributes":{"dimension":"lat"},"id":"3216","type":"MercatorTicker"},{"attributes":{},"id":"3220","type":"AllLabels"},{"attributes":{},"id":"3188","type":"ResetTool"},{"attributes":{},"id":"3227","type":"AllLabels"},{"attributes":{"fill_color":{"field":"color","transform":{"id":"3197"}},"hatch_color":{"field":"color","transform":{"id":"3197"}},"line_color":{"field":"color","transform":{"id":"3197"}},"size":{"field":"size"},"x":{"field":"Lon"},"y":{"field":"Lat"}},"id":"3204","type":"Scatter"},{"attributes":{"zoom_on_axis":false},"id":"3164","type":"WheelZoomTool"},{"attributes":{},"id":"3208","type":"BasicTicker"},{"attributes":{"code":"\n        var projections = Bokeh.require(\"core/util/projections\");\n        var x = special_vars.data_x\n        var y = special_vars.data_y\n        if (projections.wgs84_mercator.invert == null) {\n          var coords = projections.wgs84_mercator.inverse([x, y])\n        } else {\n          var coords = projections.wgs84_mercator.invert(x, y)\n        }\n        return \"\" + (coords[0]).toFixed(4)\n    "},"id":"3210","type":"CustomJSHover"},{"attributes":{"dimension":"lon"},"id":"3215","type":"MercatorTickFormatter"},{"attributes":{"below":[{"id":"3178"}],"center":[{"id":"3181"},{"id":"3185"}],"frame_height":500,"frame_width":700,"height":null,"left":[{"id":"3182"}],"margin":[5,5,5,5],"match_aspect":true,"min_border_bottom":10,"min_border_left":10,"min_border_right":10,"min_border_top":10,"renderers":[{"id":"3206"}],"right":[{"id":"3209"}],"sizing_mode":"fixed","title":{"id":"3170"},"toolbar":{"id":"3190"},"width":null,"x_range":{"id":"3162"},"x_scale":{"id":"3174"},"y_range":{"id":"3163"},"y_scale":{"id":"3176"}},"id":"3169","subtype":"Figure","type":"Plot"},{"attributes":{"dimension":"lon"},"id":"3214","type":"MercatorTicker"},{"attributes":{"data":{"Lat":{"__ndarray__":"DAZSL05bUUERJz5BvFlRQRU76MWOU1FBI8JNG75SUUGFpr+KKVhRQWlQdR2AWVFBHmRUj5xVUUHwUo3KHlZRQamMnCKNWlFBwh7ofZNbUUH1Euga7VFRQYtMcTy6UlFBtgKVpV1YUUEeKP9IbVZRQSPCTRu+UlFBtiBKHU5bUUG2IEodTltRQb9yAcqiVlFBi0xxPLpSUUH2pqnHwFZRQdQYfxjDV1FB1Bh/GMNXUUEhKqF0TFJRQfKTZ2ezUVFBck/MtTxWUUEeZFSPnFVRQbcd1Q5LWFFBHmRUj5xVUUGpjJwijVpRQVISHETAXFFBcdp6raNZUUHCHuh9k1tRQUpmPd6AXFFBuyX+IIhRUUHwUo3KHlZRQXxYeXl8U1FBOpYAJTxaUUEE/sQM61VRQYtMcTy6UlFBwh7ofZNbUUHwUo3KHlZRQQfJ9hmeXFFBB8n2GZ5cUUG7Jf4giFFRQfUS6BrtUVFBVbZHH+ZVUUEeZFSPnFVRQcIe6H2TW1FBAah9cLFSUUEeZFSPnFVRQZ61yz+HV1FBFTvoxY5TUUGqKCppL1NRQamMnCKNWlFBwh7ofZNbUUEVO+jFjlNRQTqWACU8WlFBtiBKHU5bUUF8WHl5fFNRQQfJ9hmeXFFBbxiQ0x5WUUG2IEodTltRQX83Aii5WVFBI8JNG75SUUGvOKR9U1RRQcIe6H2TW1FBQfYp1I9TUUF8WHl5fFNRQcIe6H2TW1FB","dtype":"float64","order":"little","shape":[69]},"Lon":{"__ndarray__":"2Xg1bjH9acE0qLjTcP9pwWIIf/Ui/WnBhWDB/qz9acEnJMx7N/9pwdoRL7+I/2nBLuMMavgBasFhguugov9pwWYMEXIfAGrBzYeGOQb/acHLaPmTLv9pwTUFRT9r/2nB7DUzh3/+acFQEfkNIv9pwYVgwf6s/WnB2Xg1bjH9acHZeDVuMf1pwf1pccgSAGrBNQVFP2v/acFOyBkLjwBqwZGBGpcI/2nBkYEalwj/acF8DJaHi/tpwVVsW8jPAWrBBt4IIiP+acEu4wxq+AFqwR1EUwafAWrBU03OIvgBasFmDBFyHwBqwcIxFowLAGrB8Jta+RAAasHNh4Y5Bv9pwYTIrvq2AGrBU0Ux5qkAasFhguugov9pwSdRSlwtAGrBWQj8QB39acFeKdIkc/5pwTUFRT9r/2nBzYeGOQb/acFhguugov9pwbG993VQ/WnBsb33dVD9acFTRTHmqQBqwcto+ZMu/2nB11zUS5T/acEu4wxq+AFqwc2HhjkG/2nBV+K4q1gBasEu4wxq+AFqwXNXvGc2AGrBYgh/9SL9acF4d6v+KvxpwWYMEXIfAGrBzYeGOQb/acFiCH/1Iv1pwVkI/EAd/WnB2Xg1bjH9acEnUUpcLQBqwbG993VQ/WnBfJRbnaL/acHZeDVuMf1pwZbRs5Et/mnBhWDB/qz9acFSr2MYjQBqwc2HhjkG/2nB0aQ0VCsAasEnUUpcLQBqwW14C4/h/GnB","dtype":"float64","order":"little","shape":[69]},"color":{"__ndarray__":"SZIkSZICpkCrqqqqqq+nQM3MzMzMHKJAAAAAAAA2rUCrqqqqqhWlQEmSJEmSAqZASZIkSZICpkAAAAAAAJWhQAAAAAAAUKNASZIkSZICpkCrqqqqqhWlQAAAAAAAgJ9AAAAAAIC4pUBJkiRJkgKmQKuqqqqqr6dASZIkSZICpkAAAAAAAFCjQAAAAAAA1ptAAAAAAACnpkDNzMzMzFKkQEmSJEmSAqZASZIkSZICpkAAAAAAAHKjQAAAAAAAIKdASZIkSZICpkAAAAAAADCpQEmSJEmSAqZASZIkSZICpkBJkiRJkgKmQFVVVVVV9qNAVVVVVVX2o0BJkiRJkgKmQEmSJEmSAqZAAAAAAACsqkAAAAAAAK+kQAAAAACA1qBAVVVVVVXPpEBVVVVVVfajQM3MzMzMyqhASZIkSZICpkBJkiRJkgKmQJqZmZmZXadAzczMzMwEpkAAAAAAAASjQAAAAACAZ6dASZIkSZICpkBJkiRJkgKmQEmSJEmSAqZASZIkSZICpkBVVVVVVfajQEmSJEmSAqZAzczMzMwcokBJkiRJkgKmQEmSJEmSAqZASZIkSZICpkAAAAAAAJCrQAAAAAAAZqBASZIkSZICpkAAAAAAAKemQEmSJEmSAqZASZIkSZICpkBVVVVVVfajQEmSJEmSAqZAAAAAAACSrEAAAAAAAKejQFVVVVVV9qNAAAAAAACVoUAAAAAAAO6uQFVVVVVV9qNA","dtype":"float64","order":"little","shape":[69]},"gross_rent":{"__ndarray__":"SZIkSZICpkCrqqqqqq+nQM3MzMzMHKJAAAAAAAA2rUCrqqqqqhWlQEmSJEmSAqZASZIkSZICpkAAAAAAAJWhQAAAAAAAUKNASZIkSZICpkCrqqqqqhWlQAAAAAAAgJ9AAAAAAIC4pUBJkiRJkgKmQKuqqqqqr6dASZIkSZICpkAAAAAAAFCjQAAAAAAA1ptAAAAAAACnpkDNzMzMzFKkQEmSJEmSAqZASZIkSZICpkAAAAAAAHKjQAAAAAAAIKdASZIkSZICpkAAAAAAADCpQEmSJEmSAqZASZIkSZICpkBJkiRJkgKmQFVVVVVV9qNAVVVVVVX2o0BJkiRJkgKmQEmSJEmSAqZAAAAAAACsqkAAAAAAAK+kQAAAAACA1qBAVVVVVVXPpEBVVVVVVfajQM3MzMzMyqhASZIkSZICpkBJkiRJkgKmQJqZmZmZXadAzczMzMwEpkAAAAAAAASjQAAAAACAZ6dASZIkSZICpkBJkiRJkgKmQEmSJEmSAqZASZIkSZICpkBVVVVVVfajQEmSJEmSAqZAzczMzMwcokBJkiRJkgKmQEmSJEmSAqZASZIkSZICpkAAAAAAAJCrQAAAAAAAZqBASZIkSZICpkAAAAAAAKemQEmSJEmSAqZASZIkSZICpkBVVVVVVfajQEmSJEmSAqZAAAAAAACSrEAAAAAAAKejQFVVVVVV9qNAAAAAAACVoUAAAAAAAO6uQFVVVVVV9qNA","dtype":"float64","order":"little","shape":[69]},"sale_price_sqr_foot":{"__ndarray__":"cJyd1VTgdkAj1Xd7HVZ3QMu7p//VkmlA/23ou1d2gkDg3lCz40p8QJIjOSXCpnhA8ER6wAF7ekBhIJwN63N+QHYgjQJQXIJAC1duW7bPhEAumqsjEfByQA02LireL3tABPQiJJZpf0DNvwdH/RGEQIsgrDxBTHhATKx878x1eEBGXRUgYX18QOcoDRF0HXRAyP/3Apx+g0Br5HcBJvuDQEKNqFi3GHxAP5v/3Ow+dkAFP/VX/1NlQPiqSlDEDHhAfmgaicfaeECrA3m3FTuAQOA5W0+CqXdAyXixJK7aeUCo3p7PEouAQBsbzgZFn3lA1YI2J6jjfUACLzpc59mAQOp1/4D+PYJAfSK5L8KmiEDjM3wxFTSBQFx/3pp8XohAcr9Bp4mxgUC9Hcljpi56QAabwse6W4BAhQqU+EOjfEAzwd8Vi/OAQA1GhppZunlANoyg6lAkf0A0VzbjjqF0QGKNxdbeS25ATpTGpG5QfkBicP8ngaN4QBabFVByjIVAM1aax7lbd0AUODg4wwJ1QGCc43LsxYNAlFRio9JxdECazArhG7CEQMvN+TvNGoVAb73/oN0Hg0DTKbSOXEllQMmt8u7+UIRAhuHC4SvSgUD/YX/xi4KAQL0KhXgNJIVAiyAuxmBWfUAlEBQx8j+MQEdUUCNnQnlAoAgieXXXckDK9HfV0Cd/QF5rdMb+OHNAQN/mqKGtgEBr0ERas3iFQIOO/MStBYJA","dtype":"float64","order":"little","shape":[69]},"size":{"__ndarray__":"i5CP+rQhM0Ar8FGwtlIzQIW0KYddmyxA7Dx4HmVOOEArqHwOu0Y1QJkw7ZMt3DNAfKDrH2yVNEARoV8J2RI2QFBo1ow8PThAwyXPTmjOOUCmPO4oMmgxQHZMS6xA2zRABySuczFrNkCFmCVPtlc5QH7RpAOXtzNAOT5FJGvIM0Ajvzilrlk1QPFS4cqe8DFASdluufz5OEDBC5+JRkk5QFoZEx7VMzVA6FaYHL7dMkAdwvH/6x8qQP89V6vDnTNAoFV7DhfxM0B+lS6aP8o2QNgBpbsedTNAx6bfxbxWNEC0IVk/IwI3QEvdkvxQPzRASVJY6VHeNUD6Np0XtDg3QF55yPwwKThA+FGkFh0WPEBKv41YhHY3QLpRDezS7DtAqTLPm3fLN0AXMBViqXc0QK4KUksf4TZAoGOAHNxnNUD4AZjoV0o3QFNahFIBSjRAd9KiwmtSNkCGboU2KCsyQCbmLvTzIi9ApvDD4PgFNkCqIsX93dozQO9vFbNnQjpA7wykMQlVM0CN6NpWw1UyQBDpBFmCJzlAHw48LBcWMkCxlou3yLo5QBHuz97M/DlA66dGO3atOEC6N66fZxkqQHuKDbJefzlAvzI0C1/hN0BCM2CENPw2QDM68VJ+AjpAEi8PX2WqNUBmzfHfBBE+QBrE1Bt+GjRAjLbjPt9cMUAxdnLQrFM2QANd7WmWiTFA7y8d2B4aN0DiKhDsXDY6QMrPmOHIAzhA","dtype":"float64","order":"little","shape":[69]}},"selected":{"id":"3199"},"selection_policy":{"id":"3236"}},"id":"3198","type":"ColumnDataSource"},{"attributes":{"fill_color":{"field":"color","transform":{"id":"3197"}},"hatch_color":{"field":"color","transform":{"id":"3197"}},"line_color":{"field":"color","transform":{"id":"3197"}},"size":{"field":"size"},"x":{"field":"Lon"},"y":{"field":"Lat"}},"id":"3203","type":"Scatter"},{"attributes":{},"id":"3236","type":"UnionRenderers"},{"attributes":{"dimension":"lat"},"id":"3217","type":"MercatorTickFormatter"},{"attributes":{"coordinates":null,"group":null,"text":"San Fran Neighborhoods average prices.","text_color":"black","text_font_size":"12pt"},"id":"3170","type":"Title"},{"attributes":{"margin":[5,5,5,5],"name":"HSpacer05852","sizing_mode":"stretch_width"},"id":"3260","type":"Spacer"},{"attributes":{},"id":"3174","type":"LinearScale"},{"attributes":{"fill_alpha":{"value":0.2},"fill_color":{"field":"color","transform":{"id":"3197"}},"hatch_alpha":{"value":0.2},"hatch_color":{"field":"color","transform":{"id":"3197"}},"line_alpha":{"value":0.2},"line_color":{"field":"color","transform":{"id":"3197"}},"size":{"field":"size"},"x":{"field":"Lon"},"y":{"field":"Lat"}},"id":"3205","type":"Scatter"},{"attributes":{"axis":{"id":"3178"},"coordinates":null,"grid_line_color":null,"group":null,"ticker":null},"id":"3181","type":"Grid"},{"attributes":{"children":[{"id":"3159"},{"id":"3169"},{"id":"3260"}],"margin":[0,0,0,0],"name":"Row05847","tags":["embedded"]},"id":"3158","type":"Row"}],"root_ids":["3158"]},"title":"Bokeh Application","version":"2.4.1"}};
    var render_items = [{"docid":"72b54df9-1edb-4348-acfb-a5f576f398a1","root_ids":["3158"],"roots":{"3158":"b6a073e6-44ba-4a02-a5a1-dc975557fa04"}}];
    root.Bokeh.embed.embed_items_notebook(docs_json, render_items);
  }
  if (root.Bokeh !== undefined && root.Bokeh.Panel !== undefined) {
    embed_document(root);
  } else {
    var attempts = 0;
    var timer = setInterval(function(root) {
      if (root.Bokeh !== undefined && root.Bokeh.Panel !== undefined) {
        clearInterval(timer);
        embed_document(root);
      } else if (document.readyState == "complete") {
        attempts++;
        if (attempts > 200) {
          clearInterval(timer);
          console.log("Bokeh: ERROR: Unable to run BokehJS code because BokehJS library is missing");
        }
      }
    }, 25, root)
  }
})(window);</script>



### Step 5: Use the interactive map to answer the following question:

**Question:** Which neighborhood has the highest gross rent, and which has the highest sale price per square foot?

**Answer:** Westwood Park

## Compose Your Data Story

Based on the visualizations that you have created, compose a data story that synthesizes your analysis by answering the following questions:


```python
**Question:**  How does the trend in rental income growth compare to the trend in sales prices? Does this same trend hold true for all the neighborhoods across San Francisco?

**Answer:** # Gross rent does not seem to fluctuate as hist as price per square foot. So althought the price per sq ft can increase expotentially based on neighborhood for the most part the gross rent does not see an exponential increase in gross outside of three neighborhoods. 
```


```python
**Question:** What insights can you share with your company about the potential one-click, buy-and-rent strategy that they're pursuing? Do neighborhoods exist that you would suggest for investment, and why?

**Answer:** The market seems very risky if I had to invest it would be Westwood Park as they have more units and collect the most gross rent which is on par with what they are paying per sq ft.
```


```python

```
