CybOX XML to HTML Transform
===========================

Convert CybOX XML to HTML

**Version**: 2.0beta1

    Copyright (c) 2013 - The MITRE Corporation
    All rights reserved. See LICENSE.txt for more details.

    BY USING THIS PROGRAM, YOU SIGNIFY YOUR ACCEPTANCE OF THE TERMS AND CONDITIONS
    OF USE.  IF YOU DO NOT AGREE TO THESE TERMS, DO NOT USE THIS PROGRAM.

Overview
--------

This is an XSLT to transform a CybOX 2.0.1 document of Observables into HTML for
easy viewing within a web browser.  The Observables are turned into collapsible elements
on the screen.  Details about each Observable's contents are displayed in a
format representing the nested structure of the original document.

Below the main observable, Object, Event, and Observable_Composition are
displayed.  For composite observables, the nested structure of the composition
and the logical relationships is displayed via nested tables with operators
("and" and "or) on the left and then a series of component expressions in rows
on the right.

Any time objects are referred to by reference, they can be expanded in-line.

Compatible with:
* [CybOX 2.0.1](http://cybox.mitre.org/language/version2.0.1/)

Supports:
- Observable, Observable_Composition
- Object
- Related_Object
- Associated_Object
- Event
- cybox:Properties:
  * direct children of cybox:Properties will be printed with the local name of
    the element as the property "name", the text value of the element as the
    "value", and the attributes as "constraints".
  * specific templates can be created for Properties that need more detailed
    formatting
  * the following elements have specialized formatting:
    - EmailMessageObj:Header, FileObj:*

***Warning about CybOX properties***:
The general template that is applied will use the localname of the element
that is a direct child of cybox:Properties, the value is the text value of
this element (meaning all the text nodes of descendants are concatenated),
and the constraints column shows all attributes on this same element.
  
Any element that contains richer structured content will probably need a
custom template created.

Installation
------------

Download and extract the included files into your directory of choice.

CybOX-to-HTMl requires an XSLT 2.0 engine. We strongly encourage the use of 
[Saxon 9.x](http://saxon.sourceforge.net/), the engine that has been used for testing.

Usage
-----

The following commands assume you are using Saxon, and have Saxon's files stored in /opt/saxon. 
You may need to modify the commands to reflect your environment.

You can run the transform on a single file. <output file> will be created if it does not exist.

    java -jar /opt/saxon/saxon9he.jar -xsl:cybox_to_html.xsl -s:<input file> -o:<output file>

You can also run the transform on a directory of files, using the same syntax. The <output directory>
must exist before running the script.

    java -jar /opt/saxon/saxon9he.jar -xsl:cybox_to_html.xsl -s:<input directory> -o:<output directory>

### Example files

CybOX-to-HTML comes with example input and output files. You can use these to see an example
of the program's output, or to verify you have installed the program correctly.

    $ java -jar /opt/saxon/saxon9he.jar -xsl:cybox_to_html.xsl -s:examples/CybOX_Iran-Oil_Dynamic.in.xml -o:CybOX_Iran-Oil_Dynamic.out.html
    $ diff CybOX_Iran-Oil_Dynamic.out.html examples/CybOX_Iran-Oil_Dynamic.out.html
    
Contributing
------------

This is a work in progress.  Feedback is most welcome!

Bug reports and feature requests are welcome and encouraged. Pull requests are especially appreciated. 
Feel free to use the issue tracker on GitHub or send an email directly to <cybox@mitre.org>.

More information
----------------

* CybOX - http://cybox.mitre.org/
