# 3D Motorcycle Stunt Game - Unity Physics-Based

## IMPORTANT: NO JUMP BUTTON!

This game uses **realistic physics** for motorcycle stunts. The motorcycle becomes airborne naturally through **SPEED + RAMPS + PHYSICS**.

---

## Core Gameplay Loop

```
ACCELERATE → BUILD SPEED → HIT KICKER RAMP → NATURAL TAKEOFF → 
AIRBORNE → CONTROL ROTATION → ALIGN FOR LANDING → LAND → CONTINUE
```

---

## Controls

| Action | Keys |
|--------|------|
| **Accelerate** | W / Up Arrow |
| **Brake / Reverse** | S / Down Arrow |
| **Steer Left** | A / Left Arrow |
| **Steer Right** | D / Right Arrow |
| **Brake** | Space |
| **Respawn** | R |
| **Pause** | ESC |

### Air Controls (When Airborne)
- **W/S or Up/Down**: Pitch control (frontflip/backflip)
- **A/D or Left/Right**: Roll control

---

## Project Structure

```
Assets/
├── Scripts/
│   ├── Bike/
│   │   ├── BikeController.cs          # Main motorcycle physics and controls
│   │   ├── BikeGroundDetector.cs      # Ground/air state detection
│   │   ├── BikeAirControl.cs          # Physics-based air rotation control
│   │   └── LandingDetector.cs         # Landing quality evaluation
│   ├── Game/
│   │   ├── GameManager.cs             # Global game management
│   │   ├── RespawnSystem.cs           # Checkpoint respawn system
│   │   ├── RaceTimer.cs               # Level timer
│   │   └── CrashDetector.cs           # Crash detection and handling
│   ├── Level/
│   │   ├── LevelManager.cs            # Level flow control
│   │   ├── LevelData.cs               # ScriptableObject for level info
│   │   ├── Checkpoint.cs              # Individual checkpoint behavior
│   │   └── CheckpointManager.cs       # Checkpoint progression tracking
│   ├── Stunt/
│   │   └── StuntManager.cs            # Stunt detection and scoring
│   ├── UI/
│   │   ├── HUDController.cs           # In-game HUD
│   │   ├── MainMenuUI.cs              # Main menu interface
│   │   ├── LevelSelectUI.cs           # Level selection screen
│   │   ├── PauseMenu.cs               # Pause menu
│   │   └── LevelCompleteUI.cs         # Level completion screen
│   ├── Save/
│   │   └── SaveManager.cs             # Save/load system
│   └── Audio/
│       └── AudioManager.cs            # Audio management
├── Prefabs/
│   ├── Ramps/                         # Wooden kicker ramp prefabs
│   ├── Obstacles/                     # Broken road gaps, obstacles
│   └── Checkpoints/                   # Checkpoint prefabs
└── Scenes/
    ├── MainMenu                       # Main menu
    ├── LevelSelect                    # Level selection
    ├── PhysicsTest                    # Physics tuning scene
    ├── Level1                         # Training level
    ├── Level2                         # Broken Highway
    ├── Level3                         # Mountain Stunt
    ├── Level4                         # Extreme Obstacle
    └── Level5                         # Final Stunt
```

---

## Development Order

### Phase 1: Core Physics (CRITICAL)
1. ✅ Create folder structure
2. ✅ Create all core scripts
3. ⏳ Configure motorcycle Rigidbody and WheelColliders
4. ⏳ Test throttle, brake, steering on flat ground
5. ⏳ Create wooden kicker ramp prefabs
6. ⏳ Test natural physics-based takeoff
7. ⏳ Tune speed required to clear gaps

### Phase 2: Airborne System
8. ⏳ Implement airborne detection
9. ⏳ Implement limited air rotation using physics
10. ⏳ Test stunt rotations (flips, spins)
11. ⏳ Implement landing detection and quality

### Phase 3: Game Systems
12. ⏳ Implement crash detection
13. ⏳ Implement respawn system
14. ⏳ Implement checkpoint system
15. ⏳ Implement timer and scoring

### Phase 4: UI & Menus
16. ⏳ Create HUD
17. ⏳ Create Main Menu
18. ⏳ Create Level Selection
19. ⏳ Create Pause Menu
20. ⏳ Create Level Complete screen

