# Identify Key Notions
1. Create a `key-notions.md` file from the `key-notions.md` [template](../templates/key-notions.md) and place it in the `deliverables` directory.
2. Identify a thorough list of key notions. 
    * For each key notion, explain your rationale of why it is a key notion.
    * For each key notion or set of key notions, identify a pattern which can be used to model them, otherwise indicate that there is no existing pattern.
        * Draft an instantiation of the pattern (a module) based on your use-case, where possible.
        * For key notions with no pattern, draft a module which would model them.
    * Connect the key notion to where the data is coming from. So if you have an Event as your keynotion, which piece of your identified datasets are you using to model this.
        * Occasionally you will have "controlled vocabularies." These are not really patterns, but just a list of individuals that are important (and will not change). Indicate which key notions behave as such and their list of individuals.
3. Utilize [yEd](https://yworks.com/yed) and the graphical syntax found in [this example](../templates/schema-diagram.graphml) to draw the schema diagrams.
4. Place each schema diagram draft into a folder called `schema-diagrams/` with a `.png` rendering.
    * Create a combined schema diagram draft which links together the appropriate drafts.
5. Create a `schema-diagrams.md` file. For each schema diagram draft, create a subection for it, and embed the `.png` rendering. 

**Note:** Ensure that each member contributes in explicit commits. Do not squash commits; the `git` history will serve as a record of participation and contribution.
