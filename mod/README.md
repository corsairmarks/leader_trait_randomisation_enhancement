# Overview

Frustrated that some leader traits can't be gains on level-up?  Or maybe you'd like your robotic/synthetic leaders to use the machine-specific traits too?  Then this mod is for you!

The code in this mod polishes some of the code from the base game to work better and offer options that may have been forgotten when new traits were added or systems were redesigned.

# Changes

* Removes restriction on scientists in research roles not gaining traits
* Removes invalid/inappropriate/already-extant traits from the pool when rolling
* Refers to the leader itself or its species instead of assuming based on empire (this could sometimes result in incorrect traits being applied)
* Handles machine trait alternatives better in code
* Machine/robot leaders get machine traits where there are equivalents to the "normal" traits
* Machine/robot admirals can now gain a Restore Point (this built-in trait was not coded to be randomly added but had a small chance to appear when leaders were initially generated)
* Scientists can now get a Sapient AI Assistant on level-up if the correct technology is unlocked
* Code for adding random traits generally respects the "opposites" blocks of each trait, except that scientists are not limited to only one scientific expertise (scientists could already have multiple expertises in the base game, despite the opposites block on all of the traits)
* Governors can roll Agrarian Upbringing, Bureaucrat (or equivalent), or army/navy related traits upon level up - this make a bit less narrative sense for Agrarian Upbringing and the former military traits, but I felt it was unfair to lock their benefits to only newly generated leaders
* Rulers can now roll "From the Ranks" and "Reformer" - the army related trait makes less narrative sense to add randomly, but politicians can definitely become reformers during their tenure

## Compatibility

Most of this mod is custom code, but it does replace two small parts of the base game's code.  First, it preempts the event `leader.20` that is responsible for triggering leader level-up trait randomisation.  Notably this was one of the two places that restricted researching scientists from being able to gain traits.  Second, it replaces the effect `add_random_leader_trait` that does the actual randomisation.  The majority of code improvements are here including removing the second restriction on researching scientists gaining traits.

What all this means to you is that this mod will be widely compatible with other mods, as long as they do not also affect these two narrow areas.

### Recommended Companion Mods

Like leaders?  Try a couple of my other leader-related mods that work with this one.

* [Enable All Eligible Species Traits for Leaders](https://steamcommunity.com/sharedfiles/filedetails/?id=2499031295) will ensure your leaders get all their species-based traits when being assimilated (such as Psionic or Erudite)
* [Scientist AI Assistant Upgrader](https://steamcommunity.com/sharedfiles/filedetails/?id=2498166286) will help your scientists upgrade to "Sapient AI Assistants" from "Custom AI Assistants" when you discover the right technology
* [Retain Leaders from Integrated Subjects]() will let you choose whether you would like to keep leaders from integrated subjects or conquered/infiltrated primitives.

### When to Install

This mod can be safely added to or removed from your savegame after the game has started. It is implemented through events, effects, and triggers without adding or removing gameplay objects. If you remove it, you will keep any leaders and their existing traits, but further leaders and leader level-ups will use the default code. Back up your savegame before trying to remove a mod.

## Known Issues

This mod overwrites one effect and preempts one event from the base game.  Expect to see two lines in error.log like this:

```
[20:47:35][game_singleobjectdatabase.h:147]: Object with key: add_random_leader_trait already exists
[20:47:35][eventmanager.cpp:355]: an event with id [leader.20] already exists!  file: events/leader_events_1.txt line: 950
```

What this means to you is that this mod will need a compatibility patch to work with other mods that alter the same base Stellaris content.

## Changelog

* 1.0.0 Initial version

## Source Code

Hosted on [GitHub](https://github.com/corsairmarks/leader_trait_randomisation_enhancement)

### Development Notes

It is best to clone this repository into `<Stellaris User's Directory>/Paradox Interactive/Stellaris/mod`, and then make a connection to the `mod` folder via a `*.mod` file's `path` property.  That will ensure the game can see the files, and also that CWTools will parse them.  Also note that the README.md file exists in the `mod` directory but is symbolically linked in the root directory.