# MagickaExpanded.enchantments
## Functions
#### MagickaExpanded.enchantments.*createBasicEnchantment*(*params*)
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

#### MagickaExpanded.enchantments.*createComplexEnchantment*(*params*)
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
