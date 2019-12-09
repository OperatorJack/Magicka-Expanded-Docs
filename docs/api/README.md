# API
### MagickaExpanded  
* MagickaExpanded.*info*(*message*)
   * Description
      * Logs the message to mwse.log and tes3.messageBox with log level `Info`.
   * Parameters
      * *message*: The string to show in the log.


* MagickaExpanded.*debug*(*message*)
   * Description
      * Logs the message to mwse.log and tes3.messageBox with log level `Debug`.
   * Parameters
      * *message*: The string to show in the log.


* MagickaExpanded.*error*(*message*)
   * Description
      * Logs the message to mwse.log and tes3.messageBox with log level `Error`.
   * Parameters
      * *message*: The string to show in the log.


* MagickaExpanded.*getActiveSpells*()
   * Description
      * Gets an array of all spells currently added through Magicka Expanded.
   * Returns
      * Array of `tes3Spell`.


* MagickaExpanded.**alchemy**
   * Description
      * An array of all alchemy related functions.


* MagickaExpanded.**enchantments**
   * Description
      * An array of all enchantment related functions.


* MagickaExpanded.**spells**
   * Description
      * An array of all spell related functions.


* MagickaExpanded.**effects**
   * Description
      * An array of all effect related functions.


* MagickaExpanded.**tomes**
   * Description
      * An array of all tome related functions.


* MagickaExpanded.**grimoires**
   * Description
      * An array of all grimoire related functions.


* MagickaExpanded.**functions**
   * Description
      * An array of all shared functions.

----
### MagickaExpanded.alchemy
* MagickaExpanded.alchemy.*createBasicPotion*(*params*)
   * Description
      * Creates or updates a potion based on the given *params*, 
        and adds it to the framework's list of managed potions. Accepts one
        magic effect.
   * Parameters
      * *params*: A table of parameters used to configure the potion. *params* 
        must be in the following format:
```lua
local params = {
   id = "examplePotionId",
   name = "My Potion",
   effect = tes3.effect.*,
   range = tes3.effectRange.* | nil,
   min = [int] | nil,
   max = [int] | nil,
   duration = [int] | nil,
   radius = [int] | nil,
   magickaCost = [int] | nil
}
```

* MagickaExpanded.alchemy.*createComplexPotion*(*params*)
   * Description
      * Creates or updates a potion based on the given *params*, 
        and adds it to the framework's list of managed potions. Accepts multiple
        magic effects.
   * Parameters
      * *params*: A table of parameters used to configure the potion. *params* 
        must be in the following format:
```lua
local params = {
    id = "examplePotionId",
    name = "My Potion",,
    magickaCost = [int] | nil
    effects = {
        [1] = {
            id = tes3.effect.*,
            range = tes3.effectRange.* | nil,
            min = [int] | nil,
            max = [int] | nil,
            duration = [int] | nil,
            radius = [int] | nil
        },
        [2] = {
            id = tes3.effect.*,
            range = tes3.effectRange.* | nil,
            min = [int] | nil,
            max = [int] | nil,
            duration = [int] | nil,
            radius = [int] | nil
        }
        ...
        [8] = {}
    }
}
```

----
### MagickaExpanded.enchantments
* MagickaExpanded.enchantments.*createBasicEnchantment*(*params*)
   * Description
      * Creates or updates an enchantment based on the given *params*, 
        and adds it to the framework's list of managed enchantments. Accepts one
        magic effect. Requires the enchantment ID is first created in the CS and an ESP is loaded with that ID.
   * Parameters
      * *params*: A table of parameters used to configure the potion. *params* 
        must be in the following format:
```lua
local params = {
   id = "exampleEnchantmentId",
   name = "My Enchantment",
   effect = tes3.effect.*,
   range = tes3.effectRange.* | nil,
   min = [int] | nil,
   max = [int] | nil,
   duration = [int] | nil,
   radius = [int] | nil,
   chargeCost = [int] | nil,
   maxCharge = [int] | nil,
   castType = tes3.enchantmentType.*,
}
```

* MagickaExpanded.enchantments.*createComplexEnchantment*(*params*)
   * Description
      * Creates or updates an enchantment based on the given *params*, 
        and adds it to the framework's list of managed enchantments. Accepts multiple
        magic effects. Requires the enchantment ID is first created in the CS and an ESP is loaded with that ID.
   * Parameters
      * *params*: A table of parameters used to configure the potion. *params* 
        must be in the following format:
```lua
local params = {
    id = "examplePotionId",
    name = "My Potion",
    chargeCost = [int] | nil,
    maxCharge = [int] | nil,
    castType = tes3.enchantmentType.*,
    effects = {
        [1] = {
            id = tes3.effect.*,
            range = tes3.effectRange.* | nil,
            min = [int] | nil,
            max = [int] | nil,
            duration = [int] | nil,
            radius = [int] | nil
        },
        [2] = {
            id = tes3.effect.*,
            range = tes3.effectRange.* | nil,
            min = [int] | nil,
            max = [int] | nil,
            duration = [int] | nil,
            radius = [int] | nil
        }
        ...
        [8] = {}
    }
}
```

