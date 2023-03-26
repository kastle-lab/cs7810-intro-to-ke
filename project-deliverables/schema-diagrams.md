# Draft Schema Diagrams
1. For each identified pattern, instantiate it into a module. The name of the module is generally the key notion which it models.
2. Utilize [yEd](https://yworks.com/yed) and the graphical syntax found in the [template](../templates/schema-diagram.graphml) to draw the schema diagrams.
3. Place each schema diagram source (`.graphml`) and its `.png` rendering in the `schema-diagrams` directory.
    * Files should have a consistent naming scheme, generally `module-name.graphml` and `module-name.png`.
4. Create a combined schema diagram which links together the individual schema diagram.
5. Create a `schema-diagrams.md` file from the [template](../templates/schema-diagram.md) and place it in the `schema-diagrams` directory. For each schema diagram draft, create a subection for it, and embed the `.png` rendering. 
