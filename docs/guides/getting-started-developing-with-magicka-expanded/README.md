# Getting Started: Developing With Magicka Expanded
This article will explain some of the basics of building a mod based on the Magicka Expanded framework. It will cover referencing the framework in your mod, checking if the framework is installed, claiming a spell effect ID, adding a basic effect, and adding a basic spell. This article assumes that you have some knowledge of programming with Lua and the Morrowind Script Extender. If you're new to either of those things, please refer to the Morrowind Script Extender guides before continuing. This mod will use the implementation of the spell effect "Banish Daedra" from the Magicka Expanded Lore Friendly Spell pack as an example.

## Creating a Mod  
This article will assume that you have set up a new _main.lua_ file, as described in the Morrowind Script Extender guides. This article will cover everything that you need to add to your script file, so please leave the script file empty until told otherwise. 

## Referencing the Magicka Expanded Framework  
The Magicka Expanded base framework, also known as package 00 in the mod files, is a MWSE library. This means that it is loaded into MWSE before any dependent mods, and it kept in memory while the application is active. 

To reference the framework, you need to use the MWSE function _include_, and store the result in a local variable. Consider the code below:
```lua
local framework = include("OperatorJack.MagickaExpanded.magickaExpanded")
```

You can add this as the first line in your _main.lua_ file. This will pull the framework from MWSE and let you access it through the local variable, _framework_.

## Checking if the Framework is Installed  
Creating a reference to the framework as described above does not guarantee that it is actually installed. If it is not installed, the local variable _framework _will be _nil_, or nothing. You need to check for that before trying to add your spell effects, or you will get a lot of errors!

To check if the framework is installed, consider the code below:  
```lua
-- Check Magicka Expanded framework.
if (framework == nil) then
 local function warning()
  tes3.messageBox(
"[EXAMPLE-MOD ERROR] Magicka Expanded framework is not installed!"
.. " You will need to install it to use this mod."
  )
 end
 event.register("initialized", warning)
 event.register("loaded", warning)
 return
end
```

You can add this to your _main.lua_ file, below the previous step's code. In the code, _EXAMPLE-MOD_ is the name of your mod. Replace it with the name of your mod. This code will check if _framework _is _nil_, and if so, register a warning to the user. Most importantly, it will return and prevent the script from continuing, prevent errors further in your code.

## Claiming a Spell Effect ID  
Before you can create a new magic effect, you first have to claim a numerical ID for it and register the effect name. You can do this through the MWSE function, _tes3.claimSpellEffectId_. Consider the code below:

```lua
tes3.claimSpellEffectId("banishDaedra", 220)
```

You can add this to your _main.lua_ file, below the previous step's code. This line will register my effect name, "banishDaedra" with ID 220 in the MWSE table of magic effects. The effect ID must be unique. To view existing effect IDs and claim your own, please refer to the article "Claiming a Spell Effect ID."

## Adding a Basic Magic Effect  
Magicka Expanded exposes a variety of tools to create magic effects. For a full list of tools exposed, please refer to the article "Magicka Expanded API." Consider the code below:

