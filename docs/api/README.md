# API - MagickaExpanded  
## Classes
#### [MagickaExpanded.alchemy](/docs/api/alchemy)
   * Description
      * An array of all alchemy related functions.


#### [MagickaExpanded.enchantments](/docs/api/enchantments)
   * Description
      * An array of all enchantment related functions.


#### [MagickaExpanded.spells](/docs/api/spells)
   * Description
      * An array of all spell related functions.


#### [MagickaExpanded.effects](/docs/api/effects)
   * Description
      * An array of all effect related functions.


#### [MagickaExpanded.tomes](/docs/api/tomes)
   * Description
      * An array of all tome related functions.


#### [MagickaExpanded.grimoires](/docs/api/grimoires)
   * Description
      * An array of all grimoire related functions.


#### [MagickaExpanded.functions](/docs/api/functions)
   * Description
      * An array of all shared functions.
      
## Functions
#### MagickaExpanded.*info*(*message*)
   * Description
      * Logs the message to mwse.log and tes3.messageBox with log level `Info`.
   * Parameters
      * *message*: The string to show in the log.


#### MagickaExpanded.*debug*(*message*)
   * Description
      * Logs the message to mwse.log and tes3.messageBox with log level `Debug`.
   * Parameters
      * *message*: The string to show in the log.


#### MagickaExpanded.*error*(*message*)
   * Description
      * Logs the message to mwse.log and tes3.messageBox with log level `Error`.
   * Parameters
      * *message*: The string to show in the log.


#### MagickaExpanded.*getActiveSpells*()
   * Description
      * Gets an array of all spells currently added through Magicka Expanded.
   * Returns
      * Array of `tes3Spell`.