----
### MagickaExpanded.spells  
* MagickaExpanded.spells.*getSpellCost*(*TES3spell spell*)
   * Description
      * Calculates and returns the spell costs for the given *TES3spell* parameter. Uses vanilla formula.
   * Parameters
      * *spell*: Thes TES3spell object to calculate spell costs for.

* MagickaExpanded.spells.*createBasicSpell*(*params*)
   * Description
      * Creates or updates a spell based on the given *params*, 
        and adds it to the framework's list of managed spell. Accepts one
        magic effect.
   * Parameters
      * *params*: A table of parameters used to configure the spell. *params* 
        must be in the following format:
```lua
local params = {
   id = "exampleSpellId",
   name = "My Spell",
   effect = tes3.effect.*,
   range = tes3.effectRange.* | nil,
   min = [int] | nil,
   max = [int] | nil,
   duration = [int] | nil,
   radius = [int] | nil,
   magickaCost = [int] | nil
}
```

* MagickaExpanded.spells.*createComplexSpell*(*params*)
   * Description
      * Creates or updates a spell based on the given *params*, 
        and adds it to the framework's list of managed spell . Accepts multiple
        magic effects.
   * Parameters
      * *params*: A table of parameters used to configure the spell . *params* 
        must be in the following format:
```lua
local params = {
    id = "exampleSpellId",
    name = "My Spell",,
    magickaCost = [int] | nil
    effects = {
        [1] = {
            id = tes3.effect.*,
            range = tes3.effectRange.* | nil,
            min = [int] | nil,
            max = [int] | nil,
            duration = [int] | nil,
            radius = [int] | nil
        },
        [2] = {
            id = tes3.effect.*,
            range = tes3.effectRange.* | nil,
            min = [int] | nil,
            max = [int] | nil,
            duration = [int] | nil,
            radius = [int] | nil
        }
        ...
        [8] = {}
    }
}
```

----
### MagickaExpanded.effects
* MagickaExpanded.effects.**illusion**
   * Description
      * An array of all effect related functions for the illusion school of magic.

* MagickaExpanded.effects.**conjuration**
   * Description
      * An array of all effect related functions for the conjuration school of magic.

* MagickaExpanded.effects.**alteration**
   * Description
      * An array of all effect related functions for the alteration school of magic.

* MagickaExpanded.effects.**destruction**
   * Description
      * An array of all effect related functions for the destruction school of magic.

* MagickaExpanded.effects.**mysticism**
   * Description
      * An array of all effect related functions for the mysticism school of magic.

* MagickaExpanded.effects.**restoration**
   * Description
      * An array of all effect related functions for the restoration school of magic.


----
### MagickaExpanded.effects.illusion
* MagickaExpanded.effects.illusion.createBasicEffect()

----
### MagickaExpanded.effects.conjuration
* MagickaExpanded.effects.conjuration.createBasicEffect()
* MagickaExpanded.effects.conjuration.createBasicBoundArmorEffect()
* MagickaExpanded.effects.conjuration.createBasicBoundWeaponEffect()
* MagickaExpanded.effects.conjuration.createBasicSummoningEffect()

----
### MagickaExpanded.effects.alteration
* MagickaExpanded.effects.illusion.createBasicEffect()
* MagickaExpanded.effects.illusion.createBasicWeatherEffect()

----
### MagickaExpanded.effects.destruction
* MagickaExpanded.effects.destruction.createBasicEffect()

----
### MagickaExpanded.effects.mysticism
* MagickaExpanded.effects.mysticism.createBasicEffect()
* MagickaExpanded.effects.mysticism.createBasicTeleportationEffect()

----
### MagickaExpanded.effects.restoration
* MagickaExpanded.effects.restoration.createBasicEffect()

----
### MagickaExpanded.tomes
* MagickaExpanded.tomes.addTomesToPlayer()
* MagickaExpanded.tomes.registerTome()
* MagickaExpanded.tomes.registerTomes()
* MagickaExpanded.tomes.registerEvent()

----
### MagickaExpanded.grimoires
* MagickaExpanded.tomes.addGrimoiresToPlayer()
* MagickaExpanded.grimoires.registerGrimoire()
* MagickaExpanded.grimoires.registerGrimoires()
* MagickaExpanded.grimoires.registerEvent()

----
### MagickaExpanded.functions
* MagickaExpanded.functions.getActorsNearTargetPosition()
* MagickaExpanded.functions.getEffectFromEffectOnEffectEvent()
* MagickaExpanded.functions.getCalculatedMagnitudeFromEffect()
* MagickaExpanded.functions.linearInterpolation()
* MagickaExpanded.functions.ternary()
* MagickaExpanded.functions.addSpellsToPlayer()