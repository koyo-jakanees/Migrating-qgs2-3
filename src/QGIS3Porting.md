# QGIS3 Porting

Now that you are convinced that the quickest way is to continue supporting or using a plugin is to port to the recent supported
Long term or stable release of QGIS. You should have qgis plugin dev tools already installed in your system. At the very least you should have
```pyrcc5, pyuic5, git, IDE or text editor, qgis2to3``` ```QtDesigner tool``` to edit you UI forms.
**Note:** Editing of the UI forms might not be necessary when beginning unless you want to modify the graphical interface of the plugin.

Spend sometime scheming through the code repository  before trying to load it to qgis plugin folder. To understand not just the code, files structure but to familiarize. In QGIS2  the default plugin folder was in ```$HOME/.qgis2``` which  was changed to ```$HOME/user/.local/share/QGIS/QGIS3/profiles/default/python/plugins```
for  linux based systemsas for my scenario. It is important to note that the plugin folder location differs in other OS such as Windows and OSx.

## Getting the plugin code to your local filesystem

If you are planning to contribute your changes to the main upstream plugin repo then it is adviceable to keenly go through their contributing.md guides if there exists any.
Follow the usual git workflow. Fork the repository before cloning to your system

```bash
#Install qgis2to3 helper
$pip install qgis2to3 --user
#create your development directory
$mkdir plugin-dev && cd plugin-dev

#clone the forked plugin to your local file system
$git clone https://github.com/koyo-jakanees/oam-qgis-plugin
$cd oam-qgis-plugin

#fetch from the original repo incase changes might have been made in between
$git pull upstream

#Investigate the repo structure.
$tree .  

$cd OpenAerialMap

#Create a symlink to  point to qgis3 plugin folder
$sudo ln -sr ./ $HOME/.local/share/QGIS/QGIS3/profiles/default/python/plugins/OpenAerialMap
```

You should now be having a the plugin with a symlink/shortcut point to plugin folder. Let's get our hands dirty and break some things
