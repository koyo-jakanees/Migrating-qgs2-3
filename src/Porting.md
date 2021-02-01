# Porting API v2 to API v3 python, PyQt4 to PyQT5

Assuming you already have the ```qgis2to3``` installed in your system and is callable from the Command Line Interface(CLI)

```bash
# check the documentation of the tool and help message
$qgis2to3 --help

Usage: 2to3 [options] file|dir ...

Options:
  -h, --help            show this help message and exit
  -d, --doctests_only   Fix up doctests only
  -f FIX, --fix=FIX     Each FIX specifies a transformation; default: all
  -j PROCESSES, --processes=PROCESSES
                        Run 2to3 concurrently
  -x NOFIX, --nofix=NOFIX
                        Prevent a transformation from being run
  -l, --list-fixes      List available transformations
  -p, --print-function  Modify the grammar so that print() is a function
  -v, --verbose         More verbose logging
  --no-diffs            Don't show diffs of the refactoring
  -w, --write           Write back modified files
  -n, --nobackups       Don't write backups for modified files
  -o OUTPUT_DIR, --output-dir=OUTPUT_DIR
                        Put output files in this directory instead of
                        overwriting the input files.  Requires -n.
  -W, --write-unchanged-files
                        Also write files even if no changes were required
                        (useful with --output-dir); implies -w.
  --add-suffix=ADD_SUFFIX
                        Append this string to all output filenames. Requires
                        -n if non-empty.  ex: --add-suffix='3' will generate
                        .py3 files.
```

The tool works both with directories and individual files.
Invoking or calling the porting help from your terminal or OSGeo4W shell in your plugin folder.

```bash
$qgis2to3 -w /path/plugin/folder

/home/user/.local/bin/qgis2to3 -w /home/user/Documents/osGeoLive/salientrobot-dev/oam-qgis-plugin/OpenAerialMap
RefactoringTool: Skipping optional fixer: idioms
RefactoringTool: Skipping optional fixer: ws_comma
RefactoringTool: Refactored /home/user/Documents/osGeoLive/salientrobot-dev/oam-qgis-plugin/OpenAerialMap/make_package.py
RefactoringTool: Refactored /home/user/Documents/osGeoLive/salientrobot-dev/oam-qgis-plugin/OpenAerialMap/oam_main.py
RefactoringTool: Refactored /home/user/Documents/osGeoLive/salientrobot-dev/oam-qgis-plugin/OpenAerialMap/plugin_upload.py
RefactoringTool: Refactored /home/user/Documents/osGeoLive/salientrobot-dev/oam-qgis-plugin/OpenAerialMap/set_env.py
RefactoringTool: Refactored /home/user/Documents/osGeoLive/salientrobot-dev/oam-qgis-plugin/OpenAerialMap/backup_files/backup_backup_img_uploader_wizard.py
--- /home/user/Documents/osGeoLive/salientrobot-dev/oam-qgis-plugin/OpenAerialMap/make_package.py(original)
+++ /home/user/Documents/osGeoLive/salientrobot-dev/oam-qgis-plugin/OpenAerialMap/make_package.py(refactored)
@@ -1,3 +1,4 @@
+from __future__ import print_function
 import os, sys
 
 
--- /home/user/Documents/osGeoLive/salientrobot-dev/oam-qgis-plugin/OpenAerialMap/oam_main.py(original)
+++ /home/user/Documents/osGeoLive/salientrobot-dev/oam-qgis-plugin/OpenAerialMap/oam_main.py(refactored)
@@ -22,33 +22,34 @@
  ***************************************************************************/
  This script initializes the plugin, making it known to QGIS.
 """
+from __future__ import absolute_import
+from builtins import str
+from builtins import object
 
 # Qt classes
 # from PyQt4.QtCore import *
 # from PyQt4.QtGui import *
 # from qgis.core import *
 
-from PyQt4.QtCore import (QSettings,
-                          QTranslator,
-                          qVersion,
-                          QCoreApplication)
-from PyQt4.QtGui import (QAction, QIcon)
+from qgis.PyQt.QtCore import QSettings, QTranslator, qVersion, QCoreApplication
+from qgis.PyQt.QtWidgets import QAction
+from qgis.PyQt.QtGui import QIcon
 
 # icon images
 import resources_rc ......
 
```

The ``-w`` option tells the tool to write back the modified files. You'll notice that the tool also adds some python built-in modules e.g ```from __future__ import print_function```
Don't be scared this comes about when refactoring ``py2`` to ``py3`` code.

This function will also ``stdout`` the changes the tool made to each file in ``git style`` indicating the changed lines from which v2 api to which corresponding v3 api.
At this point if the imports and porting worked out fine you should be able to load the plugin widgets and controls to the ```QgsInterface``` instance/session.
Next steps involves refactoring the api v2 used that the tool could not find quick fix {Mainly QGIS api which makes the logic/control of the plugin}. Unfortunately this is the boring part and requires a little bit of patience,  don't be hard on yourself you have reached this far.
