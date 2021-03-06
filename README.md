Selleckt
===============

A select replacement, using mustache.js for templating.

[![Build Status](https://travis-ci.org/BrandwatchLtd/selleckt.png)](https://travis-ci.org/BrandwatchLtd/selleckt)

Running the demos
=================

Pull down the repo then execute:

    ./serve.sh

and open `http://localhost:8080/demo`


Running the tests
=================

Run
    npm install testem -g
    testem

Or pull down the repo then execute:

    ./serve.sh

and open `http://localhost:8080/test`


Configuration
=================

Selleckt enhances a standard html select element. It respects the 'multiple' attribute and instantiates a multiselleckt if that attribute is set.

The plugin uses mustache templates, so its style is highly customisable.

For example, for a select with id 'foo' to instantiate select simply:

```javascript
$('#foo').selleckt(options);
```

The element is enhanced, and selleckt is available via:

```javascript
var sellecktInstance = $('#foo').data('selleckt');
```

Options
=============

The following options can be passed to selleckt:


<table>
    <thead>
        <tr>
            <th>property</th>
            <th>type</th>
            <th>default value</th>
            <th>description</th>
        </tr>
    </thead>
        <tr>
            <td>mainTemplate</td>
            <td>string or compiled mustacheJs template function</td>
            <td>
                <a href="#templates">See below for default templates</a>
            </div>
            </td>
            <td>
            </td>
        </tr>
        <tr>
            <td>selectedClass</td>
            <td>string</td>
            <td>selected</td>
            <td>The css class name for the item that triggers the dropdown to show. It should also contain an area to show text (the placeholder, or the text of the current selection.
            </td>
        </tr>
        <tr>
            <td>selectedTextClass</td>
            <td>string</td>
            <td>-</td>
            <td>
                An element to show text (the placeholder, or the text of the current selection. This should be a child of the element defined in `selectedClass`.
            </td>
        </tr>
        <tr>
            <td>itemsClass</td>
            <td>string</td>
            <td>-</td>
            <td>
                The css class name for the container in which the available selections are shown.
            </td>
        </tr>
        <tr>
            <td>itemClass</td>
            <td>string</td>
            <td>-</td>
            <td>
                The css class name for the container for an individual item. This should be a descendent of the `itemsClass` element.
            </td>
        </tr>
        <tr>
            <td>className</td>
            <td>string</td>
            <td>dropdown</td>
            <td>
                Css class name for the whole selleckt.
            </td>
        </tr>
        <tr>
            <td>highlightClass</td>
            <td>string</td>
            <td>highlighted</td>
            <td>
                The css class name for the item currently highlighted via keyboard navigation/mouseover selleckt.
            </td>
        </tr>
        <tr>
            <td>itemTextClass</td>
            <td>string</td>
            <td>itemText</td>
            <td>
                The css class name for the text container inside the `itemClass` element.
            </td>
        </tr>
        <tr>
            <td>placeholderText</td>
            <td>string</td>
            <td>Please select...</td>
            <td>
                The text shown inside the selectedClass element when there is no item currently selected.
            </td>
        </tr>
        <tr>
            <td>enableSearch</td>
            <td>bool</td>
            <td>false</td>
            <td>
                If true, then this is used in conjunction with searchThreshold to determine whether to render a search input used to filter the items.
            </td>
        </tr>
        <tr>
            <td>searchInputClass</td>
            <td>string</td>
            <td>search</td>
            <td>
                The css class of the search input.
            </td>
        </tr>
        <tr>
            <td>searchThreshold</td>
            <td>number</td>
            <td>0</td>
            <td>
                 If the amount of items is above this number, and enableSearch is true then the search input will render.
            </td>
        </tr>
    <tbody>
    </tbody>
</table>

For multiselleckts, in addition to the above:

<table>
    <thead>
        <tr>
            <th>property</th>
            <th>type</th>
            <th>default value</th>
            <th>description</th>
        </tr>
    </thead>
        <tr>
            <td>selectionTemplate</td>
            <td>string or compiled mustacheJs template function</td>
            <td>
                <a href="#templates">See below for default templates</a>
            </td>
            <td>
                The template for rendering the individual selected items
            </td>
        </tr>
        <tr>
            <td>selectionsClass</td>
            <td>string</td>
            <td>
                selections
            </td>
            <td>
                The css class name for the container in which the selected items are shown.
            </td>
        </tr>
        <tr>
            <td>selectionItemClass</td>
            <td>string</td>
            <td>
                selectionItem
            </td>
            <td>
                The css class name for an individual selected item. Should be a descendent of the selectionsClass element
            </td>
        </tr>
        <tr>
            <td>alternatePlaceholder</td>
            <td>string</td>
            <td>
                Select another...
            </td>
            <td>
                Once a single selection is made, the 'placeholder' text will be replaced with this text.
            </td>
        </tr>
        <tr>
            <td>removeItemClass</td>
            <td>string</td>
            <td>
                remove
            </td>
            <td>
                Css class of the element used to trigger removal of a selectionItemClass element from the selectionsClass container.
            </td>
        </tr>
    <tbody>
    </tbody>
</table>

<a name="templates"></a>
Templates
=================

An example basic template:
````html
<div class="{{className}}" tabindex=1>
    <div class="selected">
        <span class="selectedText">{{selectedItemText}}</span><i class="icon-arrow-down"></i>
    </div>
    <ul class="items">
        {{#showSearch}}
        <li class="searchContainer">
            <input class="search"></input>
        </li>
        {{/showSearch}}
        {{#items}}
        <li class="item" data-text="{{label}}" data-value="{{value}}">
            <span class="itemText">{{label}}</span>
        </li>
        {{/items}}
    </ul>
</div>
````
An example template for multiselleckt:
````html
<div class="{{className}}" tabindex=1>
    <ul class="selections">
    {{#selections}}
    {{/selections}}
    </ul>
    <div class="selected">
        <span class="selectedText">{{selectedItemText}}</span><i class="icon-arrow-down"></i>
    </div>
    <ul class="items">
        {{#items}}
        <li class="item" data-text="{{label}}" data-value="{{value}}">
            {{label}}
        </li>
        {{/items}}
    </ul>
</div>
````
An example template for a multiselleckt item:
````html
<li class="selectionItem" data-value="{{value}}">
    {{text}}<i class="icon-remove remove"></i>
</li>
````