# Unreal Course

These are my notes about the C++ Unreal Course on Udemy:
https://www.udemy.com/course/unrealcourse/

## Using vim for editor

I'm going to try to use vim for my IDE but if it goes wrong I can move over to
QT Creator or vscode

## Other notes

* [vim-cpp-setup.md](vim-cpp-setup.md)

## Code Style / Coding Standard / Asset Naming

* [learncpp.com](https://www.learncpp.com/cpp-tutorial/whitespace-and-basic-formatting/)
doesn't have a preference for tabs vs spaces but does prefer 1TB (One True
Brace) style for brackets.
* Unreal Engine Coding Standards: https://docs.unrealengine.com/en-US/Programming/Development/CodingStandard/index.html
* A good resource for naming https://www.tomlooman.com/ue4-naming-convention/
* From the course: https://web.archive.org/web/20181207033857/https://wiki.unrealengine.com/Assets_Naming_Convention
* Opinionated naming conventions: https://github.com/Allar/ue4-style-guide

## Debugging

### Dispossessing the Pawn

Use the Eject button (F8) to dispossess the Pawn

### Toggle Debug Camera

Use the console (\`) and use the command `toggleDebugCamera`

### Coursework Repo

https://github.com/overbyte/unrealcourse/

UPDATE: this is deprecated in favour of separate repos for each project. I've
kept it for history


# Section 2 Triplex

[Coursework link](https://github.com/overbyte/unrealcourse-section-2-triplex)

## Compiling C++ on Linux

Pass the main file into `g++`

### Example

```
g++ main.cpp -o applicationname
```

**TODO**: We should probably create a `MakeFile` to simplify this process

#### Research

* https://www.gnu.org/software/make/manual/make.html
* https://courses.cs.washington.edu/courses/cse373/99au/unix/g++.html
* https://stackoverflow.com/questions/2481269/how-to-make-a-simple-c-makefile

# Section 3 BullCowGame

[Coursework link](https://github.com/overbyte/unrealcourse-section-3-bullcow)

## Notes

### using #includes

Note: including the class.h should happen at the bottom of the list of includes.

Example (in `Grabber.cpp`):
```
#include "DrawDebugHelpers.h"
#include "Engine/World.h"
#include "Grabber.h"
```

### const methods

const methods are methods which don't mutate member variables.

Example
```
void UBullCowGameCartridge::IsIsogram(FString Word) const
```

### Parameters vs Arguments

* Parameters are given in a method declaration
* Arguments are the values that are passed using the parameters

### Using References

When we use the following in our method declaration:

```
void UBullCowGameCartridge::MyMethod(FString Guess)
```
we are actually taking a copy of the Guess FString that is passed as an
argument. If we don't intend to do any local mutations to that variable, it is
more efficient to use a reference to the original variable. 

This is done with a & at the end of the type:
```
bool IsIsogram(const FString& Word) const;
```

It is preferable to make this a `const` because it would be a bad side effect to
mutate the original variable unless you want to use an out parameter

#### Using out parameters

To use an out parameter, we declare a variable outside the method, use a
non-const reference parameter and mutate the state of that variable from within
the method. 

Seems shady as balls - all side-effect.

Example:
```
int32 Bulls, Cows;
GetBullCows(Guess, Bulls, Cows);

void UBullCowCartridge::GetBullCows(const FString& Guess, int32& BullCount, int32& CowCount) 
{
    ...
```

### Defining structs

`struct`s can be defined in the header file outside the class

```
...
#include "BullCowCartridge.generated.h"

struct FBullCowCount
{
    int32 Bulls = 0;
    int32 Cows = 0;
};

UCLASS(ClassGroup=(Custom), meta=(BlueprintSpawnableComponent))
class BULLCOWGAME_API UBullCowCartridge : public UCartridge
{
    ...
```

Note: can be initialised and must be terminated with a ;


# Section 4 Building Escape

[Coursework link](https://github.com/overbyte/unrealcourse-section-4-building-escape)

### Using pointers

Pointers are variables that contain memory addresses that allow us to refer to
memory, potentially set up by another part of the application.

Pointers can be classes, structs or variables and members can be referenced with
either a dereference by adding a `*` to the pointer name and using brackets or
the arrow operator `->`.

Dereferencing allows us to treat the pointer as the object it references.

Dereference Example:
```
(*Brogrammer).StartCoding();
```

Arrow operator Example:
```
Brogrammer->StartCoding();
```

### Logging in UE4

Example:
```
UE_LOG(LogTemp, Warning, TEXT("This is a warning"));
UE_LOG(LogTemp, Warning, TEXT("Text, %d %f %s"), intVar, floatVar, *fstringVar);
```

Types:

* Error: Red
* Warning: Yellow
* Display: Grey

Template:

* `%d`: int
* `%i`: int
* `%f`: float
* `%s`: string - requires a pointer

### Viewport

Button in top right of viewport will give quad view



### Modeling and Level Creation

#### Using Materials

* import a PNG
* right click and create material
* double click material to access material blueprint
* in content browser, right click material and create material instance to allow
  multiple scales etc

##### FFMPEG Conversion from TIF to PNG

```
ffmpeg -i TexturesCom_Wall_Cobblestone_3x3_1K_normal.tif cobblestone_normal_tex.png
```

#### Using BSP

By using the Geometry mode we can quickly rough in a bunch of shapes and items
for a level. 

Note: in the brush settings for each shape there is an additive and a
subtractive mode for each shape. Also note, by having a material selected when
the shapes are dragged out, they are automatically set.

The BSP can be converted to meshes under brush settings (may need to be
expanded)

#### Addiing code to objects

An object must be changed from a static mesh which bakes lighting and cannot be
dynamically moved to a `Moveable Object` which include dynamic lighting and can
be updated with code (See the door in the scene)

#### Fixing Player Collision and Visibility Collision view modes

Go to (top left of viewport) Show->Developer->Ray Tracing Debug

Player collision: shows collidable objects
Visibility Collision: shows visible collision (so in this mode, we can raycast
through a window, for example)

Colours:

* Pink: movable static mesh
* Cyan: static mesh
* Purple: stationary mesh
* Green: Trigger Volume
* Teal: Simulates Physics

#### Note About GetName()

There's a lot of use of `GetOwner()->GetName()` which is a weird case (currently
doesn't autocomplete in vim). 

Although `GetOwner()` returns a pointer to an `AActor` which does not have a
`GetName()` method, it actually comes from `UObjectBaseUtility`:
https://docs.unrealengine.com/en-US/API/Runtime/CoreUObject/UObject/UObjectBaseUtility/GetName/1/index.html

Forum Ref: https://community.gamedev.tv/t/aactor-getname/129972/2

#### Drawing debug lines

commit: https://github.com/overbyte/unrealcourse-section-4-building-escape/commit/a5d8d731cd772283276f1e1796215054c157d70e

Getting player viewpoint is very useful for first and third person games

we can also draw debug lines to show this

(Note Reach is a float to give the radius for the vector which will be 0-1 -
unit-based)

```
FVector PlayerViewPointPosition;
FRotator PlayerViewPointRotation;
GetWorld()->GetFirstPlayerController()->GetPlayerViewPoint(
    OUT PlayerViewPointPosition,
    OUT PlayerViewPointRotation
);

FVector LookAtPosition = PlayerViewPointPosition + (PlayerViewPointRotation.Vector() * Reach);

DrawDebugLine(
    GetWorld(),
    PlayerViewPointPosition,
    LookAtPosition,
    FColor(0, 255, 0),
    false,
    0.f,
    0,
    5.f
);
```

#### Raycast

To use a raycast collision, we can do the following

commit: https://github.com/overbyte/unrealcourse-section-4-building-escape/commit/a5d8d731cd772283276f1e1796215054c157d70e

```
// out param for raycast
FHitResult Hit;

// collision query params (no name, don't use complex collision, ignore this
// owner object
FCollisionQueryParams CollisionParams(
    FName(TEXT("")),
    false,
    GetOwner()
);

GetWorld()->LineTraceSingleByObjectType(
    OUT Hit,
    PlayerViewPointPosition,
    LookAtPosition,
    FCollisionObjectQueryParams(ECollisionChannel::ECC_PhysicsBody),
    CollisionParams
);
```

### Setting the default pawn

to change the player pawn, we need to:

* create new gamemode by creating a blueprint child of the GameModeBase C++
  class
* in the gamemode blueprint, set the default pawn class to a pawn blueprint

### pre-initialising classes / structs

Can use any of the following:
(note FRotator is a struct)

```
FRotator CurrentRotation;
CurrentRotation.Yaw = 90.f;
GetOwner()->SetActorRotation(CurrentRotation);
```

or
```
FRotator CurrentRotation{0.f, 90.f, 0.f};
GetOwner()->SetActorRotation(CurrentRotation);
```

or
```
FRotator CurrentRotation(0.f, 90.f, 0.f);
GetOwner()->SetActorRotation(CurrentRotation);
```

### Setting up collision on a mesh

There is simple collision which is always preferable but doesn't handle doorways
as they have holes in them. The collision should be set up in the model fbx but
if it isn't you can do any of the following (double click the mesh to open):

* Under Collision in the top menu, remove collision 
* In the detail panel under collision, use complex collision as simple will
  produce expensive collision
* Remove collision and create a new mesh from BSPs - remember to
  convert to mesh - Details Panel:Brush Settings:Create Static Mesh - and use
  complex collision as simple on this object instead.

really are better off getting an artist to do it in the model if poss

### Using Interpolation to animate

`FMath::Lerp(CurrentRotation, TargetRotation, Speed)` will allow per-frame
changes withing `AActor::TickComponent()`

to make this framerate agnostic, always multiply `Speed` by the `DeltaTime`
parameter.

Example:
```
CurrentYaw = FMath::Lerp(CurrentYaw, TargetYaw, DeltaTime * OpenSpeed);
FRotator DoorRotation = GetOwner()->GetActorRotation();
DoorRotation.Yaw = CurrentYaw;
GetOwner()->SetActorRotation(DoorRotation);
```

We can also use `FMath::FInterpTo(CurrentNum, TargetNum, DeltaTime, Speed)`
which includes this calculation as well. 

Example:

```
CurrentYaw = FMath::FInterpTo(CurrentYaw, TargetYaw, DeltaTime, OpenSpeed);
FRotator DoorRotation = GetOwner()->GetActorRotation();
DoorRotation.Yaw = CurrentYaw;
GetOwner()->SetActorRotation(DoorRotation);
```

# Section 7 BattleTank

[Courseworklink](https://github.com/overbyte/unrealcourse-section-7-tank-battle)

## Landscape

A Landscape is made of a mesh of Quads, created in sections, in numbers of
Components

### Landscape Creation

Go to the Landscape tool to generate

* Scale will set the size of the quads in cm (x and y are the most important)
* Section Size sets the number of Quads in a section
* Number of Components sets the number of sections on an axis (x and y)
* Overall Resolution will give the total size of the Landscape

### Sculpting

Using the Landscape tool in sculpt mode, raise (or lower with shift) the ground.

* Sculpt: raise or lower terrain based on brush size and falloff (blur)
* smooth: normalise the terrain to smooth it out
* 

#### Importing a file to generate terrain

Export the existing terrain to a terrain map by going to the terrain tool, right
click on Height map and export.

We can import a grayscale file (created with terragen or similar) when the
Landscape is being created.

## Creating a Controllable Pawn Blueprint

The tank is created from 4 meshes which have an origin at the pivot point (or
the floor in the case of the tracks).

To create the blueprint, 
* create a new Pawn blueprint
* in the viewport add the tank body as a `static mesh`
* in the mesh object for the tank body add sockets for the turret and 2 tracks
  (note this is a weird set of instructions but gets around a bug in the editor):
  * add a socket (do not rename yet)
  * set the socket mesh to the turret
  * position the socket
  * clear the mesh from the socket
  * rename the socket to `Turret`
* add a turret as a child of the body mesh using the Turret socket
* set the socket to be the `Turret` socket
* repeat for the tracks
* in the Turret mesh add a socket for the barrel
If, once the child meshes are added with the sockets in the blueprint, they are
not in the expected place, set their xyz coordinates to 0 again.

We can simplify it a bit by setting the tank body to be the root element by
dragging it over the default.

To make physics apply to the element, in the blueprint, check the `simulate
physics` box and assign a weight in kg on the tank body (root element)
root element.

## Setting up input

* In `BP_Tank`
  * Create a new Event Graph called `InputBindingGraph`
* In project settings
  * in engine:input, add control called `AimAzimuth` - see
    [this](https://en.wikipedia.org/wiki/Azimuth) - it's the diameter of the
    sphere that we're moving the camera in (note: it's yaw for mapping purposes)
    * add x axis mouse input 
    * add right-stick-x axis
  * do the same for `AimElevation` on the y axis
* add blueprint
![input blueprint](images/unrealcourse-section-7-tank-input-blueprint.png)
  * notes
    * this multiplies the spring arm azimuth by world delta seconds and 100 and
      pipes it into the yaw
    * this multiplies the spring arm elevation by world delta seconds and 100 and
      pipes it into the pitch
* to stop the rotation to start rolling when the camera is both pitched and
  yawed add a `scene` component to use as a gimbal to use for azimuth rotation
  and parent it to tank (named `AzimuthElevation`)
  * make the spring arm a child of this
  * the gimbal is the camera target - translate z by 150 cm to target the tank
    top or it will end up on the floor
  * reset the position and rotation of the spring arm and camera so the camera
    ends up on the end of the spring arm (marked in red)
  * increase the length of the spring arm to push the camera away and rotate the
    spring arm to elevate the camera
  * update the blueprint to make the scene input elevation use the gimbal as the
    target
* to stop the camera from rolling when the tank is at an angle (ie on a slope),
  on the springarm, uncheck the `inherit roll` box

## Adding player UI

* create a 'user interface:widget blueprint'
* add an image to the interface 
  * move the anchor from the center to where the image should be on the screen -
    this is a ratio to make it relative to screen resolution
  * reset the position x and y numbers
  * set the size x and y
  * set the alignment to x=0.5, y=0.5 to center the image on the anchor
* create a `Player Controller` blueprint and add 
  * create ui widget
  * add to viewport
![player controller blueprint](images/unrealcourse-section-7-create-player-ui.png)
* update the player controller section of the BattleTank Game Mode

Notes:

* for a main menu level, we can use the level blueprint instead of using the
  player controller blueprint
* for main menus, if we want a background image that scales to fill, we add a
  scale box component and make the image a child of it
  * set the anchors of the scale box to fill the screen
  * set the offsets to 0
  * reset the size of the image so it scales correctly
* to turn on the mouse (eg for a menu), in the level blueprint for the main
  menu
  * get the player controller
  * set the mouse cursor (click the checkbox)
  * attache the mouse cursor to the end of the add to viewport
![main menu level blueprint](images/unrealcourse-section-7-main-menu-ui.png)

### Enabling the start button

from the `BP_MainMenuUI` Event Graph

* use the `on button clicked` button on the button in the designer panel
* from the new event use `Open Level` and add the name of the gameplay level

### Adding controller support to start page

* create a widget ready custom event at the end of the chain in the `MainMenu`
  level blueprint

![main menu level blueprint update](images/unrealcourse-section-7-main-menu-ready.png)

* update the `BP_MainMenuUI` with a listener for the widget ready event
* set the input mode ui only to the start button
* once the level is open, set it back to game mode only

![main menu ui with controller](images/unrealcourse-section-7-main-menu-ui-controller.png)

### Adding fonts

Download the .ttf and import it to the project.

* version used is [Series Orbit](https://www.dafont.com/seriesorbit.font?l[]=10&l[]=1)

### Blueprint parent classes

We can reparent a blueprint class by

* taking note of its superclass in the top right of the blueprint graph editor
  screen
* create new C++ class of the same type
* select the new C++ class from the blueprint `Class Settings`

## C++ Polymorphism

demo can be found at https://github.com/overbyte/unrealcourse-7a-polymorphism-demo
along with notes

## posessing the tank with an AI controller

* create new C++ class and select `show all classes` to select the AIController
  and create `TankAIController`
* in the `BP_Tank`
  * make sure `Auto Possess` is off
  * make sure `Auto Possess AI` is set to `Placed in the world`
  * set the AI Controller class to new `TankAIController`

## Example raycast by channel

The Player Controller includes a raycast to look at a point indicated in the UI
with a dot (called the crosshair)

https://github.com/overbyte/unrealcourse-section-7-tank-battle/blob/master/BattleTank/Source/BattleTank/Private/TankPlayerController.cpp

```

bool ATankPlayerController::GetLookVectorHitLocation(const FVector &LookDirection, FVector &OutHitLocation) const
{
    FHitResult OutHitResult;

    FVector StartLocation = PlayerCameraManager->GetCameraLocation();
    FVector EndLocation = StartLocation + LookDirection * ProjectileRange;

    if (GetWorld()->LineTraceSingleByChannel(
            OutHitResult,
            StartLocation,
            EndLocation,
            ECollisionChannel::ECC_Camera
        )
    )
    {
        OutHitLocation = OutHitResult.Location;
        return true;
    }

    OutHitLocation = FVector(0.f);
    return false;
}

```
notes
* `OutHitLocation` is an out paramter (that is a reference to state that is
  mutated as a side effect of this method. Icky but all over Unreal probably
  because the scope holds the memory
* The `GetLookDirection` method de-projects the point indicated by the UI to a
  world position
* `ScreenLocation` should probably be renamed to something like
  `CrosshairLocation2D` to be more descriptive
* `FCollisionQueryParams` adds `GetPawn()` (instead of `GetOwner()`) to be
  ignored when considering the ray cast collision
* `ECollisionResponse::ECR_Block` is a guess and should probably be removed to
  allow the default to go in - the [docs](https://docs.unrealengine.com/en-US/API/Runtime/Engine/Engine/ECollisionResponse/index.html)
  are frustratingly non-descriptive

## The C++ Compilation

It is prefereable to include header files for other classes in the cpp file but
not in the header file for a class. This is to avoid dependency problems later
on. It does mean, however that the headers should be added int he order they're
required.

### Forward declarations

We can get around the need to use one of our class header files in another
header file by using a forward declaration. We need to declare the class in the
header file that depends on it. We will then redeclare it in the actual header /
implementation file

Example: `TankAimingComponent.h` re: `TankBarrel`

```
  7 #include "TankAimingComponent.generated.h"
  8
 11 class UTankBarrel;
 12
 13 UCLASS( ClassGroup=(Custom), meta=(BlueprintSpawnableComponent) )
 14 class BATTLETANK_API UTankAimingComponent : public UActorComponent
 15 {
 16     GENERATED_BODY()
 17
 25 private:
 26     UTankBarrel* Barrel = nullptr;
```

## make variable editable in blueprints

in the header file where the property is declared 

```
UPROPERTY(EditAnywhere, Category = Setup)
```

Notes:
* `EditAnywhere` allows the var to be editable per instance of the blueprint
  * `EditDefaultsOnly` will only allow the var to be edited in the blue
  * `VisibleAnywhere` read-only on all instances

## making component blueprint spawnable

in the header file, add the following to the UCLASS declaration

```
UCLASS(meta = (BlueprintSpawnableComponent))
```

This will allow the C++ component to be able to be used in a blueprint (will
appear in the components list to be dragged to the blueprint)

Drag this as a child of the turret, add it to the event graph (blueprint) and
hook it up to the `Set Barrel Reference` (which expects an object of type,
`TankBarrel`) node to fix the errors

To give some useful information, add a comment before the UCLASS declaration -
this will be available in the tooltip

Some other interesting options:

##### Remove categories from blueprint (to stop designer misusing them)

Example: remove the collision section from a component

```
UCLASS(meta = (BlueprintSpawnableComponent), hidecategories = ("Collision"))
```

## How the barrel elevates

![How the barrel elevates](images/unrealcourse-section-7-howthebarrelelevates.png)

Commits:
* https://github.com/overbyte/unrealcourse-section-7-tank-battle/commit/3bd5504644d9f6351e336a8d5258e143eace96a2

## Rotating the turret

Very similar to elevating the barrel 

Commits:
* https://github.com/overbyte/unrealcourse-section-7-tank-battle/commit/484bb1e817d40143aab65775507829a0837b23ed

## Launching a projectile

* Create a C++ class called project
* Create a blueprint from the C++ class
* add a default subobject to the project of UProjectileMovementComponent and
  turn off bAutoActivate so we can set parameters manually
* at launch, set initial velocity in local space on the movement component
* then activate it

Commits:
* https://github.com/overbyte/unrealcourse-section-7-tank-battle/commit/e7027f805b3281f2315693f6b78ba96cd5323d90
* https://github.com/overbyte/unrealcourse-section-7-tank-battle/commit/5659afe8c998cf5a2dcec6f1280cdf834af7db82

## Moving the tank

### Silly version with sliding and kerazy physics

Apply a forward force (from -1 to +1) to each track with a `SetThrottle` method.

```
void UTankTrack::SetThrottle(float Throttle) 
{
    FVector ForceApplied = GetForwardVector() * Throttle * MaxDrivingForceNewtons;
    FVector ForceLocation = GetComponentLocation(); 
    PrimitiveComponent *TankRoot = Cast<UPrimitiveComponent>(GetOwner()->GetRootComponent()); 
    TankRoot->AddForceAtLocation(ForceApplied, ForceLocation);
}
```

Notes:
* `MaxDrivingForceNewtons` is a multiplier to create enough force to drive the
  weight of the tank (about 4000kg)
* `GetComponentLocation` is used to apply the force at the center of the track
  (where it is attached to the socket)
* get the root of the track component and apply force - simple and silly

This shows the 2 types of movement controls - manual forward / backwards drive
to the tracks and fly-by-wire controls on the left thumbsticks. The manual
version will be removed as the fly by wire option is much more comfortable.

![Movement Control Blueprints](images/unrealcourse-section-7-movementcontrols.png)

### Applying sideways force to stabilise the movement

In TankTrack.cpp

```
void UTankTrack::ApplySidewaysForce()
{
    FVector RightVelocity = GetRightVector();
    FVector ForwardVelocity = GetComponentVelocity();
    float SlippageSpeed = FVector::DotProduct(RightVelocity, ForwardVelocity); 
    // work out the required acceleration in m/s/s to correct this slippage
    float DeltaTime = GetWorld()->GetDeltaSeconds();
    FVector CorrectionAcceleration = -SlippageSpeed / DeltaTime * RightVelocity;
    // calculate and apply sideways friction (opposite acceleration) for F = ma
    // note: there are two tracks so divide by 2
    UStaticMeshComponent *TankRoot = Cast<UStaticMeshComponent>(GetOwner()->GetRootComponent());
    FVector CorrectionForce = (TankRoot->GetMass() * CorrectionAcceleration) / 2;
    TankRoot->AddForce(CorrectionForce);
}
```

### Only drive when track is in contact with an object

to stop the tank going nuts in the air because force is still being applied:

```
void UTankTrack::BeginPlay()
{
    Super::BeginPlay();

    // register delegate for oncomponenthit events
    OnComponentHit.AddDynamic(this, &UTankTrack::OnHit);
}

void UTankTrack::OnHit(UPrimitiveComponent* HitComponent, AActor* OtherActor, UPrimitiveComponent *OtherComponent, FVector NormalImpulse, const FHitResult& Hit)
{
    DriveTrack();
    ApplySidewaysForce();
    CurrentThrottle = 0;
}
```

## using pathfinding ai in the AIController

* Create a navmesh volume on the landscape for the AI to calculate the paths for
![How Pathfinding works](images/unrealcourse-section-7-pathfinding.png)

Notes:
* `MoveToActor()`
* `RequestDirectMovement` 

* to decide how to move towards the player tank, use the safe normal, dot
  product of the `MoveVelocity` FVector to determine the forward (+) / backward
  (-) intent (Note the desire is to stop moving when the ai tank is alongside
  the player tank)
* to decide how to turn towards the player tank, use the safe normal, Z-axis of
  the *cross* product of the `MoveVelocity` FVector

Notes:
* `MoveVelocity` is the distance vector to the next point in the path determined
  by the pathfinding combination of 
  `AAIController::MoveToActor()` -> `UNavMovementComponent::RequestDirectMovement()`
* `GetSafeNormal()` will return an `FVector` where the combined total of the
  `X`, `Y` and `Z` will be 1 so it gives direction without magnitude
* `FVector::DotProduct()` will calculate the **cosine** of the angle of 2
  vectors, so:
  * if the angle is 90 deg, the ratio will be 0
  * if the angle is 0 deg, the ratio will be 1
  * Links:
    * [Wikipedia: Dot Product Geometric Meaning](https://en.wikipedia.org/wiki/Dot_product#Geometric_definition)
![Wikipedia Dot Product Demo](https://upload.wikimedia.org/wikipedia/commons/thumb/7/76/Inner-product-angle.svg/330px-Inner-product-angle.svg.png)
    * [UE4 FVector::DotProduct](https://docs.unrealengine.com/en-US/API/Runtime/Core/Math/FVector/DotProduct/index.html)
* `FVector::CrossProduct()` will calculate the **sine** of the angle of 2
  vectors, returning a vector where the z axis is the output, so:
  * if the angle is 90 deg, the z axis of the cross product will be 1
  * if the angle is 0 deg, the z axis of the cross product will be 0
  * Links:
    * [Wikipedia Cross Product: Geometric Meaning](https://en.wikipedia.org/wiki/Cross_product#Geometric_meaning)
![Wikipedia Cross Product Demo](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6e/Cross_product.gif/330px-Cross_product.gif)
    * [UE4 FVector::CrossProduct()](https://docs.unrealengine.com/en-US/API/Runtime/Core/Math/FVector/CrossProduct/index.html)

## Architecture Refactor

![Old busted architecture vs new hotness](images/unrealcourse-section-7-architecturerefactor.png)

Commits:

* https://github.com/overbyte/unrealcourse-section-7-tank-battle/commit/fdcef6556574b3bc7df728cafb4deba6e48c513c
* https://github.com/overbyte/unrealcourse-section-7-tank-battle/commit/b8bb1120e0cfad4988af05764e159a4f7ccc268c
* https://github.com/overbyte/unrealcourse-section-7-tank-battle/commit/ebb4adc4cb7349d403ca420e6d513d7302d27538

## Adding projectile

The projectile is a spawnable actor blueprint that includes:
* particle system on spawn
* particle system that activates on impact
* explosive (radial) force impulse that fires on impact

```
AProjectile::AProjectile()
{
 	// Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = false;

    // default add move component
    ProjectileMovement = CreateDefaultSubobject<UProjectileMovementComponent>(FName("Projectile Movement"));
    ProjectileMovement->bAutoActivate = false;

    CollisionMesh = CreateDefaultSubobject<UStaticMeshComponent>(FName("Collision Mesh"));
    SetRootComponent(CollisionMesh);
    CollisionMesh->SetNotifyRigidBodyCollision(true);
    CollisionMesh->SetVisibility(true);

    LaunchBlast = CreateDefaultSubobject<UParticleSystemComponent>(FName("Launch Blast"));
    LaunchBlast->AttachToComponent(RootComponent, FAttachmentTransformRules::KeepRelativeTransform);

    ImpactBlast = CreateDefaultSubobject<UParticleSystemComponent>(FName("Impact Blast"));
    ImpactBlast->bAutoActivate = false;
    ImpactBlast->AttachToComponent(RootComponent, FAttachmentTransformRules::KeepRelativeTransform);

    ExplosionForce = CreateDefaultSubobject<URadialForceComponent>(FName("Explosion Force"));
    ExplosionForce->AttachToComponent(RootComponent, FAttachmentTransformRules::KeepRelativeTransform);

}

void AProjectile::Launch(float AtSpeed)
{
    ProjectileMovement->SetVelocityInLocalSpace(FVector::ForwardVector * AtSpeed);
    ProjectileMovement->Activate();
}
```

### Adding event delegates

in `BeginPlay()`, the OnComponentHit event is delegated back to the projectile
class which exposes the `OnHit` method based on the signature talked about in
[this thread](https://answers.unrealengine.com/questions/429353/cpp-on-component-hit-doesnt-fire.html)

implementation:
```
void AProjectile::OnHit(UPrimitiveComponent* HitComponent, AActor* OtherActor, UPrimitiveComponent *OtherComponent, FVector NormalImpulse, const FHitResult& Hit)
{
    LaunchBlast->Deactivate();
    ImpactBlast->Activate();
    ExplosionForce->FireImpulse();

    // remove visible shell from world while leaving particles
    SetRootComponent(ImpactBlast);
    CollisionMesh->DestroyComponent();

    // set a timer to destroy projectile completely
    FTimerHandle OutTimerHandle;
    GetWorld()->GetTimerManager().SetTimer(OutTimerHandle, this, &AProjectile::RetireProjectile, TimeToDestroy, false);
}

void AProjectile::RetireProjectile()
{
    Destroy();
}
```

Notes:
* This uses a slight janky way of destroying the projectiles by:
  * setting a new root component
  * destroying the visible collision mesh
  * setting a timer to clean up the projectile object

### ways to implement projectile destruction

| Scheme                   	| Pros                                                                               	| Cons                                                                                            	|
|--------------------------	|------------------------------------------------------------------------------------	|-------------------------------------------------------------------------------------------------	|
| projectile destroy timer 	|  Simplicity. Projectile responsible for itself                                       	|  Not performant with a lot of projectiles (each one includes a timer)                         	|
| spawn explosion effect   	|  More phyiscal. projectile gone but   explosion remains                            	|  More complicated. Can cause slowdown from spawning / destroying objects at the point of impact 	|
| projectile pool          	|  Probably the most performant   when there's a natural limit   to # of projectiles 	|  Most complicated. Object pooling / ring buffer would require a manager class and good reset    	|

Commits

* https://github.com/overbyte/unrealcourse-section-7-tank-battle/commit/09f62b14b4d71df527e13603a361ea3d084f1304
* https://github.com/overbyte/unrealcourse-section-7-tank-battle/commit/b0463b314569776056323b5fe71353dd2933af66
* https://github.com/overbyte/unrealcourse-section-7-tank-battle/commit/a70678bca78cb4e18343eac7383afc9ccb5a1942

## Depossessing a Pawn

### From the AI

On the AAIController subclass (TankAIController), when the tank is destroyed, it
is dispossessed with 

```
void ATankAIController::OnTankDestruction()
{
    // get for pawn pointer
    if (!GetPawn()) { return; }

    // dispossess tank
    GetPawn()->DetachFromControllerPendingDestroy();
}
```

* https://github.com/overbyte/unrealcourse-section-7-tank-battle/commit/290fdb8c59dea98ae8324ad149d867a4aca03190

### From the player

On the APlayerController subclass (TankPlayerController), when the player is
destroyed, currently the tank is dispossess with `StartSpectatingOnly()`.

* https://github.com/overbyte/unrealcourse-section-7-tank-battle/commit/c3d739f3aa4407e309069764eb0c05fd81b3d4d9

## Creating the spring

The secret sauce for springs are the physics constraint components

* Create new Actor Blueprint
* Add 2 static meshes and set them to cubes (use view options: show engine
  content if they're not availble)
  * set them both to simulate physics
  * the top cube
    * is set as the actor root component
    * is called `Mass` (need to give these names to phyiscs
    * has a mass of 40,000 kg (40 tonnes)
    constraint)
  * the bottom cube
    * is called `Wheel`
    * has a mass of 1000kg
* add a physics constraint
  * add the two names under `Constraint:Component Name 1` and `2`
  * set all of the `angular limits` to `locked` to stop the cubes turning /
    twisting
  * set the x and y `linear limits` to locked
  * set the z `linear limits` to free to allow the cubes to move freely on the z
    axis
  * in the Linear Motor: Position Strength
    * turn on the z-axis
    * set the position target strength to 1000 to set the spring strength to push
      back against the mass of the top cube
    * set the velocity target strength to 500 to give the spring some damping to
      stop it oscillating for too long

Links:
* https://docs.unrealengine.com/en-US/Engine/Components/Physics/index.html

### Switching to CPP

* Set up a SpawnPoint class to reliably spawn in actors
```
// Called when the game starts
void USpawnPoint::BeginPlay()
{
	Super::BeginPlay();

    // start spawning actor but defer it
    auto ActorToSpawn = GetWorld()->SpawnActorDeferred<AActor>(SpawnClass, GetComponentTransform());
    if (!ActorToSpawn) { return; }
    // attach to world (not local)
    ActorToSpawn->AttachToComponent(this, FAttachmentTransformRules::KeepWorldTransform);
    // finish spawning actor
    UGameplayStatics::FinishSpawningActor(ActorToSpawn, GetComponentTransform());
}
```
Source: https://github.com/overbyte/unrealcourse-section-7-tank-battle/blob/master/BattleTank/Source/BattleTank/Private/SpawnPoint.cpp

* Set up SprungWheel class to recreate blueprint described above
https://github.com/overbyte/unrealcourse-section-7-tank-battle/blob/master/BattleTank/Source/BattleTank/Private/SprungWheel.cpp

## Important when using physics

The physics for the engine is usually constrained by the framerate meaning that
if the framerate drops, the physics will behave differently to normal making it
unpredictable. To Combat this, in the `Project Settings: Physics` set the
`substepping` checkbox to true. This allows the physics to be calculated
multiple times a frame.
