# Chlora Godot Project Template

Recommended organization:

game/
  assets/      Raw/imported game assets
  scenes/      Godot scenes (.tscn)
  scripts/     GDScript files
  resources/   Reusable .tres/.res resources
  tests/       Prototype and test scenes

Suggested autoloads:
- GameManager
- SaveManager
- AudioManager
- SceneManager
- InputManager

Art source files remain in /art at the repository root.
Only game-ready assets should be copied into /game/assets.
