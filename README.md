# AgeVR_IVE_core

## Start Template

### 1. VR App

#### 1.1 Play in Editor

Open the initiate study scene and start the PIE Mode from there.

#### 1.2 Build Project

Before building the export directory (_ExportDir_) path has to be set in the BP_StudyResults_Explorative Blueprint

Start the build. The initiate study scene (black) should load. You then can proceed to controll the StudySystem via the experimenter interface.

### 2. experimenter interface
The repository for the interace can be found here ([VR-StudySystem-Template-WebApp](https://github.com/RBW1999/VR-StudySystem-Template-WebApp))

#### 2.0 first time SetUp

You need Node.js on the system. The StudySystem template was build with Node v20.11.0

```
npm install
```

#### 2.1 Choose correct playMode

Dependig of using Play in Editor or a build for the VR App the playMode in _index.js_ has to be adjusted.

#### Start experimenter interface / host website

When the VR App is already running (1.) and the correct playMode is selected (2.1) you can start the exprimenter interface.

```
npm run dev
```

If you want to host the exprimenter interface to the local network use:

```
npm run dev -- --host
```

## Create new Szneario

In this section the creation of a new scenario in the unreal engine and the connection setup in the experimenter interface is explained.

### VR App

Create a new folder with the name of the Level in _Content/Maps/Szenarien/_ and the create a level with the same name in this folder. This folder structure is important for the
At the end it should look like this:

```
Content
├── Maps
|   ├── Szenarien
|   |   ├── InitiateStudy
|   |   |   └── InitiateStudy (Level)
|   |   ├── TestEnviroment
|   |   |   └── TestEnviroment (Level)
|   |   ├── ...
|   |   └── NewScenario
|   |       └── NewScenario (Level)
...
```

#### Build Scenraio from Level

Each scenario needs 8 actors. Some of these need further configuration setUps in the details panel (see below).

[] **BP_ConnectionManger**
[] set Default/ADManager reference
[] set Default/TManager reference

[] **BP_ADManger**
[] set Illumination/Ref/ Sky Light reference
[] set Illumination/Ref/ Directional Light reference
[] set Illumination/Ref/ GoodSky reference

[] **BP_TaskManager**
[] create BP_TaskObject Childs and set the refernce to the IC or OT Task Object array

[] **BP_GoodSky**
[] set Sky Beta/Directional Light Actor refrence

[] **Directional Light**

[] **SkyLight**

[] **PlayerStart**

[] **NavMeshBoundsVolume** (for teleport)

### Experimenter Interface

1. Add scenario to scr/stores/studyStore
   [] add the scenario as new property of the Scenario Object (line 13)
   [] add the scenario to the allScenarioOrders (line 28)
2. Add the scenario to the src/pages/scenario.vue to make it accessible for the debug mode _(optional)_
   [] copy existing image button
   [] set the scenario as newScenario parameter in @click="store.changeScenario(...)"
   [] set :selected property to the chosen scenario

## Trouble Shooting

### No connection bad request response in experimenter interface

1. When the VR app is running in the editor check if the WebServer for the remote control is running / restart the server.

   ```
   WebControl.StopServer
   WebControl.StartServer
   ```

2. Check if ur using the correct playMode for the experimenter interface in the index.js. The build modes differ.

### Post Process Volume: Auto Exposure

For the Adaption Dimenison Illumination intensity the follwing Auto Exposure settings have to be set to 0.

- Exposure Compensation: 0
- Min EV100: 0
- Max EV100: 0

### Teleport not working in scenraio / config

By default the teleport is only active during a task or in the debug study mode.
This can be set via the _setCanTeleport(bool)_ function in the studyStore.

# Assets

All Assets in this template are from [PolyHaven](https://polyhaven.com/)

Here are the direct links

https://polyhaven.com/a/watering_can_metal_01
https://polyhaven.com/a/wooden_crate_02
https://polyhaven.com/a/wooden_bucket_01
https://polyhaven.com/a/wooden_bucket_02
