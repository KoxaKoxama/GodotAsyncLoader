# GodotAsyncLoader


[![Loading scenes asynchronously in Godot](https://img.youtube.com/vi/GR95TXHz5kg/0.jpg)](https://www.youtube.com/watch?v=GR95TXHz5kg, "Loading scenes asynchronously in Godot")

## How to install and use plugin

1. Install the GodotAsyncLoader plugin in AssetLib

2. Enable the plugin (Project -> Project Settings -> Plugins -> Enable)

![groups](https://github.com/ImmersiveRPG/GodotAsyncLoader/blob/v2/docs/plugins.png)

3. Add scenes to groups

![groups](https://github.com/ImmersiveRPG/GodotAsyncLoader/blob/v2/docs/groups.png)

4. Setup plugin in main scene
```GDScript
const CATEGORIES := [
	"terrain",
	"building",
	"furniture",
	"plant",
	"item",
	"npc",
	"etc",
]

func _init() -> void:
	SceneAdder._sleep_msec = 100
	SceneAdder.set_categories(CATEGORIES)
```

5. Use the plugin to change to a new scene and load it asynchronously
```GDScript
func _on_start_pressed() -> void:
	SceneSwitcher.change_scene("res://src/World/World.tscn")
```

## How to load child scene async

```GDScript
# Instance scene asynchronously and add to current scene
var target = get_tree().get_current_scene()
var scene_file := "res://src/Animals/Puma.tscn"
var pos := Vector3(0, 1, 0)
SceneLoader.load_scene_async(target, scene_file, pos, true)
```

## How to load child scene async with callback

```GDScript
# Instance scene asynchronously and send to callback
var target = get_tree().get_current_scene()
var scene_file := "res://src/Animals/Puma.tscn"
var pos := Vector3(0, 1, 0)
SceneLoader.load_scene_async_with_cb(target, scene_file, pos, true, funcref(self, "on_animal_loaded"), {})

func on_animal_loaded(path : String, instance : Node, pos : Vector3, is_pos_global : bool, data : Dictionary) -> void:
	var target = get_tree().get_current_scene()
	instance.transform.origin = pos
	target.add_child(instance)
```

## How to load child scene sync

```GDScript
# Instance scene synchronously and add to target scene
var scene_file := "res://src/Animals/Puma.tscn"
var target = get_tree().get_current_scene()
var instance := SceneLoader.load_scene_sync(target, scene_file)
```
