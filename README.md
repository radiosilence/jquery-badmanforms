BADMAN FORMS
============

Just some little useful things to make forms either prettier or to make working
with them less awful.

All visual modification falls back gracefully an ting.

SELIMIT
-------

This be a function to limit one dropdown based on another, using a
pre-generated object to look up what objects are supposed to be "assigned" to
what.

For instance, contacts and companies. You have two drop downs, one of
companies, the other of contacts, and you only want the second to display
contacts that are in the company selected by the company in the first dropdown.

    <select name="company">
        <option val="1">Derpcorp</option>
        <option val="2">Pugg Ltd.</option>
    </select>

    <select name="contact">
        <option val="1">Timmy Octopus</option>
        <option val="2">Sausage McWarble</option>
        <option val="3">Johnny Five-Aces</option>
    </select>

We must then represent represent the data of who is in what company, so say
Timmy and Johnny were in Pugg Ltd. and Sasuage was in Derpcorp, we'd need an
object like this:

    var employees = {
        1: [2],
        2: [1, 3]
    }

It is simply the company IDs with a list of employee IDs. You could generate
this using backend code and insert it into your template or whatever you want.

Then, we initialise the plugin on page load:

    $(function() {
        $('select[name=company]').selimit(
            employees,
            'select[name=contact]'
        );
    })

And it is done.

There is one more advanced use case, however, for dealing with situations where
there may be more than one "set" of selects, such as a list view.

Say the layout was a table like this:

    <tr>
        <td>
            <select name="company">
                ...
            </select>
        </td>
        <td>
            <select name="contact">
                ...
            </select>
        </td>
    </tr>
    <tr>
        ...
    </tr>

There is a third option we can pass - a selector for the "parent" that binds
"sets" of selects together like this:

    $(function() {
        $('select[name=company]').selimit(
            employees,
            'select[name=contact]',
            'tr'
        );
    })

Similar thing could be done for things like fieldsets, divs, etc.


CHECKGROUP
----------

This simply converts a boring, ugly multiple select field into a beautiful
group of checkboxes.

Use it like:

    $('select.blah').checkgroup();


MULTIFILTER
-----------

Similar to above, however instead of checkboxes, this converts a multiple
select into what appears to be an empty select box. When something is, however,
selected in that box...another select box appears! If a select box is made
blank (select the "default" item), or the X next to it is pressed, it
disappears, leaving only the remaing selected items.

Use it like:

    $('select.blah').multifilter();


OH BTW: Both this and checkgroup work totally A++ if there are already selected
items for whatever selects they are replacing.