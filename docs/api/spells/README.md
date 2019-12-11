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
