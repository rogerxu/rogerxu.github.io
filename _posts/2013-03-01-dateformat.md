---
layout: post
title: Date Format
---

# ISO8601

[W3C Date and Time Formats](http://www.w3.org/TR/NOTE-datetime)


    Year:
        YYYY (eg 1997)
    Year and month:
        YYYY-MM (eg 1997-07)
    Complete date:
        YYYY-MM-DD (eg 1997-07-16)
    Complete date plus hours and minutes:
        YYYY-MM-DDThh:mmTZD (eg 1997-07-16T19:20+01:00)
    Complete date plus hours, minutes and seconds:
        YYYY-MM-DDThh:mm:ssTZD (eg 1997-07-16T19:20:30+01:00)
    Complete date plus hours, minutes, seconds and a decimal fraction of a second
        YYYY-MM-DDThh:mm:ss.sTZD (eg 1997-07-16T19:20:30.45+01:00)

## Java

### Joda DateTime

    new org.joda.time.DateTime(0).toString()                                    // "1970-01-01T08:00:00.000+08:00"

### Jackson

    Date epoch = new Date(0);
    com.fasterxml.jackson.databind.util.ISO8601DateFormat.format(epoch)         // "1970-01-01T00:00:00Z"
    com.fasterxml.jackson.databind.util.StdDateFormat.format(epoch)             // "1970-01-01T00:00:00.000+0000"

### Apache Commons Lang 3

    org.apache.commons.lang3.time.FastDateFormat ISO_DATETIME_TIME_ZONE_FORMAT = org.apache.commons.lang3.time.DateFormatUtils.ISO_DATETIME_TIME_ZONE_FORMAT;
    ISO_DATETIME_TIME_ZONE_FORMAT.format(epoch)                                 // "1970-01-01T08:00:00+08:00"

## JavaScript

    var epoch = new Date(0);
    epoch.toISOString()                                                         // "1970-01-01T00:00:00.000Z"
    epoch.toJSON()                                                              // "1970-01-01T00:00:00.000Z"

### UI5

* "z": "timezoneGeneral"
* "Z": "timezoneRFC822"
* "X": "timezoneISO8601"

Example:

    var pattern = {};
    pattern["timezoneGeneral"] = "yyyy-MM-dd'T'HH:mm:ss.SSSz";
    pattern["timezoneRFC822"] = "yyyy-MM-dd'T'HH:mm:ss.SSSZ";  // e.g. -0200 or +0200
    pattern["timezoneISO8601"] = "yyyy-MM-dd'T'HH:mm:ss.SSSX"; // e.g. -02:00 or +02:00

    var epoch = new Date(0);
    var DateFormat = sap.ui.core.format.DateFormat;
    DateFormat.getDateTimeInstance(pattern["timezoneGeneral"]).format(epoch);   // "1970-01-01T08:00:00.000GMT+08:00"
    DateFormat.getDateTimeInstance(pattern["timezoneRFC822"]).format(epoch);    // "1970-01-01T08:00:00.000+0800"
    DateFormat.getDateTimeInstance(pattern["timezoneISO8601"]).format(epoch);   // "1970-01-01T08:00:00.000+08:00"


# RFC822
