# Rack
A rack for your [gun](https://github.com/amark/gun)

Rack is a tool for visualizing your Gun database as a force-directed graph.  
More info about Gun can be found on [Gun's GitHub](https://github.com/amark/gun) and on [Gun's website](https://gun.eco).  
If you're new to graph databases (or databases in general) a visual aid can be very helpfull in grasping underlying concepts.  
This is also how Rack was born; as a hands-on practice to gain some experience in basic graph/gun usage.

## Usage
Go to [billynate.github.io/rack](https://billynate.github.io/rack) to open up Rack. You'll see a blank canvas.  
By clicking anywhere on the canvas, a button will become visible and upon hitting the button you'll be able to create a new node.  
First the identifier of the node will have to be set (this can only be done on creation), then the attributes (key/value) can be added.  
Once you have multiple nodes, they can reference eachother by creating (or editing) an attribute and hitting the &#9671; button. Hitting a node now will create a reference and the button will turn into &#9094;.  
In order to remove an attribute from a node, the attribute's key needs to be emptied. There's a trashcan icon in the bottom right to remove a whole node. (Pay attention to the [caveats](#caveats) about deleting!)

## Caveats
Because Rack was only created as practice it remained rather unpolished. Also some work-arounds were used to get it working as intended.  
Obviously Rack is not meant for production, but may still be useful to anyone new to Gun or (graph) databases. There are some caveats you might want to know about though:
- User input is neither sanatized nor validated
- Data isn't actually removed on deletion, but instead a "tombstone" is set in place:
  - When removing an attribute, the value is actually set to `null`
  - When removing a node, all attributes are set to `null` and a new attribute is added with a key of `VOID`
- When a node is removed that is referenced by other nodes, the attributes that reference the removed node are left unchanged
- Some work arounds are used:
  - Nodes are loaded from localStorage on page load by [some hacked together code](https://github.com/BillyNate/rack/blob/master/index.html#L35). Other storage locations are _not_ checked.
  - Several properties of the Gun database are accessed instead of (or in absence of) the API: [`._.graph`](https://github.com/BillyNate/rack/blob/master/index.html#L522), [`.['#']`](https://github.com/BillyNate/rack/blob/master/index.html#L424), etc&hellip;

## Contribute
1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -m 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request :)

## Licenses
Licensed under the same licenses are Gun: [Zlib / MIT / Apache 2.0](https://github.com/BillyNate/rack/blob/master/LICENSE), just pick what you like.
