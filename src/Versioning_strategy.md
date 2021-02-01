# Source Code Versioning

Before you start editting the source files of the plugin, it's good practice to branch out the current *main* branch to a another branch e.g 'Legacy' or 'api v2'
off the main. For example

```bash
$git checkout -b API_V2
```

Remember the final goal is to have an updated main branch that is compatible with QGIS api3. So go ahead and create a new  branch(the one will be using to experiment and port) before merging back to main.
Same as before but name the new branch with self describing name e.g 'upgrade_2_to_v3'

```bash
$git checkout -b upgrade_2_to_v3
```

After ensuring the legacy code stays in its own branch and now we're working on the feature branch ``upgrade_2_to_v3``, It's time to start fixing the imports in individual python files.
