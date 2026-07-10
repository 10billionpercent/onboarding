# Critical Rendering Path

Critical rendering path is the sequence of steps followed by the browser to display a webpage on the screen.

## Steps

- Browser recieves HTML from the server through an HTTP request.
- TThe HTML tags are parsed one by one to create the nodes of the DOM tree. Each node in this tree has a startTag and endTag. If the browser encounters a resource (such as stylesheets, images etc) it has not obtained, it makes HTTP requests to download it. Sometimes these requests can be blocking, ie halt the creation of the DOM tree.
- Next the browser creates the CSSOM tree from all the stylesheets. This is similar to DOM tree, but for CSS. It is not created incrementally like the DOM tree because CSS can be overridden by using more specific selectors later on in the stylesheet. This process is render blocking because the page cannot be rendered until the CSSOM has been created (since the broswer needs to know how to style the page). More specific selectors take longer to process, but it is still usually very fast.
- Next the browser applies any JavaScript that modifies either the DOM or CSSOM.
- Next the browser combines the DOM and CSSOM trees to create the render tree, which contains only the visible content. Nodes with `display: none;` and their children are not included in this tree.
- Next the browser performs layout, which is the process of determining how and where the elements should be placed on the page. It calculates the width, height and relative position of each element with respect to each other. Layout takes longer when the DOM tree has a larger number of nodes. This process happens each time the render tree is modified.
- Then the browser paints the pixels in memory  using the layout calculations, and performs compositing (combining layers).
- Finally the browser paints the pixels onto the screen. The complete page is painted only on load, and after that, only the changed parts are repainted. Painting is a very fast process in general, but depends on what is changing in the render tree.