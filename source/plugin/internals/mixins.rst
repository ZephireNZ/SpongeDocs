=============
Plugin Mixins
=============

`Mixins <https://github.com/SpongePowered/Mixin>`_ can be used to modify classes at runtime before they are loaded. You
can use them in plugins if you want to optimize a part of the game specifically for your server - without having to fork
Sponge. The modifications will be bundled directly with your plugin and are only active as long as the plugin is loaded.

Refer to the `Mixin documentation <https://github.com/SpongePowered/Mixin/wiki>`_ for more information on how to use
mixins. This article explains how to bundle Mixins with plugins.

Setup
-----
#. Add the Mixin library as dependency to your plugin:

    .. code-block:: groovy

        dependencies {
            compile 'org.spongepowered:mixin:0.5.10-SNAPSHOT'
        }

#. Add a new Mixin configuration for your plugin, e.g. ``mixins.myplugin.json`` inside your resource folder:

    .. code-block:: json

        {
            "package": "com.example.myplugin.mixin",
            "refmap": "mixins.myplugin.refmap.json",
            "target": "@env(DEFAULT)",
            "compatibilityLevel": "JAVA_8",
            "server": [
                "MixinMinecraftServer"
            ],
            "injectors": {
                "defaultRequire": 1
            }
        }

#. Add the Mixin class to the specified package

Debugging
`````````
Normally, the Mixin configuration is registered inside the plugin's JAR manifest. Since the plugin is not packaged in a
JAR while debugging inside the IDE you need to add the Mixins to apply manually as command line options.

Add a ``--mixin <mixin config file name>`` option for each Mixin configuration file to the program arguments of your run
configuration, e.g. ``--mixin mixins.myplugin.json``.

Production
``````````
You need to make some changes to your build script to be able to apply your Mixin in production:

#. Apply the MixinGradle plugin to your build script:

    .. code-block:: groovy

        buildscript {
            repositories {
                maven {
                    name = 'sponge'
                    url = 'http://repo.spongepowered.org/maven'
                }
            }
            dependencies {
                classpath 'org.spongepowered:mixingradle:0.4-SNAPSHOT'
            }
        }

        apply plugin: 'org.spongepowered.mixin'

#. Set the Minecraft tweak class to the Mixin tweaker:

    .. code-block:: groovy

        minecraft {
            tweakClass = 'org.spongepowered.asm.launch.MixinTweaker'
        }

#. Set the refmap you added before in your Mixin configuration:

    .. code-block:: groovy

        sourceSets {
            main {
                refMap = "mixins.pluginmixintest.refmap.json"
            }
        }

#. Add your Mixin configuration to your JAR manifest. The ``FMLCorePluginContainsFMLMod`` manifest entry is necessary if
you want to load your Mixin on SpongeForge:

    .. code-block:: groovy

        jar {
            manifest {
                attributes(
                        'MixinConfigs': 'mixins.myplugin.json',
                        'FMLCorePluginContainsFMLMod': 'true',
                )
            }
        }

#. Make sure to re-build the plugin using the ``build`` Gradle task. Your Mixin should now be applied by SpongeVanilla
and SpongeForge.
