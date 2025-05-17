Tool Webber
SRL webber with WaspLib maps.

Run it to launch the tool. This is the tool used to maked TRSWalker WebGraphs. You can read more about web graphs online but it’s basically an array of nodes (or points) and connections between them. This is what TRSWalker uses to follow certain paths when you use TRSWalker.WebWalk().

Further usage instructions are displayed in Simba’s output when you run the tool.

When you finish your webgraph, keep in mind you need to print it, copy it from the Simba output and paste it into an empty .graph file that you have to include in your script later.

You can then set TRSWalker.WebGraph := MyCustomGraph with whatever name you gave it.

If you want to edit WaspWeb you need to open Simba/Includes/WaspLib/osr/walker/waspweb.graph and replace it’s contents. Keep in mind that unless you send a PR with your additions, they will be lost with WaspLib updates.

const OFFSET_POINT

Optional offset for the webgraph. Can be handy.
