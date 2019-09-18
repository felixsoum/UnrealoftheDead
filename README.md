# UnrealoftheDead
![UnrealoftheDead](https://user-images.githubusercontent.com/6082364/65124555-e3c91600-d9c2-11e9-942f-01740e4ae260.png)

## Gfycat Preview
https://gfycat.com/yawningevergreenamazonparrot

## Instructions (en)

### Create BP_Zombie
1. Use the yellow mannequin SK
1. Add variable PatrolLocation (vector, public)
1. Put 2 zombies in the level and specify their PatrolLocation
1. Lower walk speed to 25

### Create BB_Zombie
1. Add vector key SpawnLocation
1. Add vector key PatrolLocation

### Create BT_Zombie
1. Assign its Blackboard: BB_Zombie
    1. Clear and redo if variables don't appear
    1. Create sequence of move to patrol, move to spawn, then wait

### Create AIC_Zombie
1. Add event On Possess
    1. Connect with Run BT and use BT_Zombie
    1. Cast pawn to BP_Zombie and promote it
    1. Set the PatrolLocation vector value
       1. Careful to use blue version of Blackboard variable
1. Go to BP_Zombie and set its AIController to this

### Add nav mesh
1. Add nav mesh bounds from volumes in modes window
1. Change to top view then use R to resize
1. Change to right view and resize also
1. Press P to see nav mesh
1. Test PIE

### Fix BP_Zombie
1. Fix mesh rotation
1. Fix turn snapping
    1. Uncheck Use Controller Rotation Yaw in root
    1. Check Use Controller Desired Rotation in CharacterMovement

### Import Zombie assets
1. Rename, rename, rename!
1. Fix material
1. Setup animation
    1. Try the Blend Space 1D
        1. Set Target Weight Interpolation to 2
        1. Add animations

### Prepare wandering behavior
1. Add decorator to sequence to only run if PatrolLocation is set
1. Add logic in AIC to only set PatrolLocation if unequal to 0 vector
1. Create WanderLocation in BB
1. Create new BTTask_Wander
    1. Implement wander with GetRandomReachablePointInRadius
    1. Set blackboard value with WanderLocation and make sure it is InstanceEditable
    1. Use it in the BT

### Prepare chasing behavior
1. Add AI Perception component to AIC_Zombie
    1. Set senses config to AI Sight config
        1. Set Sight Radius to 500
        1. Set Les Sight Radius to 1000
        1. Set Peripheral Vision to 60
    1. Make sure to sense neutral affiliation
    1. Add OnTargetPerceptionUpdated binding
1. Add Player tag to player BP
1. Add funtion to change walk speed in BP_Zombie
1. Add BTTask_Chase to change speed to 400

### Add line trace damage
1. Add line trace to gun
1. Readjust crosshair (-5 height)
1. Change BP_Zombie mesh physics preset to block visibility
1. Add damage function to BP_Zombie and call it
    1. Set attacker input to pass to blackboard
