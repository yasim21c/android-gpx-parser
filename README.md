Android GPX Parser
=======

A library to parse XML Gpx files, built for Android.
Far from complete, pull requests are welcome.

Download
--------

Grab via Gradle:

```groovy
compile 'io.ticofab.androidgpxparser:parser:0.1.1'
```

or Maven:
```xml
<dependency>
  <groupId>io.ticofab.androidgpxparser</groupId>
  <artifactId>parser</artifactId>
  <version>0.1.1</version>
</dependency>
```

Dependencies
------------

[Joda DateTime for Android][1]
Google Play Services, [Maps module][2] - only for the LatLng object. I'm considering removing it.

Usage
-----

Get a parser instance:

```java
GPXParser mParser = new GPXParser(); // consider injection
```

Then there are two options: given an InputStream,

```java
try {
    InputStream in = getAssets().open("test.gpx");
    parsedGpx = mParser.parse(in);
} catch (IOException | XmlPullParserException e) {
    e.printStackTrace();
}
```

or you might want to fetch the Gpx track from a server and parse it. In that case, pass the track Url and a listener:

```java
mParser.parse("http://myserver.com/track.gpx", new GPXParser.FetchAndParseGpxTask.GpxFetchedAndParsed() {
            @Override
            public void onGpxFetchedAndParsed(Gpx gpx) {
                if (gpx == null) {
                    // error parsing track
                } else {
                    // do something with the parsed track
                }
            }
        });
```

License
--------

    Copyright 2015 Fabio Tiriticco

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

[1]: https://github.com/dlew/joda-time-android
[2]: https://developers.google.com/android/guides/setup
