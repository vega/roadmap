
# Roadmap for the Vega projects

In this repository,
you can find [the roadmap](https://github.com/orgs/vega/projects/9)
for the main [Vega projects](https://github.com/vega/.github/blob/main/CHARTER.md).
The roadmap is informed by the needs of the community,
and the priorities of the active project contributors.
It reflects the overarching goal of the Vega projects:
to provide a standard language
for data visualization practice and research,
regardless of the underlying programming language used
(e.g., JavaScript, Python, etc.).
While the roadmap is designed
to communicate the direction of the Vega projects,
it's not a commitment to complete these items
in a particular timeframe.

If you or your organization
would like to help contribute to any of these areas (or suggest new ones),
please comment on the open issues in the project board via the link above.

A few of the main areas of focus are described below,
but please see the roadmap's project board for details.

## Gridded Data Support

Vega-Lite and Vega-Altair currently requires tidy tabular data as input,
so it is not a natural choice for working with gridded data,
such as images.
We would like to extend the project
to include native support for gridded datasets,
including support for Python array/tensor interchange protocol
(through the `__dlpack__` interface),
support for creating charts from Xarray [DataArray](https://docs.xarray.dev/en/stable/generated/xarray.DataArray.html) objects,
and natively support a raster mark in the Vega-Lite grammar
for displaying images with pixel level interactions.

## Increased Coverage of Statistical Charts

While Vega-Lite and Vega-Altair
supports many types of statistical visualizations,
there are a few important types that are not yet possible.
Future improvements in this area
include the addition of violin charts, 2D density charts,
and added conveniences for plotting 1D density charts.

## Improved geospatial visualizations

Using the Vega primitives,
Vega-Lite and Vega-Altair seeks to provide first-class support 
for geospatial interactions.
The next steps in this area includes support for
map interactions such as panning and zooming,
faceting of geoshape marks,
and displaying map tiles from xyz tile providers like OpenStreetMap.
We've released a
first version of
[altair_tiles](https://github.com/altair-viz/altair_tiles) to
accomplish this. Feedback is very welcome!

## Scale/Performance Improvements

In the traditional Vega-Lite/Vega-Altair architecture,
a chart's entire input dataset is serialized to JSON
and transferred to the browser for data transformation and rendering.
Rendering itself is then performed by the Vega JavaScript library
using the Canvas API
(which is not GPU accelerated).
This architecture has many advantages
(e.g. chart specifications are fully self-contained
and portable to Python-free rendering environments),
but it is not well suited for creating charts of large datasets.

Our immediate efforts in this area
are focused on improving performance
for working with large data set in Vega-Altair
to benefit the many Python-based data science and scientific communities.
Our goal is to allow all Vega-Altair charts
to scale comfortably to over 1 million rows.

The main areas of focus here are the following:

- Provide integration with VegaFusion
  to automatically move data transformation steps from the browser
  to efficient
  multi-threaded implementations in the Python kernel.
  We aim to utilize binary serialization of datasets
  in Apache Arrow IPC format
  between the Python kernel and the browser.
  This will significantly
  reduce serialization time for large unaggregated visualizations
  such as scatter plots.
- Extend VegaFusion
  to support Vega-Altair charts that can reference tables
  in external database systems,
  and convert data transformation steps to SQL
  that can be evaluated by the database before the results are
  transferred to the Python kernel.
- Add support for GPU accelerated rendering directly in Vega.
  This will enable rendering of large unnagregated visualizations
  at interactive speeds.
  For example,
  pan and zoom interactions on a large scatter plot.

## Chart animations

We aim to enable animations for all chart types
by integrating the work from already published research in this area.


## Ecosystem Integration

We want Vega-Altair to be well integrated
with the PyData and scientific Python communities.
Currently,
the main area of focus is
to provide integration
with the broader Python DataFrame ecosystem
and ensure that all of Vega-Altair's features
are available to any DataFrame library that implements the
[DataFrame Interchange Protocol](https://data-apis.org/dataframe-protocol/latest/index.html).
We are also working with dashboard toolkit maintainers
to ensure that Vega-Altair is well supported
and readily available to dashboard users.

## Static Image Export

Although Vega-Altair charts are rendered by the Vega JavaScript library,
it's important to provide reliable (and easy to install)
support for exporting charts to static images.
Image export was dramatically simplified in Vega-Altair 5.0
with the adoption of VlConvert,
which has no external dependencies on a system web-browser or Node.js installation.
Now that image export is easy to install and easy
to use, we want to improve support for publication workflows
and support exporting charts to vector PDF files with embedded text
(**both released in 5.2 via vl-convert**).

## API ergonomics

The primary job of the Vega-Altair library is to provide an ergonomic
Python API for generating Vega-Lite JSON specifications,
and there are
several improvements here that we would like to investigate:

-   Improve the syntax for creating condition expressions with two or
    more predicates.
-   Explore the possibility of a new operator, `*`, for modular
    compositing of sub components. See also
    [Deneb.jl](https://brucala.github.io/Deneb.jl/dev).
-   Standardize the API of methods that convert charts into other
    formats (`alt.Chart().to_<format>`).
-   **Released in Vega-Altair 5.2:** *Add type hints to the public API and most of
    the internals so that users can type check their Altair code with a
    static type checker such as mypy. This will also make it easier for
    other packages to integrate with Altair.*

Significant improvements to API ergonomics would also come from
enabling the use of Expression References in additional places in Vega-Lite,
allowing for more convenient ways of achieving currently verbose specifications,
as well as important new functionality beyond a more ergonomic API.

## Documentation

We want to continue to develop official documentation for the Vega Projects,
and are currently focused on making the Vega-Altair documentation
more useful for both beginning and experienced users.

-   Incorporate a conceptual guide that includes best practices of
    effective data communication.
-   Update and extend the tutorial section and replace outdated
    materials.
-   Add usage guide with best practices for publishing Vega-Altair
    charts in various contexts including websites, research papers,
    embedded dashboards, and interactive platforms.
-   Add guide on building domain specific visualization packages on top
    of Vega-Altair. For example, Vega-Altair for soccer analytics.
-   Add documentation for the expression language that is available
    throughout the API.
