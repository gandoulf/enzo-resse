# LFOW V1.2.0

Adding the new features `Stealth Area` and `Heat Texture` to the plugin. Adding MOBA template, documentation, and many fixes.

**Features**

- `Stealth Area`: Allows bush mechanics to be added to the games.
- `Heat Texture`: Smooths the state transition of the fog.
- `Texture Sample SceneCapture`: Previously, only the camera texture sample was available.

**Fixes**

- `SetDrawingEntityTeam`: If the actor was an entity, the team wasn't set.
- `TextureSample`: Some texture samples were calling ShrinkSample, generating an incorrect AABB.
- `Listen Server`: During play in the editor, NetMode was being set too late for correct initialization of the FOW, so an alternative method is now used.
- `Loading`: A save could generate some blinking.
- `Tile Merging`: Has been revised to correctly fit with the heat texture.

**Documentation**

- `Network` architecture documentation has been added.
- `MOBA` template documentation has been added.
- `Heat Texture` tutorial documentation has been added.
- `Material` tutorial documentation has been added.
- `Stealth Area` tutorial documentation has been added.
- `Teams` tutorial documentation has been added.
- `Toggle Render` tutorial documentation has been added.

**LayeredFOW_Demo**

- A template for a `MOBA` game is now provided in this project. You can migrate the `MOBATemplate` folder to your `UE5.4 project` to set up an online game.

That's all for this update. Don't hesitate to ping me on my `Discord` if you find issues or if you'd like to submit a feature idea!

**Next Features to Come**

- `Linux` compilation.
- `Rendering` feature should come next.

---
_Documentation built with [**`Unreal-Doc` v1.0.9**](https://github.com/PsichiX/unreal-doc) tool by [**`PsichiX`**](https://github.com/PsichiX)_