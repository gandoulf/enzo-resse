# Blockers

- [Create Blocker](#create-blocker)
  - [Use Case](#use-case)
  - [Custom Tooltip](#custom-tooltip)

`Blocker` and `Blocker Data` can be created in both `C++` and `Blueprint`. This tutorial will describe only the Blueprint implementation.
Once you understand Blueprint, implementing it in C++ should be straightforward.

## Create Blocker

First, you will need to create two Blueprints inheriting from:
- `P2B_Blocker` Call it `BP_TutorialBlocker`. This will be the object spawned by the generator when associated with a color.
- `P2B_BlockerData` Call it `BP_TutorialBlockerData`. This will hold any custom data you preset in the `DataAsset`, which will then be sent to the associated `Blocker`.

![BlockersPicture](../../assets/Tutorials/Blockers/0_CreateBlockerClass.png)

If you open `BP_TutorialBlocker`, you will have access to several overrideable functions that are called during `Blocker` generation.
The blocker is spawned in a deferred state to allow modifications before the construction script:
- `PreDynamicMeshGeneration` Called before `Finish Spawn` and before the `DynamicMesh` is generated.
- `PostDynamicMeshGeneration` Called before `Finish Spawn` and after the `DynamicMesh` is generated.
- `OnBlockerSpawnFinished` Called after `Finish Spawn`, when the construction script has been executed.

These functions provide access to the `Blocker Data` class that generated the `Blocker`. You can cast it to any type, and if the cast is valid, use the data it holds.
These functions are the core of customization, where you will add all your logic.

![BlockersPicture](../../assets/Tutorials/Blockers/1_BlockerOnGenerationFunction.png)

Next, open the `Template Data Asset` used by your `Blocker Generator`. This tutorial uses `PDA_Default_Generation`. Modify the following:
- Set `Default Blocker` to the new data class `BP_TutorialBlockerData`.
- Update `Blocker Soft Class` in the settings to `BP_TutorialBlocker`.

If you hit generate, all blockers will now be of the type you've just created.

![BlockersPicture](../../assets/Tutorials/Blockers/2_ReplaceBlockerClasses_DataAsset.png)

If you want only a specific color to generate this new blocker, simply create a new `Blocker DataAsset`, let's call it `PDA_Tutorial_Blocker` and add it to the list.

![BlockersPicture](../../assets/Tutorials/Blockers/3_AddBlockerDataAssets.png)

Open it and add two rows to the `Color to Blocker` section. This allows you to spawn two types of `Tutorial_Blocker` with different settings.

![BlockersPicture](../../assets/Tutorials/Blockers/4_AddGenerationColor.png)

Finally, if you open `Paint 2 Blocking Mode`, you will see that the new blocker colors are available for drawing.

![BlockersPicture](../../assets/Tutorials/Blockers/5_OpenPaintMode.png)

## Use Case

Now that the custom `Blocker` is set up, let's see how to use it properly. The goal of the plugin is to generate blockers and iterate on game design quickly.
For this reason, a `Blocker` isn't just a 3D mesh with a collider, it can also have logic and play a role in gameplay. 
For example, blockers can define cover areas, loot spawn zones, destructible barricades, etc.

Let's simulate a life system as an example. First, create a new component call it `BP_LifeHandler_Component`.

![BlockersPicture](../../assets/Tutorials/Blockers/6_CreateLifeComponent.png)

Open it and add a new variable: `CurrentLife`. I recommend assigning it a proper `Category`, such as `Settings|Life`.

![BlockersPicture](../../assets/Tutorials/Blockers/7_CreateCurrentLifeVariable.png)

Next, open `BP_TutorialBlockerData` and do the same, add a new variable called `BlockerLife`, and set its `Category` to `Settings|Life`. 
If you check the `Class Default` values, they should look like this:

![BlockersPicture](../../assets/Tutorials/Blockers/8_CreateDataBlockerLife.png)

Now, open `BP_TutorialBlocker`, add the `BP_LifeHandler_Component`, and override `PostDynamicMeshGeneration` or `OnBlockerSpawnFinished`. 
Don't forget to call the parent function.

Now, follow these steps:
- Cast `BlockerData` to `BP_TutorialBlockerData`.
- If the cast is valid:
- Get the `BlockerLife` value from the data.
- Set `CurrentLife` in `BP_LifeHandler_Component`.

![BlockersPicture](../../assets/Tutorials/Blockers/9_SetBlockerLife.png)

Finally, open `PDA_Default_Generation` or `PDA_Tutorial_Blocker` and set the blocker life values as needed.

![BlockersPicture](../../assets/Tutorials/Blockers/10_SetLifePerBlocker.png)

Now, when you paint different blockers, they will have different life values. This example is simplified and lacks logic for gameplay,
but it's easy to imagine a real system with targets and health mechanics.

## Custom Tooltip

`Blocker Data` is directly linked to `Paint 2 Blocker Mode`, meaning you can pass information between them. 
When this mode is open, hovering over a `Color Preset` will display a tooltip. You can add custom information to this tooltip
by overriding `GenerateParametersTooltip` in the `BlockerData` class.

For example, to display the `BlockerLife` parameter in the tooltip:
- Override `GenerateParametersTooltip` and call the parent function.
- Create a local array variable and name it `Tooltip`.
- Add an element to the array with `ParameterName` and the value of `CurrentLife`.
- Return the `Tooltip` variable.

![BlockersPicture](../../assets/Tutorials/Blockers/11_AddParameterToTT.png)

Open `Paint 2 Blocker Mode` and hover over a color. The tooltip should now display the `BlockerLife`.

![BlockersPicture](../../assets/Tutorials/Blockers/12_OveerColorForTT.png)

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_