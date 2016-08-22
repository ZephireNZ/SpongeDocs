======================
Publishing Your Plugin
======================

Sponge's official plugin / mod repository, `Ore <http://ore-staging.spongepowered.org>`_, is a free and open-source
project that anyone may publish their Sponge plugins or Forge mods on.

Packaging Your Plugin
~~~~~~~~~~~~~~~~~~~~~

Ore requires any projects to be packaged with a ``mcmod.info`` descriptor file in the top-level of your JAR file. This
file is used to automatically infer some important details about your project to make the upload process easier.
Luckily, Sponge API has a built in annotation processor that creates this file for you automatically, on compile, using
the ``@Plugin`` annotation that you have likely already created in your plugin's main class.

For reference, here is a sample ``mcmod.info`` file:

.. code-block:: json

    [
        {
            "modid": "my-plugin",
            "name": "MyPlugin",
            "version": "1.0.0",
            "description": "My first plugin!",
            "url": "https://spongepowered.org",
            "authorList": [
                "windy",
                "Zidane",
                "gabizou"
            ],
            "requiredMods": [
                "bookotd@1.0.0",
                "ore-test@1.0.0",
                "worldedit@1.0.0"
            ],
            "dependencies": [
                "bookotd@1.0.0",
                "ore-test@1.0.0",
                "worldedit@1.0.0"
            ]
        }
    ]

At the very least, each Ore project *must* have the ``modid``, ``name`` and, ``version`` fields completed.

Uploading Your Plugin
~~~~~~~~~~~~~~~~~~~~~

Once your plugin's JAR file is packaged with an ``mcmod.info`` descriptor file in the top-level, your plugin is ready
for uploading! To create a project on Ore, you must have an account with us on the forums. Hitting the "Sign up"
button in the top-right corner will take you to the appropriate page to create one. If you already have an account,
just hit the "Log in" button in the top-right corner to log into Ore.

Once logged in, navigate to your avatar and select the "New" option in the drop-down menu that appears, or just press
the "C" key. Once at that page, publishing your project is as easy as following the onscreen instructions.