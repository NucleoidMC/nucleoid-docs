# Adding taters to Nucleoid Extras

## Add tater

1. Fork [Nucleoid Extras repository](https://github.com/NucleoidMC/nucleoid-extras)
2. Create a branch `namehere-taters` where `namehere` refers to the tater kind
3. Navigate to [en_us.json](https://github.com/NucleoidMC/nucleoid-extras/blob/1.19.4/src/main/resources/data/nucleoid_extras/lang/en_us.json#L54)
4. Copy an existing tater line
5. Paste it, and make sure the name reflects the one you want to add
6. Go to [NEItems.java](https://github.com/NucleoidMC/nucleoid-extras/blob/1.19.4/src/main/java/xyz/nucleoid/extras/lobby/NEItems.java)
7. Copy existing tater lines - `public static final` and the `register` one
8. Change values according to your tater's name
9. Go to [NEBlocks.java](https://github.com/NucleoidMC/nucleoid-extras/blob/1.19.5/src/main/java/xyz/nucleoid/extras/lobby/NEBlocks.java)
10. Copy existing tater lines
11. Change values according to your tater's name, change the effect if needed [(color picker here)](https://rgbcolorcode.com)
9. Upload the head skin to [MineSkin](https://mineskin.org) [(templates here)](https://minecraft.fandom.com/wiki/Skin#Official_skin_templates)
10. Copy the generated URL that starts with `ewog`
11. Paste it to your tater's row, replacing the existing `ewog`
11. Commit and push
12. Create a pull request

## Edit tater image

1. Copy the `ewog`
2. [Paste it here](https://www.base64decode.org)
3. Copy the textures -> SKIN -> url value
4. Download the image
5. Edit it
6. See adding instructions for adding the updated one back

Instructions based on [this Discord message](https://discord.com/channels/733462796582387753/744090136945360936/913463834994413618)
```.
