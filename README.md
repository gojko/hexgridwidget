# hexgridwidget

A simple jQuery Hex Grid Widget, implemented using SVG, for prototyping hex-grid
based games.

- Fields can are clickable, and the grid has dispatches an event with row and
  column position for easy analysis
- Fields have DOM attributes attached to signal row and column position, so you can
  easily select them using jQuery or DOM selectors. 
- Fields have jQuery meta-data attached to point to the center of the field, so
  you can easily put other objects on them and position relative to the grid
- Everything can be styled using CSS, there is no style enforcement by the
  widget. 

## Usage

Initialise the grid by calling hexGridWidget:

    $('#container').hexGridWidget(radius, columns, rows, cssClass)

- _radius_ is the length (in pixels) of the side of a single hexagon (effectively
the radius of the circle in which the hex field will be inscribed. 
- _columns_ is the number of columns of the hex grid (horizontal hex count)
- _rows_ is the number of rows (vertical hex count)
- _cssClass_ is the css class that will be set on the hex polygons, for easy
styling

##Selecting individual hex elements

Use the _hex-row_ and _hex-column_ DOM attributes to select an individual hex in
the grid. For example:

    $('#container [hex-row=2][hex-column=3]')

##Capturing clicks

There are two ways to capture clicks. The first one is to listen to a _hexclick_
event on the grid container DOM element. 

    $('#container').hexGridWidget(radius, columns, rows, cssClass).on('hexclick', function (e) { 
				console.log('clicked [' + e.column + ',' + e.row +']' +
				' hex with center at [' + e.center.x + ',' + e.center.y + ']');
    });

This event will have the following properties:

- column: hex grid column clicked
- row: hex grid row clicked
- center: object with {x, y} containing the center position of the clicked hex
  field, relative to the grid container

The second option is to assign a normal click handler to individual hex field,
or even a group of hexfields.

    $('#container .hexfield').click(function () {
      this.classList.toggle('clicked');
    });

The _hexclick_ event is particularly useful if you plan to resize grids
dynamically after creation, because the individual hexes will be destroyed after
resizing. 

##Styling

Just pass a CSS class name as the fourth argument of the widget initialisation
function, and style as you would any other DOM SVG element. 

The individual hex fields are SVG polygons, so any CSS styles that work on
polygons will also work on the grid.
