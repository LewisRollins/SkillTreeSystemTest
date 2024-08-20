Skill Tree System README
Project Overview

This project implements a skill tree system in Unreal Engine using Blueprints. It includes functionalities for unlocking skills, managing skill dependencies, and displaying the skill tree in a user interface. The project is structured to allow easy modification and extension by designers and developers.
Key Components
1. BP_SkillTreeManager

    Responsibilities:
        SpawnSkills(): Initializes and spawns all skill nodes in the skill tree.
        IsSkillUnlockable(): Checks if a skill can be unlocked based on dependencies and prerequisites.
        UnlockSkill(): Unlocks a skill and updates the skill tree state.

2. WBP_SkillTree (Widget)

    Responsibilities:
        Parses and sets all skill information in the UI.
        Handles the input for unlocking skills through the UI.
        Communicates with the SkillTreeManager to update the skill tree state.

3. WBP_SkillNode (Widget)

    Responsibilities:
        Parses and displays individual skill information.
        Handles the input for selecting and interacting with skill nodes.
        Dispatches events that are bound in the character blueprint.

4. BP_ThirdPersonCharacter

    Responsibilities:
        Initiates the skill tree system and constructs the SkillTreeManager object.
        Binds to events to handle skill tree UI animations and skill unlocking logic.
        Manages the opening and closing of the skill tree menu.

Note: On reflection I would move the interaction and timeline logic from the SkillTreeAnimationGraph on the ThirdPersonCharacter to SkillTreeManager. This would require the SkillTreeManager to inherit from Actor instead of Object to access timelines

Setup Instructions
1. Adding New Skills

To add new skills to the skill tree, follow these steps:

    Create a New Skill:
        Create a child class of BP_Skill.
        Set all relevant variables, including the skill tree position index, which determines where the skill will appear on the skill tree.

    Update Skill Manager:
        Open BP_SkillManager.
        Add the newly created skill classes to the Skills array.

    Update Skill Tree Widget:
        Open WBP_SkillTree.
        Add instances of WBP_SkillNode to the design graph.
        Position the skill nodes according to the desired layout.
        Ensure that each WBP_SkillNode has its skill tree position index set to match the corresponding skill in BP_SkillManager.

2. Using Skills

    To check if a skill is available for use, reference the SkillRef array in the SkillManager.
    Unlocked skills can also be modified by making changes to these references.
    To reward new skill points, increment the NumberOfSkillPoints variable in the SkillManager.
