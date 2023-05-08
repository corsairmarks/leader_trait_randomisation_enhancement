**_DEPRECATED:_** Due to the changes in Stellaris version 3.8 "Gemini" to how leaders gain traits (and trait "levels") as they level up, this mod is no longer applicable. It has been discontinued.

# Overview

Frustrated that some leader traits can't be gained on level-up?  Or maybe you'd like your robotic/synthetic leaders to use the machine-specific traits too?  Then this mod is for you!

The code in this mod polishes some of the code from the base game to work better and offer options that may have been forgotten when new traits were added or systems were redesigned.

# Changes

* Removes invalid/inappropriate/already-extant traits from the pool when rolling
* Refers to the leader itself or its species instead of assuming based on empire (this could sometimes result in incorrect traits being applied)
* Handles machine trait alternatives better in code
* Machine/robot leaders get machine traits where there are equivalents to the "normal" traits
* Machine/robot admirals can now gain a Restore Point (this built-in trait was not coded to be randomly added but had a small chance to appear when leaders were initially generated)
* Machine/robot leaders have lifespan-altering traits removed (they are immortal)
* Scientists can now get a Sapient AI Assistant on level-up if the correct technology is unlocked
* Code for adding random traits generally respects the "opposites" blocks of each trait, except that scientists are not limited to only one scientific expertise (scientists could already have multiple expertises in the base game, despite the opposites block on all of the traits)
* Governors can roll Agrarian Upbringing, Bureaucrat (or equivalent), or army/navy related traits upon level up - this make a bit less narrative sense for Agrarian Upbringing and the former military traits, but I felt it was unfair to lock their benefits to only newly generated leaders
* Rulers can now roll "Space Miner," "From the Ranks," and "Reformer" - the army related trait makes less narrative sense to add randomly, but politicians can definitely become reformers during their tenure
* English localisation to change the descriptions for traits that sounded odd when randomly added after a leader was spawned, including their descriptions:
    * Agrarian Upbringing is now Agrarian Affinity
    * Army Veteran is now Military Liaison
    * Retired Fleet Officer is now Naval Liaison
    * From the Ranks wasn't renamed - I felt the name fit the effect very well - maybe it can be justified as leader's military experience becoming more widely known?
* Leaders now gain the regular and "ruler" version of generic traits (+/-experience, +/-lifespan, Arrested Development) (and if they gain one while being a ruler, it transfers back to their regular class)
* Leaders that have "ruler" generic traits (invisible until a leader becomes a ruler) have it/them removed and rerolled to another non-generic trait - together with the above point, this will help leaders always benefit from their generic traits when they are rulers (e.g. not losing Resilient and then dying)
* Leaders with opposing traits, e.g. Adaptable and Stubborn, will have the negative trait removed (this mod should no longer roll them at all, so this fix is for any existing leaders you have)

Optional feature (defaults to disabled): Leaders will have a higher chance to gain traits related to their current role.  This feature is experimental and only applies to scientists at present.  Enable or disable by running this command on the console: `event better_leader_trait_randomization.3`.  Check the status with `trigger is_leader_trait_role_weight_enabled = yes` (showing a green checkmark indicates the feature is enabled, a red x is disabled).

## Compatibility

Built for Stellaris version 3.7 "Canis Minor."  Not compatible with achievements.

Most of this mod is custom code, but it does replace two small parts of the base game's code.  First, it preempts the event `leader.20` that is responsible for triggering leader level-up trait randomisation.  Notably this was one of the two places that restricted researching scientists from being able to gain traits.  Second, it replaces the effect `add_random_leader_trait` that does the actual randomisation.

What all this means to you is that this mod will be widely compatible with other mods, as long as they do not also affect these two narrow areas.

### When to Install

This mod can be safely added to or removed from your savegame after the game has started. It is implemented through events, effects, and triggers without adding or removing gameplay objects. If you remove it, you will keep any leaders and their existing traits, but further leaders and leader level-ups will use the default code. Back up your savegame before trying to remove a mod.

