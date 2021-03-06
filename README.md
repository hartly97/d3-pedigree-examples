# d3-pedigree-examples

Examples of how to create traditionally styled family pedigrees with [D3](http://d3js.org/). 

When I started learning how to draw pedigrees with D3, I had difficulty mixing and 
matching techniques from different examples and separating the basics from the fancy 
stylistic additions. Hopefully by showing the basics and how to incrementally add
advanced features, you won't have to become an expert in D3 just to draw a pedigree.

My requirements were:

* A tree with __square boxes and straight connecting lines__. Most D3 tree examples
  used circles for nodes and curved connecting lines.
* There needed to be a __fixed distance between generations__. By default, D3 trees
  fill up all the available space given to them.
* The tree needed to be __expandable and collapsible__.
* Need a way to display both __ancestors and descendants__.
* __Pan and zoom__.

### Examples

* __[Basic](http://justincy.github.io/d3-pedigree-examples/basic.html)__: A basic static pedigree.
* __[Expand and Collapse](http://justincy.github.io/d3-pedigree-examples/expandable.html)__: Click on persons to expand and collapse the tree.
* __[Smooth Transitions](http://justincy.github.io/d3-pedigree-examples/transitions.html)__: Changes are animated when the tree is expanded or collapsed.
* __[Ancestors and Descendants](http://justincy.github.io/d3-pedigree-examples/descendants.html)__: Show both ancestors and descendants.
* __[Ancestors and Descendants - OOP](http://justincy.github.io/d3-pedigree-examples/descendants-oop.html)__: A more sane example of ancestors and descendants using classes.

#### Notes

* Pan and zoom via the mouse are enabled in all examples.

* In the code you'll often see the variable `d` as the only parameter of an
  anonymous function. `d` is a D3 convention that stands for 
  [data](https://github.com/mbostock/d3/wiki/Selections#data).

* D3 tree layouts are configured for top -> bottom displays. We want a left -> right
  display so the x and y coordinates are flipped for nodes and links only. This is
  made even more complicated by svg using screen coordinates instead of cartesian
  coordinates.

  Say D3 calculates that a root node will be displayed at `(10,10)` with a child
  below it at `(10,20)`. We switch the x and y which leaves the root at `(10,10)`
  but moves the child to `(20,10)` which is now to the right. This gives us the
  traditional left to right ancestral pedigree view.
  
  To display descendants we swap the x and y then negate the x value which puts
  child nodes at the left.
  
* You have to draw two different trees in order to display both ancestors and
  descendants which dramatically increases the complexity. I strongly suggest
  an OOP approach if you need to do that. As you can see in the source code, it
  gets pretty hairy otherwise.

* Displaying formatted text in SVG can be a pain because you have little control.
  There is no built-in way to do text wrapping and you also can't easily
  style one word or phrase in a sentence. To get around these limitations you
  could use a [`foreignObject`](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/foreignObject)
  to display HTML and have all the formatting tools of CSS. However, `foreignObject`
  is not supported by any version of IE (11 is the latest at the time of writing).
  If you need to support any version of IE then you need to stick with pure SVG.
  Since we're using D3 we can use the handy [D3plus](http://d3plus.org/) library
  to help with [text wrapping](https://github.com/alexandersimoes/d3plus/wiki/Text%20Wrapping).