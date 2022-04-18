# trufi-server-modules

A repository as a recipe to create your own production backend environment which powers your very own version of Trufi App. This only contains the services which actually **consume & serve but <u>do not create</u>**

- the search index (consumed by extension `photon`)
- the mbtile (map tiles for your region) (consumed by extension `tileserver`)
- the static png tiles for your region) (consumed by extension `static_maps`)
- the routing graph (consumed by extension `otp` - **O**pen**T**rip**P**lanner )

and of course Nginx which combines these extensions to one service to make them appear as *one* with *one* HTTPS certificate, web identity and url scheme.

If you actually need to create the stuff e.g. the mbtiles or the graph you better go to [Trufi Server Resources](https://github.com/trufi-association/trufi-server-resources).


## Concept

This repository contains a bunch of service „extensions“ rather than just one big service containing everything. This allows a community to just run what they need using nginx as web proxy. Each "extension" has a specified job and contains a README.

## Extensions

You can find all in the [root](.) folder. Each extension has a README file with more detailed info.

- **[otp](./otp)**
  This is [OpenTripPlanner](https://opentripplanner.org) used to calculate the best route for the user of the app. *This service is mandatory for the app to work.*
- **[photon](./photon)**
  This is [Photon by Komoot](https://photon.komoot.io) used to provide online search results inside the app when the user searches for a POI to navigate from or to using public transportation. *This service is optional and but in case you **don't** use it you need to build the search index on the frontend site and only @SamuelRioTz knows how that works.*
- **[static_maps](./static_maps)**
  Use this service to serve pre-generated background map tiles. *This use of the service is optional but we recommend it if you have a server which is less in resources.*
- **[tileserver](./tileserver)**
  Use this service to serve the data needed to display the background map shown in the app. This does not include the styling (e.g. a highways are yellow lines and the water blue). The styling is done on the client side.  This allows you/us to make modifications to the stylings without the need to rerender all pngs of the background map for your city. It generates the png background map tiles on the fly for clients which do not support dynamic map tiles. *This use of the service is optional and cause much CPU usage when it needs to generate background maps on the fly (this is a wrong usage of this service). Our app currently does not support client side rendering of background maps so we only recommend using this service on a server with much CPU resources.*

Concerning background map tiles: Decide wethever you want to use the extension *static_maps* or *tileserver*. Using both is useless.