### Recommended Companion Mods

Like leaders?  Try a couple of my other leader-related mods that work with this one.

* [Leader Traits: All Eligible Species Traits](https://steamcommunity.com/sharedfiles/filedetails/?id=2499031295) will ensure your leaders get all their species-based traits when being assimilated (such as Psionic or Erudite)
* [Leader Traits: Scientist AI Assistant Upgrader](https://steamcommunity.com/sharedfiles/filedetails/?id=2498166286) will help your scientists upgrade to "Sapient AI Assistants" from "Custom AI Assistants" when you discover the right technology
* [Retain Leaders from Integrated Subjects & Pre-FTL Civilizations](https://steamcommunity.com/sharedfiles/filedetails/?id=2553818684) will let you choose whether you would like to keep leaders from integrated subjects or conquered/infiltrated primitives

## Known Issues

This mod overwrites one effect and preempts one event from the base game.  Expect to see two lines in error.log like this:

```
[15:38:58][game_singleobjectdatabase.h:165]: Object with key: add_random_leader_trait already exists, using the one at  file: common/scripted_effects/better_leader_trait_randomisation_scripted_effect_overrides.txt line: 2
[15:38:59][eventmanager.cpp:368]: an event with id [leader.20] already exists!  file: events/leader_events_1.txt line: 950
```

What this means to you is that this mod will need a compatibility patch to work with other mods that alter the same base Stellaris content.

## Changelog

* 1.0.0 Initial version
* 1.0.1 Ensure leader traits are checked when returning to pre-ruler class
* 1.1.0 Minor new features
    * A leader can gain a level-up trait once per leader class (assuming they somehow can switch classes - most commonly by becoming a Ruler), as opposed to once ever
    * Maimed is now preserved as a Scientist -> Ruler trait (Paranoid and Traumatized were considered, but their effects are tailored for Scientists)
    * Maimed is removed should a leader become robotic
* 2.0.0 Update for compatibility with Stellaris 3.1 "Lem" - add handling for Clone Army admiral traits
* 2.1.0 Mark a compatible with Stellaris 3.2 "Herbert" - no script changes
* 2.2.0 Add optional leader weighting based on their leadership role at time of level-up
* 2.2.1 Fix bug with Clone Soldier handling - was improperly adding the trait when it should have been removed instead
* 3.0.0 Update for Stellaris version 3.3.0 "Libra" - integrate underlying changes from the base game
* 4.0.0 Update for Stellaris version 3.4 "Cepheus" - use memory optimization feature for effects and triggers
* 5.0.0 Update for Stellaris version 3.6 "Orion" (and changes from version 3.5 "Fornax")
    * Add randomisation support for the new Mindful scientist trait
    * Unity generation traits are now based on species (normal/machine/hive) rather than authority - that was previously required because of empire-specific job boosts before the Unity rework
* 5.0.1 Remove event trigger from `on_debris_scavenged_and_researched` - it doesn't have a reference to the science vessel that interacted with the debris
* 5.1.0 Add a compatibility trigger for other mods to check whether this one is active
* 5.2.0 Match criteria for randomizing Trait: Iron Fist with the requirements on the trait itself (no gestalts; must allow slavery or have a percent-enslaved modifier or have at least one enslaved species)
* 6.0.0 Update for Stellaris version 3.7 "Canis Minor"
    * Support new scientist Archaeostudies expertise
    * Support new Trickster variant introduced with First Contact

## Source Code

Hosted on [GitHub](https://github.com/corsairmarks/leader_trait_randomisation_enhancement)

### Development Notes

It is best to clone this repository into `<Stellaris User's Directory>/Paradox Interactive/Stellaris/mod`, and then make a connection to the `mod` folder via a `*.mod` file's `path` property.  That will ensure the game can see the files, and also that CWTools will parse them.  Also note that the README.md file exists in the `mod` directory but is symbolically linked in the root directory.