# The Last Alchemist

A third-person action game made in **Unity (C#)** for gamepad. You play a fire mage who collects ingredients across the map, brews new powers at a cauldron, and defends your base against waves of enemies.

Made as the final exam project for *Game Development 3*.

![Unity](https://img.shields.io/badge/Unity-2021.3-000000?logo=unity&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?logo=csharp&logoColor=white)

## Gameplay

- **Explore** a forest map hidden under **fog of war**, using a minimap to find your way.
- **Fight enemies** to take the ingredients they guard. You start with only a basic fire shot.
- **Brew abilities** at the cauldron with the ingredients you've collected.
- **Pick an ability** from a radial wheel menu. Holding the button slows time to 5% while you choose.
- **Defend your base**: a day passes every 15 seconds, and every fifth day enemies attack the base.
- **Win** by defeating every enemy. **Lose** when your health runs out.

### Abilities

| Ability | Effect |
|---------|--------|
| Shooting | Basic fireball attack |
| Fire Comet | Aim at a spot and call a comet down on it from the sky |
| Freeze | Freezes all enemies within a radius for a few seconds |
| Shockwave | Knocks back nearby enemies |
| Enemy Takeover | Turns an enemy against its allies |
| Necromance | Raises three skeleton allies that fight on your side |
| Sudden Death | Instantly destroys every enemy within a radius |

### Enemies

- **Dwarf**: melee attacker
- **Healer**: heals nearby enemies, so take it out first
- **Necromancer**: keeps summoning skeleton minions while you're in range

## Code structure

- **`BaseAbility`** (abstract): every ability inherits from it and defines its own cooldown, UI (icon, colour, description in the wheel menu) and effect. Adding a new ability means adding a new subclass.
- **`BaseEnemy`**: shared health, movement, attack and status-effect logic (frozen, hit, taken over). `Dwarf`, `Healer` and `Necromancer` override `Attack()` and related methods.
- **Status effects** are handled by the enemy base class, so any ability can freeze or take over any enemy type.
- **`Manager`**: game state, health, day cycle with timed base attacks, pause menu and game over.
- **`Cauldron` / `Ingredient`**: inventory and crafting.

```
Assets/Scripts/
├── BaseAbility.cs, Abilities/     Ability system (one class per ability)
├── BaseEnemy.cs, Enemies/         Enemy types
├── Manager.cs                     Game state and day/attack cycle
├── Cauldron.cs, Ingredient.cs     Crafting
├── MenuScript.cs, WheelMenuItem.cs  Radial ability menu
└── Map.cs, MapIcon.cs             Minimap
```

Third-party art, UI and fog-of-war packages are kept separately in `Assets/ImportedPackages/`.

## Running it

1. Install **Unity 2021.3.10f1** via Unity Hub and open this folder as a project.
2. Connect a **gamepad** (the game is built for controller input).
3. Open `Assets/Scenes/MainMenu.unity` and press **Play**.
