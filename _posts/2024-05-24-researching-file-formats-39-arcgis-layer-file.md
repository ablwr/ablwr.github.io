---
layout: post
title: "Researching file formats 39: ArcGIS Layer File"
date: 2024-05-24 09:00:00 -0500
tags: [file formats, fdds]
---

This blog post is part of a series on file formats research. See [this introduction post](https://bits.ashleyblewer.com/blog/2023/08/04/researching-file-formats-library-of-congress-sustainability-of-digital-formats/) for more information.

Update: The official format definition is now online here: [ArcGIS Layer File](https://www.loc.gov/preservation/digital/formats/fdd/fdd000626.shtml). [Comments welcome](https://www.loc.gov/preservation/digital/formats/contact_format.shtml) directly to the Library of Congress.

We've made it to the last file format!!!

Last but not least is ArcGIS Layer Files. They're a bit of a bonus 2-for-1 deal, too.

Layer files store all properties for a GIS "layer." It doesn't hold actual GIS data, but overlay data that goes on top of the GIS data. A bit meta, I guess. Symbols, classifications, properties, scale, definitions.

It's intended to be used with ArcGIS products, so ArcGIS's company, Ersi, doesn't have incentive to make it openly documented or work with any other products. More vendor lock-in. Since these files work with ArcMap and ArcGIS / ArcGIS Pro, typical warnings around software obsolescence apply here -- the files only have use within the context of this software. File conversion will be required to use with other software platforms, including those not yet built. This makes a little more sense than some of the other formats that are treated this way, since it is somewhat specific and only useful with this product. Open and fully documented is always better, but this is something that relatively doesn't get in the way of other things, in my opinion. It's made by the software and has a life in the software. I guess what I'm saying is that these are files that are meant to be used while working on things, like a middle-state production format, and aren't supposed to live a longer life beyond that unless converted to something else. 

Oh, what did I mean by being 2-for-1?

"Layer files authored with ArcGIS Desktop have a .lyr extension and layer files created with ArcGIS Pro have a .lyrx extension. There is a notable difference. Older .lyr files only store a single layer or a single group layer at the root level although a group layer can have multiple layers or group layers within it. Newer .lyrx files can store multiple layers and/or group layers at the root level. Therefore, a reference to a layer file will be a reference to a list of layers." ([source]((https://pro.arcgis.com/en/pro-app/latest/arcpy/mapping/layerfile.htm)))

If you are someone who likes to make [PRONOM](https://www.nationalarchives.gov.uk/PRONOM/) entries, you're in luck because this format does not have one! Get your name in there!