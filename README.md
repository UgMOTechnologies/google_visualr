# Overview

This Ruby gem, GoogleVisualr, is a wrapper around the {Google Chart Tools}[http://code.google.com/apis/chart/interactive/docs/index.html] that allows anyone to create the same beautiful charts with just plain Ruby.

You don't have to write any JavaScript at all!

Good for any Ruby on Rails setup whereby you prefer to work your logic in models or controllers.

Please refer to the {GoogleVisualr API Reference site}[http://googlevisualr.heroku.com/] for a complete list of Google charts that you can create with GoogleVisualr.

## The Gist

* In your model or controller, write Ruby code to create your chart (e.g. Area Chart, Bar Chart, even Spark Lines etc).
* Configure your chart with any of the options as listed in Google Chart Tools' API Docs. E.g. {Area Chart's Configuration Options}[http://code.google.com/apis/chart/interactive/docs/gallery/areachart.html#Configuration_Options].
* In your view, invoke a <em>chart.to_js(div_id)</em> method and that will magically generate and insert JavaScript into the final HTML output.
* You get your awesome Google chart, and you didn't write any JavaScript!

## Limitations

GoogleVisualr is created solely for the aim of simplifying the display of a chart, and not the interactions.

Hence, do note that GoogleVisualr is not a 100% complete wrapper for Google Chart Tools.

For example, Methods and Events as described in Google Chart Tools' API Docs, for use after a chart has been rendered, are not implemented because they felt more native being written as JavaScript functions, within views or .js files.

## Differences Between Gem and Plugin

Gem
* is Rails 3 compatible.
* implements many of the newer versions of Google Charts E.g. Core Charts.
* enjoyed a major refactoring, and also now has Tests!

Plugin
* has not been tested for Rails 3 compatibility
* implements the older versions of Google Charts.
* has deprecated methods.

This gem, however, is not a drop-in replacement for the plugin, as there are numerous changes in its usage.

Notably, you will have to interact mostly with GoogleVisualr::DataTable which was absent in the plugin.

# Install

Assuming you are on Rails 3, include the gem in your Gemfile.

  gem "google_visualr", ">= 2.1"

# Basics

This section describes a basic implementation of the GoogleVisualr::DataTable and GoogleVisualr::AreaChart classes.

For detailed documentation and advanced implementations, please refer to the {GoogleVisualr API Reference site}[http://googlevisualr.heroku.com/] or read the source.

---

In your Rails layout, load Google Ajax API in the head tag, at the very top.

  <script src='http://www.google.com/jsapi'></script>

In your Rails controller, initialize a GoogleVisualr::DataTable object with an empty constructor.

  data_table = GoogleVisualr::DataTable.new

Populate data_table with column headers, and row values.

  # Add Column Headers
  data_table.new_column('string', 'Year' )
  data_table.new_column('number', 'Sales')
  data_table.new_column('number', 'Expenses')

  # Add Rows and Values
  data_table.add_rows([
    ['2004', 1000, 400],
    ['2005', 1170, 460],
    ['2006', 660, 1120],
    ['2007', 1030, 540]
  ])

Create a GoogleVisualr::AreaChart with data_table and configuration options.

  option = { width: 400, height: 240, title: 'Company Performance' }
  @chart = GoogleVisualr::Interactive::AreaChart.new(data_table, option)

In your Rails view, render the Google chart.

  <div id='chart'></div>
  <%= render_chart(@chart, 'chart') %>

# Support

Please feel free to fork the project, make improvements or bug fixes and submit pull requests. Ideally, all pull requests should also come with tests!

Please submit all feedback, bugs and feature-requests to {GitHub Issues Tracker}[http://github.com/winston/google_visualr/issues].

# Change Log

*Version 2.1.0*
* Added `#render_chart` as a helper method in Rails views.

# Author

GoogleVisualr is maintained by {Winston Teo}[mailto:winstonyw+googlevisualr@gmail.com].

Who is Winston Teo? {You should follow Winston on Twitter}[http://www.twitter.com/winstonyw], or find out more on {WinstonYW}[http://www.winstonyw.com] and {LinkedIn}[http://sg.linkedin.com/in/winstonyw].

# License

Copyright © 2011 Winston Teo Yong Wei. Free software, released under the MIT license.
