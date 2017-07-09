# Was macht Java auf dem Client?
## Talks
- Podiumsdiskussion "Was macht Java auf dem Client?", Anton Epple, Hendrik Ebbers

## Content
- no "talk" in classical sense, more a discussion / asking questions to Anton and Hendrik
- perception: web often perceived as more interesting for frontend developers. However: every x days new releases, everything unstable. Release cycles too short. Not viable for projects because not sure how long used frameworks will work / survive next update
- perception: JavaFX not developed further by Oracle. Answer of Hendrik and Anton: Young framework + important functionality added (for example WebView and accessibility functions in Java 8). Also, in Java 9 modularity: JavaFX will be separated into 3 modules.
- Hendrik: "I don't miss anything in JavaFX" => Well, true. What else could there be to wish  for?
- web development: traditional separation of designers and developers. In FX, developers have to write both design and code. => In the early days, FX was promised to have a separation of both, so designers can create fxml-files and developers can work on functionality. => Hendrik: "I think the separation of designer and developer works great in JavaFX", however it's not practiced very well ("wird nicht gelebt"). Suspected reason: Designer has to leave his comfort zone and install FX-Designer - "Daran scheitern viele"
- demonstration of JProIO (running FX in browser, state is on the server)
- Gluon makes FX mobile with special controls => Hendrik: "One fits all" doesn't exist! Desktop + Smart Watch + Mobile + Holo Lens and others cannot be developed in one framework => specialization = better user experience and performance
- Github: cannoo/dolphin-platform = open source
    - client in FX and AngularJS
    - model shared between FX, Angular, Polymer, ...
    - logic completely server-side, client only for rendering
- duke script: pure client technology: Writing Java, rendering HTML => TODO have a look at that

## Tasks
