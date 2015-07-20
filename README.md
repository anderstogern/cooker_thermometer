# Cooker thermometer

Licenced under the Creative Commons Attribution-ShareAlike 3.0 Unported (CC BY-SA 3.0) licence:
http://creativecommons.org/licenses/by-sa/3.0/

*A wireless thermometer for barbecuing and smoking*

Um right, but what is it?
------------------------
The Cooker Thermometer can measure the temperatures of up to three different
pieces of meat. If you happen to have a smoker of some sort, e.g. the Weber
Smokey Mountain, it can also assist you in keeping the right temperature for
low-and-slow cooking by measuring the temperature at the top of the smoker.

The thermometer is wireless and transmits its measures using RF (434MHz RFM12B)
to a Raspberry Pi base station, which in turn stores the measures in a
database. The front-end is a custom Android app that handles sessions and reads
the measures from the database, presenting them with alerts and graphs.

How does it work, again?
------------------------
The Cooker Thermometer measures temperatures, transmits the
measures to a Raspberry PI that puts the measures in a database. Then the
Android app reads the measures from the database and acts on these according
to set thresholds, etc. in order to act as you would expect a thermometer for
cooking would.

### Please sir, I wan't some more

In more detail, the Cooker Thermometer is based on Nathan Chantrell's
[TinyTX](https://github.com/nathanchantrell/TinyTX)3 sensor node, which was
somehow the inspiration to the project.
The TinyTX3 is a tiny (yup, that's right!) RF sensor node based on the popular
(and now discontinued--replaced by [RFM69](http://www.hoperf.cn/upload/rf/RFM69-V1.3.pdf))
[RFM12B](http://www.hoperf.com/upload/rf/RFM12B.pdf) radio tranciever by
[HopeRF](http://www.hoperf.com/).

The TinyTX can interact with a number of sensors and transmit their measures
to a base station using the RFM12B. This base station needs to be within range
and work at the same frequency as the transmitter--normally it is based on a
RFM12B as well. In my case--and in most cases--the base sation is a Raspberry
PI with the [RFM12PI](http://wiki.openenergymonitor.org/index.php/RFM12Pi_V2)
(now replaced by [RFM69PI](http://wiki.openenergymonitor.org/index.php/RFM69Pi_V3))
expansion module from the [Open Energy Monitor Project](http://openenergymonitor.org).
That means that the sensor--and in this case the Cooker Thermometer--is not
portable outside the location that has the base station. A minor concern as
these things tend to be statically located.

Handling of the measures received by the RPI is done my EmonHub, which is
configured with a custom receiver to put the measures in a MySQL database (which
is located on a NAS, but could be running on the RPI).

That was basically the measuring part of the Cooker Thermometer. The
"monitoring" part is somewhat more complex as it is based solely on a custom
Android app, which handles defining limits and thresholds--based on meat type
and desired finish--and reading the measures from the database, showing them
with values and graphs as well as--finally--alerting when the meat is done or
overcooked, or the heat is too low or too high in the WSM.

I won't go into much detail about the Android app because it 1) is not finished
and 2) is very inefficient at times--although I have come a very long way with
it!

.. More info to come ..
