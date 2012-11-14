---
layout: post
title: GIS Vendors
---

# GIS Vendors

## SAP Geo-Map Integration Solution

### SAP TM

[Geo-Map Integration](https://wiki.wdf.sap.corp/wiki/display/SAPTM/Geo-Map+Integration)

[TM Geo-Map FAQ](https://wiki.wdf.sap.corp/wiki/display/SAPTM/TM3+-+FAQ#TM3-FAQ-GeoMap)

[Geo-Map @ SAP TM](https://wiki.wdf.sap.corp/wiki/display/SAPTM/TM+Geo-Map)

#### History
1. SAP TM 6.0 - built-in IGS framework within SAP APO / TPVS
  * difficult server setup
  * GIS vendors limited
  * missing interaction capabilities
2. SAP TM 7.0 - SAP Visual Business 1.0
3. SAP TM 8.0 - SAP Visual Business 1.1 - NAVTEQ
4. SAP TM 9.0 - SAP Visual Business 2.0 - HTTP requests based GIS vendors

#### Summary

SAP TM => SAP Visual Business => 3rd party GIS Vendor

* SAP Visual Business takes over all GIS related responsibilities.
* For the displayed content, which must be provided by a GIS vendor, the customer must make separate contracts.

Limitations:

* The Visual Business front-end component must be installed on the client.
* The Visual Business component can be [used in a HTML page][1] but it is using ActiveX technology.

[1]: https://wiki.wdf.sap.corp/wiki/display/VisualBiz/Creating+a+HTML+Application "Creating a HTML Application with Visual Business Component"

#### GIS Vendors

[GIS Service Provider](https://community.wdf.sap.corp/sbs/groups/gis4saptm?#/?tagSet=19022)

* NAVTEQ
* PTV
* ALK

### SAP CVOM

Currently they use NAVTEQ to build Geo Map. They will support more providers in the coming several months.

#### NAVTEQ

[Demo](http://shg-cvom-build3.dhcp.pgdev.sap.corp:8080/job/html5_viz_trunkdev_build/lastSuccessfulBuild/artifact/bin/cvom.riv.html5.viz/examples/index.html)

* 3 Geo charts integrated.
* No street level geo data.

#### Google Maps

Not available due to legal issues.

#### ESRI

The next candidate for CVOM GIS vendor. They are waiting for the ESRI deal formalized later this month. After the ESRI deal completes, then we would be able to use the ESRI JavaScript APIs in the CVOM based solution.

This deal does not include the maps, only the APIs as described at [ArcGIS API for JavaScript](http://help.arcgis.com/en/webapi/javascript/arcgis/).

The ESRI API supports connecting to Google Maps, ESRI and OpenStreetMaps. [ArcGIS Services Directory](http://server.arcgisonline.com/ArcGIS/rest/services)

They plan to support multiple providers, although the exact timeline has not been confirmed.


