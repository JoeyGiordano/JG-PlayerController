==== README ====

--- TITLE ---
JG Player Controller 3d

--- AUTHOR ---
Joey G

--- CONTENTS ---
 Summary
 Dependencies
 Setup
 Features
 Repo Organization
 Assets Organization
 Prefab Organization
 How to Use/Modify
 Acknowledgements

--- SUMMARY ---
  A functional and expandable player controller, movement state machine, and cameara rig. The player controller uses rigidbody physics, and is designed so that other (or new) movement states can be used in conjunction. The movement state machine handles switching between states and works with an abstract template class to make adding new states easy. The camera rig has four 3rd person camera perspectives (uses cinemachine) and a first person perspective (uses unity camera). All of the scripts are heavily commented so that it is easy to make changes.

--- DEPENDENCIES ---
Unity 2022.3, 3d URP or 3d BuiltIn Render Pipeline
Cinemachine

--- SETUP ---
1. Open a new or existing Unity 3D URP Project
2. Install Cinemachine
    a. Window > Package Manager
    b. In the 'Packages' dropdown, choose Unity Registry
    c. Seach Cinemachine
    d. Press 'Install'
3. Import package
    a. With the Unity Editor open, double click the .unitypackage file in the package folder
    b. Select all files
    c. Press 'Import'
4. Prepare for the prefab
    a. Delete (or disable) the MainCamera
    b. Add a new Layer 'Player'
    c. Add a new Layer 'Terrain' (for what the player controller will consider ground, if you don't already have one)
    d. (Optional) Create some ground for the player by adding some cubes to the hierarchy and setting their layer to 'Terrain' (or use the terrain package!)
5. Instantiate Player prefab
    a. Open Assets > Player
    b. Drag the PlayerAndCamera Prefab into the scene
6. Set up player prefab
    a. Open the Prefab into Prefab editing mode
    b. Make sure the Layer of the 'Player' object (PlayerAndCamera > Player) and all its children is set to 'Player' layer (from 4b)
    c. Select the 'Player' object. In the Inspector find the MovementResources script and set the 'Terrain Layer' to 'Terrain' (from 4c)
    d. On PlayerAndCamera > PlayerCam > FirstPersonPlayerCam > Camera, under Camera (Script) > Rendering, set the Culling Mask to include all things you want the first person camera to render. Make sure to select 'Terrain' and deselect 'Player'
    e. On PlayerAndCamera > PlayerCam > ThirdPersonPlayerCam > BrainCamera (it should have a little Cinemachine logo), under Camera (Script) > Rendering, set the Culling Mask to include all things you want the third person camera to render. Make sure to select 'Terrain' and 'Player'
    f. Make sure these changes are applied to the Prefab. (Because of the Cinemachine, it will always say there are Overrides)
7. Run
    a. Run the scene
    b. There should be no errors
    c. To instantiate another PlayerAndCamera in another scene, you should only have to do step 5
    d. Read on to find out how to easily modify the Player Scripts for your game!

--- FEATURES ---
PlayerAndCamera Prefab - all of the scripts prepared and organized on a prefab
Basic Player Model - temporary player model... with googles!
PlayerMovementStateMachine - scripts that manages switching between states
MovementState - abstract class that acts as a template for new movement states
AWSDMovement - script that handles awsd movement (walk, sprint, slopes, grounding) with many adjustable settings (doesn't handle stairs, sorry)
MovementResources - script with many useful flags, references, and methods to use when creating new movement states
Free and Jump MovementState Scripts - two basic example (but probably useful) movement states
6 Other MovementState Scripts - in the 'JG Player Controller - Extra - Unity 3d URP' Package, Crouch, Slide, AirDash, Grapple, WallRun, WallJump. They're not as refined as the other scripts.
PlayerCam (and corresponding script) - easy way to manage the five cameras
FirstPersonPlayerCam (and corresponding script) - a first person camera with lerp based tilt and fov changing
ThirdPersonPlayerCam (and corresponding script) - easy way to manage the 4 third person camera. Uses cinemachine. Easy to create new cameras

--- REPO ORGANIZATION ---
This repo contains four different versions of the player controller, each with its own corresponding project (they're small files, don't worry). The player controllers are made for either the Built In Render Pipeline or the Universal Render Pipeline, and either with or without the extra six movement states. The folders, packages, and projects are labelled accordingly. The URP and Builtin folders also both contain a testing terrain package for that render pipeline. Note: If you make modifications in one pipeline and realize you want to use the other pipeline, it's fairly simple to switch it over guided by the compiler errors.

--- ASSETS ORGANIZATION ---
> Player
   > PlayerAndCamera (Prefab)
   > Model
   > PhysicsMaterials
   > Scripts
      > Camera
         > Perspectives
      > GeneralUse
      > Movement
         > States

--- PREFAB ORGANIZATION ---
Note: if the description says folder, the gameobjects doesn't have scripts, it's purely organizational.
> PlayerAndCamera
  > Player - The object with the rigidbody, collider, and all the movement scripts. Player and all its children should be tagged Player.
    > Feet(forPhysics) - A sphere collider to give the bottom of the player static friction without affecting the sides.
    > Orientation - Stores the direction the player is facing. Rotated by cameras based on input.
      > Locations - Folder for transforms important points on the player
        > BottomOfPlayer - Transform at the bottom of the player collider
        > TopOfPlayer - Transform at the top of the player collider
        > CenterOfPlayer - Transform at the center of the player collider
      > CameraTargets - Folder for transforms of important points for the cameras
        > CameraPosFirstPerson - Transform at the location of the "eyes" for first person view
        > CameraTargetThirdPerson - Transform that third person views point at
        > CameraTargetCombat - Transform that combat view points at
    > PlayerModel - Holds all parts of the player model. Rotated by cameras based on input (not always exactly like Orientation)
      > ... (irrelevant)
  > PlayerCam - Holds all player cameras. To disable all player cameras disable this object (no other method calls needed)
    > FirstPersonPlayerCam - Holds a camera and points it accordingly, disable to turn of first person cam (no other method calls needed)
      > Camera - Camera for first person view
    > ThirdPersonPlayerCam - Holds cameras for third person views and switches between them, disable to turn of third person cam (no other method calls needed)
      > BrainCamera - Cinemachine Brain and Camera script
      > PlayerCam___ - 4 virtual camera objects that give different 3rd person views of the player

--- HOW TO USE/MODIFY ---
Add movement states:
Instructions in the PlayerMovementStateMachine script.

Add cameras:
Instructions in the PlayerCam and ThirdPersonPlayerCam scripts.

--- ACKNOWLEDGEMENTS ---
Dave / GameDevelopment - https://www.youtube.com/@davegamedevelopment
