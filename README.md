Yggdrasil
===
Dumb "tree-based" programming language

Theory
===
Everything in this programming language operates on a giant node-tree.

Variables are declared by *pushing* new nodes onto the tree.  
Variables are acessed by *grabbing* those nodes, and getting their stored values.

    // Declare foo.
    <- foo;

That will *push* a new node called *foo* onto the tree.

    // Get foo's value.
    -> foo $ val;

That will *grab* the first node called *foo* and return its value.  
But wait a minute! *foo* has no value, so it returns *nil*! We should do this first:

    // Construct foo.
    -> foo[12];

That will set *foo*'s value to be 12.

You can also make your own trees. Just push a new node onto another node!

    // Make a new node.
    <- root;
    
    // Attach some new nodes to this root.
    root <- foo;
    foo[34];
    root <- bar;
    bar[17];
    root <- qux;
    qux[96];

You can also do this:

    // Make a new node.
    <- root;
    
    // Construct
    -> root
    [
        <- foo[34];
        <- bar[17];
        <- qux[96];
    ];

To access the nodes (and their values) in *root*, do this:
    
    // Access their values.
    -> root -> foo $ val; // Returns 34.
    -> root -> bar $ val; // Returns 17.
    -> root -> qux $ val; // Returns 96.

However, you cannot assign a *val* to *root* because it's "value" is its children.

    // This is no good.
    -> root[33];

That will overwrite foo, bar, and qux. In addition, you will no longer be able to reference them or their values, so it'll cause memory leaks!

To delete something, do this:

    // Push foo into the _trash.
    -> _trash <- foo;

First we *grab* _trash from the global tree, then *push* foo into it. That will immediately delete it and any value it has. You can't get it back out of the trash, though! That would be gross.

    // Eww! No way!
    -> _trash -> foo $ val;

There are also some shorthand ways of writing this code to make your life easier.

    // This is can be shortened...
    -> foo $ val;
    
    // ...into this!
    foo;
    
    // And this can be shortened...
    <- foo;
    -> foo[17];
    
    // ...into this...
    <- foo
    foo[17];
    
    // ...or this!
    <- foo[17];


    