```lua
-- onBanishDaedraTick represents the actual logic of the effect. Skip this for a moment and come back after reading the function below this one.
local function onBanishDaedraTick(e)
 -- Trigger into the spell system.
 if (not e:trigger()) then
  return
 end

 -- Ignore any non-daedric opponents.
 if (e.effectInstance.target.object.type ~= tes3.creatureType.daedra) then
         -- Setting the effectInstance.state to retired will prevent the effect from processing again.
  e.effectInstance.state = tes3.spellState.retired
  return
 end

     -- Here we use a ME framework function to retrieve the effect object from the onTick event parameter.
 local effect = framework.functions.getEffectFromEffectOnEffectEvent(e, tes3.effect.banishDaedra)
     -- We can then use that effect object to calculate a random magnitude based on the effect configuration.
 local magnitude = framework.functions.getCalculatedMagnitudeFromEffect(effect)

     -- e.effectInstance.target represents the target of the spell cast. Here, we check if their level is less than the magnitude we calculated previously.
 if (e.effectInstance.target.object.level <= magnitude) then
         -- If it is, delete the target! They've been "banished"!

  --@type tes3reference
  e.effectInstance.target:disable()

  timer.delayOneFrame({
callback = function()
 e.effectInstance.target.deleted = true
end
  })

  tes3.messageBox("%s has been banished!", e.effectInstance.target.baseObject.name)
 else
         -- If it is not, we don't delete the target.
  tes3.messageBox("%s was too powerful to be banished!", e.effectInstance.target.baseObject.name)
 end

     -- Since Banish Daedra should only occur 1 time, we set the effect state to retired. However, some effects may not require this.
 e.effectInstance.state = tes3.spellState.retired
end

-- addBanishDaedraEffect is the function that actually adds the new magic effect to the system. 
local function addBanishDaedraEffect()
     -- It does this through the ME framework functions. Here, we are using the conjuration.createBasicEffect function to register the effect. This means that many of the other settings available to use are automatically configured to the standard defaults of a conjuration spell. This will also provide default VFX and icons for you, unless as choose to override them as below.
 framework.effects.conjuration.createBasicEffect({
  -- Base information.
  id = tes3.effect.banishDaedra,
  name = "Banish Daedra",
  description = "Banishes a daedric creature back to its originating plane. The effect's magnitude is the level of daedra that it can banish.",

  -- Basic dials.
  baseCost = 25.0,

  -- Various flags.
  allowEnchanting = true,
  allowSpellmaking = true,
  appliesOnce = true,
  canCastTarget = true,
  canCastTouch = true,
  hasNoDuration = true,
  nonRecastable = true,
  unreflectable = true,

  -- Graphics/sounds.
  icon = "RFD\\RFD_lf_banish.dds",
  particleTexture = "vfx_myst_flare01.tga",
  lighting = { 0.99, 0.95, 0.67 },

         -- The onTick callback registered here is the function above this one. Each time the spell effect ticks, it will be called. onCollision is also a callback. For more examples, refer the the ME spell packs.
  -- Required callbacks.
  onTick = onBanishDaedraTick,
 })
end

-- Now, we must actually register the functions above to be executed. We do this by tying them to the magicEffectsResolved event, which is a system event provided by MWSE.
event.register("magicEffectsResolved", addBanishDaedraEffect)
```

You can add this to the bottom of your _main.lua_ file, below the previous step's code. Please read the comments and thoroughly consider the code you see before continuing.

## Adding a Basic Magic Spell  
Now that our effect is registered, we can create a spell with it. This is very easy. Consider the code below:

```lua
-- This declares a function to register any spells in our mod. Here, we are just registering one.
local function registerSpells()
  -- This function uses ME framework functions to create the spell. spells.createBasicSpell will create a spell with one magic effect. If the spell ID you pass already exists in the game or in a mod, the first effect will be overwritten.
  framework.spells.createBasicSpell({
 id = "OJ_ME_BanishDaedraSpell",
 name = "Banish Daedra",
 effect = tes3.effect.banishDaedra,
 range = tes3.effectRange.touch,
 min = 30,
 max = 50
  })
end

-- Finally, we register the spell to the event MagickaExpanded:Register. This is a ME framework event that is called after all other magic effect events are registered and completed. This insures that you don't try to create a spell before the effect is available!
event.register("MagickaExpanded:Register", registerSpells)
```

You can add this to the bottom of your _main.lua_ file, below the previous step's code. Please read the comments and thoroughly consider the code you see before continuing.

## Conclusion
That's it! Your spell is now "in-game". You can load the game and use the console command _addSpell_ to add it to your spell list and try it out. 

At this point, please explore the [API](../../api).

If you have comments or concerns, please contact me on Discord for the fastest response. I am always happy to help people create new effects.