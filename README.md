# FME® UTMZoneDetector
## About
This transformer tries to find a fitting UTM zone for an input feature. It also outputs the hemisphere and a matching WGS84 coordinate system name, suitable for FME's [Reprojector](https://www.safe.com/transformers/reprojector/) or [CoordinateSystemSetter](https://www.safe.com/transformers/coordinate-system-setter/), for instance.

If a fitting zone was found, 3 attributes will be added to the feature:  
- _\_utm.hemisphere_ ("S" or "N")  
- _\_utm.zone_ (an integer ranging from 1 to 60)  
- _\_utm.coordsys_ (a matching WGS84 UTM coordinate system name)

No actual reprojection takes place on the output feature. The transformer should be able to deal with rasters and various kinds of vector geometry. Note however that this transformer does not check if the _whole_ feature is inside a zone. It merely checks if the "inside point" (or center point if that failed) of the feature belongs to a certain zone. This is why this transformer should not be used on really large features that span multiple zones, like continent or country boundaries.

If the zone could not be retrieved, e.g. when the feature has a missing coordinate system or when the feature is outside the valid latitudinal UTM bounds of {-80, 84}, it will be rejected and a _\_utm.error_ attribute will be added.

### Notes  
- Also available on [FME Hub](https://hub.safe.com/transformers/utmzonedetector) for convenient installation.  
- This transformer has been tested on Python 2.7 and 3.4.  
- Released under [GNU General Public License v3.0](https://github.com/SanderSchaminee/fme-utmzonedetector/blob/master/LICENSE).  
- If you notice a bug or desire a new feature, please contact me. Or make a pull request!  
- The [test workspace](https://github.com/SanderSchaminee/fme-utmzonedetector/blob/master/UTMZoneDetectorTest.fmwt) is used for testing and provides some examples.
