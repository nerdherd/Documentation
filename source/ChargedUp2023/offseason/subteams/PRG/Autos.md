### Cube Shooter Autos

During the offseason, we created 4 different autos for the cube shooter robot. To create these autos, we made an auto path using pathplanner and then created commands within RobotContainer.java to integrate the path planner autos into our program. Our four autos were 3PieceShort, 3PieceLong, DirectBalance, and Balance. They will each be explained in detail below. We also made a ShuffleBoard tab with a dropdown menu with which we can change the auto currently being used. Finally, to get rid of the lag that occurred at the beginning of each auto, we used hashmap to initialize the paths so that they built before the auto was run.


#### 1. 3PieceShort Auto

The 3PieceShort auto involves scoring a preloaded cube onto the high node on the non-cable side, followed by two cubes onto the low nodes. This auto also includes mobility (taxi) as the two low cubes were picked up from the field.

![3PieceShort Auto](https://github.com/nerdherd/Documentation/blob/main/source/images/Offseason/Prog/3PieceShortPathPlannerAuto.PNG)​

#### 2. 3PieceLong Auto

The 3PieceLong auto is essentially the same auto as 3PieceShort, but it occurs on the cable side of the field. The 3PieceLong auto involves scoring a preloaded cube onto the high node on the cable side, followed by two cubes onto the low nodes. This auto also includes mobility (taxi) as the two low cubes were picked up from the field.

![3PieceLong Auto](https://github.com/nerdherd/Documentation/blob/main/source/images/Offseason/Prog/3PieceLongPathPlannerAuto.PNG)​

#### 3. DirectBalance Auto

The DirectBalance auto involves scoring a preloaded cube onto the high node in the middle of the grid. The robot then engages on the charge station.

![DirectBalance Auto](https://github.com/nerdherd/Documentation/blob/main/source/images/Offseason/Prog/DirectBalancePathPlannerAuto.PNG)​

#### 4. Balance Auto

The Balance auto is similar to the DirectBalance auto, except that it taxis before engaging on the charge station. The Balance auto involves scoring a preloaded cube onto the high node in the middle of the grid. The robot then taxis and engages on the charge station.

![Balance Auto](https://github.com/nerdherd/Documentation/blob/main/source/images/Offseason/Prog/BalancePathPlannerAuto.PNG)​

#### Code Segments

The code block shown below turns each auto path into a command that can be accessed and chosen within Shuffleboard. 

```java
private void initAutoChoosers() {
    final String[] paths = {
       "3Piece Short","3Piece Long","Balance","DirectBalance"
    };
    
    PathPlannerAutos.init(swerveDrive);

    for (String path : paths) {
      PathPlannerAutos.initPath(path);
      PathPlannerAutos.initPathGroup(path);
    }

    autoChooser.addOption("Do Nothing", Commands::none);
    autoChooser.addOption("Path Planner Balance", () -> new Balance(PathPlannerAutos.autoBuilder, swerveDrive, shooter, wrist));
    autoChooser.addOption("Path Planner 3PieceShort", () -> new Auto3PieceShort(PathPlannerAutos.autoBuilder,swerveDrive, shooter, wrist));
    autoChooser.addOption("Path Planner 3PieceLong", () -> new Auto3PieceLong(PathPlannerAutos.autoBuilder, swerveDrive, shooter, wrist));
    autoChooser.addOption("Path Planner DirectBalance", () -> new DirectBalance(PathPlannerAutos.autoBuilder, swerveDrive, shooter, wrist));

    ShuffleboardTab autosTab = Shuffleboard.getTab("Autos");

    autosTab.add("Selected Auto", autoChooser);
  }

```

The code block shown below includes the hashmap initialization that allows us to build autos before they are run to prevent lag.

```java

public class PathPlannerAutos {
    private static HashMap<String, PathPlannerTrajectory> cachedPaths = new HashMap<>();

    /**
     * Load the selected path from storage.
     * @param pathName
     */
    public static void initPath(String pathName) {
        if (cachedPaths.containsKey(pathName)) {
            DriverStation.reportWarning(String.format("Path '%s' has been loaded more than once.", pathName), true);
        }

        PathPlannerTrajectory path = PathPlanner.loadPath(pathName, kPPPathConstraints);

        if (path == null) {
            DriverStation.reportWarning(String.format("Path '%s' could not be loaded!", pathName), true);
        }
        cachedPaths.put(pathName, path);
    }
    
    public static PathPlannerTrajectory getPath(String pathNameString) {
        if (!cachedPaths.containsKey(pathNameString)) {
            DriverStation.reportWarning(String.format("Path '%s' was not pre-loaded into memory, which may cause lag during the Autonomous Period.", pathNameString), true);
            initPath(pathNameString);
        }
        return cachedPaths.get(pathNameString);
        
    }
}
```