### Phase 5: Levels
21. ⏳ Create PhysicsTest scene
22. ⏳ Create Level 1 - Training
23. ⏳ Create Level 2 - Broken Highway
24. ⏳ Create Level 3 - Mountain Stunt
25. ⏳ Create Level 4 - Extreme Obstacle
26. ⏳ Create Level 5 - Final Stunt

### Phase 6: Polish
27. ⏳ Add audio system
28. ⏳ Add particle effects
29. ⏳ Optimize performance
30. ⏳ Build and test

---

## Motorcycle Physics Configuration

### Rigidbody Settings
- **Mass**: 150-220 kg (configurable)
- **Drag**: 0.5
- **Angular Drag**: 2
- **Use Gravity**: YES
- **Interpolate**: Interpolate
- **Collision Detection**: Continuous Dynamic

### WheelCollider Settings
**Front Wheel:**
- **Mass**: 20 kg
- **Radius**: 0.35-0.4m
- **Wheel Damping Rate**: 0.5
- **Suspension Distance**: 0.3m
- **Suspension Spring**: 35000
- **Damper**: 4500
- **Target Position**: 0.5

**Rear Wheel:**
- **Mass**: 25 kg
- **Radius**: 0.4-0.45m
- **Same suspension settings**

### Configurable Physics Values
All important physics values are exposed via `[SerializeField]`:
- Motor torque
- Brake torque
- Maximum speed
- Steering angle
- Air control strength
- Landing thresholds
- Crash detection values

---

## Stunt Scoring System

| Stunt | Score |
|-------|-------|
| Backflip | 100 |
| Frontflip | 100 |
| 360° Spin | 150 |
| 540° Spin | 200 |
| 720° Spin | 300 |
| Perfect Landing | +50 |
| Normal Landing | +20 |

---

## Kicker Ramp Types

1. **SmallKicker** - Low height, gentle angle
2. **MediumKicker** - Medium height, moderate angle
3. **LargeKicker** - High height, steep angle
4. **ExtremeKicker** - Maximum height, extreme angle

Each ramp type requires different approach speeds:
- **Small**: Moderate speed
- **Medium**: High speed
- **Large**: Very high speed
- **Extreme**: Maximum speed

---

## Landing System

### Landing Quality Levels:
1. **Perfect Landing** - Both wheels, correct orientation, low impact
2. **Normal Landing** - Acceptable orientation, moderate impact
3. **Hard Landing** - Poor orientation or high impact
4. **Crash** - Upside down, extreme impact, or missed landing

---

## Testing Checklist

### Physics Test Scene:
- [ ] Motorcycle accelerates smoothly
- [ ] Braking works correctly
- [ ] Steering responds naturally
- [ ] Balance maintained when grounded
- [ ] Small ramp launches bike naturally
- [ ] Medium ramp requires more speed
- [ ] Large ramp requires high speed
- [ ] Air control allows rotation
- [ ] Perfect landing detected correctly
- [ ] Crash detection works on bad landings
- [ ] Respawn system works
- [ ] No artificial jump behavior

---

## Assets Used

The game uses assets from `Extreme-Bike-Stunt-main` folder including:
- Motorcycle models and materials
- Ramp meshes
- Environment objects (containers, buildings, rocks)
- UI sprites and icons
- Textures and materials

---

## Unity Version

**Recommended**: Unity 2021.3 LTS or newer with URP (Universal Render Pipeline)

---

## Next Steps

1. Open Unity and create scenes
2. Configure motorcycle GameObject with Rigidbody + WheelColliders
3. Attach BikeController, BikeGroundDetector, BikeAirControl scripts
4. Create PhysicsTest scene with flat ground and test ramps
5. Tune physics values until motorcycle feels realistic
6. Build levels progressively

---

## CRITICAL RULES

✅ **DO:**
- Use Rigidbody physics for all movement
- Let ramps naturally launch the bike
- Make speed matter for clearing gaps
- Use AddTorque() for air rotation
- Detect landing quality through physics

❌ **DON'T:**
- Add a Jump button
- Use AddForce(Vector3.up) on button press
- Directly set transform.position for jumps
- Use Lerp for flight
- Automatically rotate bike during landing
- Fake any physics behavior

---

## Support

For questions or issues, check:
1. Physics values are properly configured
2. WheelColliders have correct settings
3. Ground layer is assigned
4. Ramps have colliders
5. Player tag is set on motorcycle
#   3 D - B i k e - G a m e  
 