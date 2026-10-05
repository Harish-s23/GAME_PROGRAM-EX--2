# GAME_PROGRAM-EX--2

## EX 2 : Create a player movement using character, collectable, player health and score

## NAME :HARESH R

## REGISTER NUMBER : 212224040097

## Aim
Create a playable third-person character in Unreal Engine that can move and run, collect coin-like collectibles, track a Score and Player Health, and display both on-screen (UI).

## Overview:

Player Character (BP_PlayerCharacter) — handles movement, input, health, and overlaps with collectables.
Collectable (BP_Collectable) — simple actor with collision that gives score (and optionally health) when overlapped.
UI (WBP_HUD) — UMG Widget showing Score and Health values.
GameMode / PlayerState — (optional) hold persistent Score/HighScore across respawns.
Game flow — pickup increments Score, maybe plays sound/particle and destroys the collectable; health decreases on damage, and player dies or respawns when health ≤ 0.
Step-by-step Implementation (Blueprint-first)
1. Project & Input Setup
Create a Third Person Blueprint project (or use your existing ThirdPersonMap).

Open Project Settings → Input and ensure these mappings exist:

MoveForward (W / Up arrow)
MoveRight (A/D or Left/Right)
Turn / LookUp (mouse)
Jump (SpaceBar)
Run (Left Shift) — optional if you want sprint
2. Player Character Blueprint (BP_PlayerCharacter)
Duplicate the existing ThirdPersonCharacter (or create a new Character blueprint) and name it BP_PlayerCharacter.

Variables to add (Expose where useful):

Score (Integer) — default 0
MaxHealth (Float) — e.g. 100.0
Health (Float) — default equal to MaxHealth
bIsRunning (Boolean) — if you want sprinting
Movement (in Event Graph):

Use Add Movement Input hooked to MoveForward and MoveRight axis mappings.
Use Turn and LookUp to rotate camera.
If using Run: on Run Pressed set Max Walk Speed on the Character Movement component (e.g. 1200) and reset on Released (600 default).
Health functions:

Function: ApplyDamage(float DamageAmount)

Subtract DamageAmount from Health.
If Health <= 0 → call OnDeath event (disable input, play animation, respawn or show Game Over).
Update HUD (call event to update widget binding).
Function: AddHealth(float HealAmount)

Add to Health but clamp to MaxHealth.
Update HUD.
Score management:

Function: AddScore(int Amount)

Score = Score + Amount → update HUD.
BP_Collectable → OnComponentBeginOverlap (Sphere)
Other Actor → Cast To BP_PlayerCharacter

Branch (if cast success)

Call AddScore(ScoreValue) on Player Character
If GiveHealth > 0 Call AddHealth(GiveHealth)
Play Sound at Location
Spawn Emitter at Location
Destroy Actor
BP_PlayerCharacter → AddScore (Custom Event)
Input: Amount (int)
Score = Score + Amount
Call UpdateScoreDisplay on the HUD widget reference
(Optional) Play pickup sound, animate, or show floating text
BP_PlayerCharacter → ApplyDamage (Custom Event)
Input: Damage (float)

Health = Health - Damage

If Health <= 0

Call OnDeath (Disable Input; show Game Over)
Update HUD: Call UpdateHealthDisplay

## OUTPUT:
<img width="1041" height="583" alt="Screenshot 2026-10-05 202057" src="https://github.com/user-attachments/assets/b51d0733-269d-4654-9d3a-078c4a070ed2" />
<img width="802" height="307" alt="Screenshot 2026-10-05 202110" src="https://github.com/user-attachments/assets/23896133-a3aa-411e-84ee-6b2f3cba76ae" />
<img width="1042" height="405" alt="Screenshot 2026-10-05 202119" src="https://github.com/user-attachments/assets/74a8903b-50c6-4a97-b27c-7c3ffdd821a5" />
<img width="1041" height="582" alt="Screenshot 2026-10-05 202134" src="https://github.com/user-attachments/assets/fe60b5b3-4e24-4cb9-91d7-6a283501ee22" />



## RESULT :
The AI character successfully roams within the defined NavMesh area, choosing random destinations at intervals using the Behavior Tree logic.
