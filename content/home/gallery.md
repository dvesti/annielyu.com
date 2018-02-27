+++
# Custom widget.
# An example of using the custom widget to create your own homepage section.
# To create more sections, duplicate this file and edit the values below as desired.
widget = "custom"
active = true
date = "2018-02-26T22:00:00"
  
# Note: a full width section format can be enabled by commenting out the `title` and `subtitle` with a `#`.
title = "Gallery"
subtitle = ""
  
# Order that this section will appear in.
weight = 65
  
[[gallery_item]]
album = "1"
image = "gallery/Yellowstone.jpg"
caption = "Yellowstone Sep-04-2017"
  
[[gallery_item]]
album = "1"
image = "gallery/tree.jpg"
caption = "Page Sep-03-2017"

+++
    
{{< gallery album="1" >}}