====================
Using MCP in plugins
====================

ForgeGradle_ is a Gradle plugin which integrates the MCP workflow into the Gradle build system. It handles setting up
the workspace, as well as the re-obfuscation of your plugin.

.. note::
    Since ForgeGradle depends on Gradle the following pages assume you are using Gradle to build your plugin. See
    :doc:`../project/gradle` to get started.

Configuring ForgeGradle
-----------------------
You can choose between two different kinds of workspaces:

- **Vanilla workspace:** You should use this if you want to support SpongeVanilla **and** SpongeForge.
- **Forge workspace:** Only use this if you do **not** want to support SpongeVanilla (**only** SpongeForge).

.. tip::
    In most cases, the Vanilla workspace can be used for SpongeVanilla and SpongeForge. In some cases, there may be
    problems on one of the platforms because of changes in the Minecraft code by Forge. Make sure to always test your
    plugin on both platforms when using MCP.

Vanilla workspace
`````````````````
.. code-block:: groovy

    buildscript {
        repositories {
            maven {
                name = 'forge'
                url = 'http://files.minecraftforge.net/maven'
            }
            maven {
                name = 'minecrell'
                url = 'http://repo.minecrell.net/releases'
            }
        }

        dependencies {
            classpath 'net.minecraftforge.gradle:ForgeGradle:2.2-SNAPSHOT'
            classpath 'net.minecrell:VanillaGradle:2.0.3_1'
        }
    }

    plugins {
        id 'org.spongepowered.plugin' version '0.6'
    }

    apply plugin: 'net.minecrell.minecraft.server.library'

    minecraft {
        version = '1.10.2'
        mappings = 'snapshot_xxx' // TODO
    }

Forge workspace
```````````````
.. code-block:: groovy

    buildscript {
        repositories {
            maven {
                name = 'forge'
                url = 'http://files.minecraftforge.net/maven'
            }
        }

        dependencies {
            classpath 'net.minecraftforge.gradle:ForgeGradle:2.2-SNAPSHOT'
        }
    }

    plugins {
        id 'org.spongepowered.plugin' version '0.6'
    }

    apply plugin: 'net.minecraftforge.gradle.forge'

    minecraft {
        forgeVersion = '1944' // TODO
        mappings = 'snapshot_xxx' // TODO
    }

Setting up the workspace
------------------------
Everytime you update the Minecraft or mappings version, or want to re-import your project you need to start with setting
up your workspace using Gradle. To do that, run the ``setupDecompWorkspace`` Gradle task of your project, before
importing the project into your IDE:

.. code-block:: bash

    gradle setupDecompWorkspace

Now you can import your Gradle project, as described in :doc:`../project/gradle`. If your project is already imported,
make sure to refresh the Gradle configuration so your IDE can register the new Minecraft dependency.

Building your plugin
--------------------
ForgeGradle automatically configures your plugin to re-obfuscate to Searge mappings when building it so you can run it
in production. Make sure to use Gradle's ``build`` task and not ``jar`` directly.

.. _ForgeGradle: https://github.com/MinecraftForge/ForgeGradle
