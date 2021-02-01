# Finding API v2 Usages

Congratulations on making it this far. There are two useful resources and/or tools that will help you in porting the Qgs API v2 used within the plugin code base

- [QGIS2API finder](https://github.com/opengisch/qgis2to3/tree/master/qgis2to3/api2finder) is bundled with qgis2to3 tool and will also be available
- [QGIS API break](https://qgis.org/api/api_break.html) API documentation details backword incompatible changes.

> The API of QGIS libraries is allowed to be changed just between major versions of QGIS. For example, there are various planned backwards incompatible changes between QGIS 1.8 and 2.0 because the version 2.0 is a new major version. After a release of a major version of QGIS (e.g. 2.0) the developer team is committed to maintain stable API for all subsequent minor releases (2.2, 2.4, ...). That roughly means we do not rename classes and methods, remove them nor change their semantics. Existing code should keep working when the user updates QGIS to another minor version (e.g. from 2.0 to 2.2), so all extensions of existing classes should be done in a manner that third party developers do not need to adjust their code to work properly with newer QGIS releases.
>
> Sometimes, however, we may need to break the API as a result of some code changes. These cases should be only exceptions and they should happen only after consideration and agreement of the development team. Backwards incompatible changes with too big impact should be deferred to a major version release.
>
> This page tries to maintain a list with incompatible changes that happened in previous releases.

Using the ``qgis2apifinder`` to find uses of api v2 in the code base and ``stdout`` potential required changes for the current version.

```bash
$qgis2apifinder  --all /path/to/plugin/folder

./OpenAerialMap/__init__.py::53: Found name -> ['(class QgsSimpleMarkerSymbolLayer) and setName() have been removed. Use shape() and setShape() instead.']
./OpenAerialMap/__init__.py::56: Found instance -> ['(class QgsAuthManager) was removed in favor of QgsApplication::authManager() that returns an instance of the Auth Manager']
./OpenAerialMap/plugin_upload.py::100: Found name -> ['(class QgsSimpleMarkerSymbolLayer) and setName() have been removed. Use shape() and setShape() instead.']
./OpenAerialMap/plugin_upload.py::115: Found name -> ['(class QgsSimpleMarkerSymbolLayer) and setName() have been removed. Use shape() and setShape() instead.']
./OpenAerialMap/set_env.py::26: Found map -> ['(class QgsMapCanvas) has been removed because QgsMapCanvasMap is not available in API anymore.']
./OpenAerialMap/set_env.py::97: Found map -> ['(class QgsMapCanvas) has been removed because QgsMapCanvasMap is not available in API anymore.']
./OpenAerialMap/oam_main.py::57: Found instance -> ['(class QgsAuthManager) was removed in favor of QgsApplication::authManager() that returns an instance of the Auth Manager']
./OpenAerialMap/oam_main.py::85: Found actions -> ['(class QgsDataItem) now requires a new QWidget parent argument. Subclasses should ensure that returned items have been']
./OpenAerialMap/oam_main.py::127: Found normal -> ['(class QgsVector) was removed. Use normalized() instead.']
./OpenAerialMap/oam_main.py::159: Found actions -> ['(class QgsDataItem) now requires a new QWidget parent argument. Subclasses should ensure that returned items have been']
```

As you can see from the terminal output the tool schemes through the whole plugin to find  v2 api uses and gives out suggestions  to the possible changes in v3. This is critical when hunting for this differences and minimizes time spent going through a whole file but jumping straight to the affected lines.
Using this tool alongside the QGIS api break wiki to refactor your code further
since the output of the tool is only available in the terminal it's a good option to stream it to a file like ``api2find.log.md`` for  futrue reference so that you don't have to run the command everytime you want to refactor or if in a new terminal session.

```bash
$qgis2apifinder --all /plugin/folder > ./api2find.log.md
```

If you are planning to maintain the plugin for future migrations keep checking the [Plugin Migration to QGIS3 wiki](https://github.com/qgis/QGIS/wiki/Plugin-migration-to-QGIS-3) for updated information and best practices when delving into this path.

## Extras

1. **CI/CD** [QGIS plugin CI](https://github.com/opengisch/qgis-plugin-ci)
2. **Submitting a pull request**
