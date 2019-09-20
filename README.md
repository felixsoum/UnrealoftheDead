# UnrealoftheDead
![UnrealoftheDead](https://user-images.githubusercontent.com/6082364/65124555-e3c91600-d9c2-11e9-942f-01740e4ae260.png)

## Gfycat Preview
https://gfycat.com/yawningevergreenamazonparrot

## Instructions (en)

### Create BP_Zombie
1. The parent class is Character
    1. Change the SK and you can add static meshes as child, but make sure they no collision
1. Add variable PatrolLocation (vector, public)
1. Put 2 zombies in the level and specify their PatrolLocation
1. Optional: lower walk speed to 25

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
1. Optional: Add funtion to change walk speed in BP_Zombie
    1. Add BTTask_Chase to change speed to 400

### Add line trace damage
1. Add line trace to gun
1. Readjust crosshair (-5 height)
1. Change BP_Zombie mesh physics preset to block visibility
1. Add damage function to BP_Zombie and call it
    1. Set attacker input to pass to blackboard

## Instructions (fr)

### Créer BP_Zombie
1. La classe parente est Character
    1. Modifiez le SK et vous pouvez ajouter des maillages statiques comme enfant, mais assurez-vous qu’ils ont aucune collision
1. Ajouter la variable PatrolLocation (vector, public)
1. Mettez 2 zombies dans le niveau et spécifiez leur PatrolLocation
1. Facultatif: réduire la vitesse de marche à 25

### Créer BB_Zombie
1. Ajouter une clé vectorielle SpawnLocation
1. Ajouter la clé vectorielle PatrolLocation

### Créer BT_Zombie
1. Attribuer son tableau: BB_Zombie
    1. Effacer et refaire si les variables n'apparaissent pas
    1. Créez une séquence de déplacement pour patrouiller, déplacez-vous au spawn, puis attendez

### Créer AIC_Zombie
1. Ajouter l'événement On Possess
    1. Connectez-vous avec Run BT et utilisez BT_Zombie
    1. Castez le pion à BP_Zombie et le promouvoir en variable
    1. Définir la valeur du vecteur PatrolLocation
       1. Attention à utiliser la version bleue de Blackboard variable
1. Allez sur BP_Zombie et configurez son contrôleur AIC sur ceci

### Ajouter un maillage de navigation
1. Ajouter des limites de maillage de navigation à partir de volumes dans la fenêtre de modes
1. Passez en vue de dessus puis utilisez R pour redimensionner
1. Changer en vue de droite et redimensionner aussi
1. Appuyez sur P pour voir le maillage de navigation
1. Test PIE

### Correction de BP_Zombie
1. Correction de la rotation du maillage
1. Fixer la rotation trop rapide
    1. Décochez la case "Use Controller Rotation Yaw in root"
    1. Cochez la case "Use Controller Desired Rotation in CharacterMovement" dans CharacterMovement.

### Importer des ressources Zombie
1. Renommer, renommer, renommer!
1. Réparer le matériel
1. Installer les animations
    1. Essayez le Blend Space 1D
        1. Définissez l'interpolation du poids cible sur 2
        1. Ajouter des animations

### Préparer un comportement "wandering"
1. Ajoutez le décorateur à la séquence à exécuter uniquement si PatrolLocation est défini
1. Ajouter une logique dans AIC pour définir uniquement PatrolLocation si non égal à vector 0
1. Créer WanderLocation dans BB
1. Créer un nouveau BTTask_Wander
    1. Implémentez wander avec GetRandomReachablePointInRadius
    1. Définissez la valeur du tableau avec WanderLocation et assurez-vous qu’il est InstanceEditable
    1. Utilisez-le dans le BT

### Préparer le comportement de poursuite
1. Ajouter la composante AI Perception à AIC_Zombie
    1. Définissez la configuration des sens sur AI Sight
        1. Définissez le rayon de visée sur 500
        1. Réglez le rayon de vue sur 1000
        1. Définissez la vision périphérique sur 60
    1. Assurez-vous de sentir une affiliation neutre
    1. Ajouter une liaison OnTargetPerceptionUpdated
1. Ajouter un tag de joueur au joueur BP
1. Facultatif: Ajouter une fonction pour changer la vitesse de la marche dans BP_Zombie
    1. Ajoutez BTTask_C hase pour modifier la vitesse en 400

### Ajouter des traces de ligne
1. Ajouter un tracé de ligne au pistolet
1. Réajustez le réticule (hauteur -5)
1. Modifiez le paramètre prédéfini Physique du maillage BP_Zombie pour bloquer la visibilité.
1. Ajoutez la fonction de dommage à BP_Zombie et appelez-le
    1. Définir l’attaquant pour qu’il passe au tableau
