====================
MCP (Mod Coder Pack)
====================

The `Mod Coder Pack`_ (short MCP) was originally created as a collection of scripts, tools and mappings to make the
development of mods for Minecraft easier. Since Minecraft is not open-source and for the most part obfuscated,
development against it was painful since the original code was almost unreadable. MCP was designed as a workspace in
which developers can create mods using decompiled, deobfuscated (human-readable) Minecraft code.

Workflow
========
Using MCP adds additional steps to the development workflow of plugins, simplified below:

- Set up the MCP workspace
    - Download the Minecraft client/server files
    - Deobfuscate the code (changing obfuscated names into human-readable ones)
    - Decompile the code (generating source files from the binary classes)
- Create a plugin using the deobfuscated Minecraft source
- Re-obfuscate the plugin code so it can be used with the obfuscated code at runtime

Mappings
========
MCP is using two different sets of mappings which are applied separately during the workspace setup. The difference
between "Notch", "Searge" and "MCP" mappings can be seen in the example below:

.. code-block:: java

    // Notch
    void a(a ☃);

    // Searge
    void func_4454848_a(Entity p_445848_1);

    // MCP
    void spawn(Entity entity);

- **Notch mappings** are the original names in the obfuscated Minecraft binary. They change regularily with Minecraft
  mappings.
- **Searge mappings** contain unique names for all obfuscated methods, fields and parameters, as well as human-readable
  names for the classes. Unlike Notch mappings they stay usually the same across Minecraft updates unless the method
  signatures change. For SpongeVanilla and SpongeForge, they are also used in production.
- **MCP mappings** contain human-readable names largely contributed by the community. They are typically only used in
  the development environment, and then reobfuscated to Searge or Notch mappings. If you encounter an unnamed method,
  you can name it using the `MCP bot`_, which is available in the MCP and Sponge IRC channel. Name changes can be
  requested on `GitHub <https://github.com/ModCoderPack/MCPBot-Issues/issues>`_.

When you create a plugin you work with *MCP mappings* in your development environment. To run the plugin in production
(outside of your IDE) you need to reobfuscate it to *Searge mappings*.

.. _`Mod Coder Pack`: http://www.modcoderpack.com
.. _`MCP bot`: http://mcpbot.bspk.rs/
