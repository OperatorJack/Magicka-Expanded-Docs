# MagickaExpanded.alchemy
#### MagickaExpanded.alchemy.*createBasicPotion*(*params*)
 * Description
    * Creates or updates a potion based on the given *params*, and adds it to the framework's list of managed potions. Accepts one magic effect.
 * Parameters
    * *params*: A table of parameters used to configure the potion. *params* must be in the following format:
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

#### MagickaExpanded.alchemy.*createComplexPotion*(*params*)
 * Description
    * Creates or updates a potion based on the given *params*, and adds it to the framework's list of managed potions. Accepts multiple magic effects.
 * Parameters
    * *params*: A table of parameters used to configure the potion. *params* must be in the following format:
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
