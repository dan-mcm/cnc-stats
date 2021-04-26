# C&C Tiberian Dawn - Tanks & Infantry
Formatted from the hardwork of [Nyerguds](http://nyerguds.arsaneus-design.com/cnc95upd/inirules/).

This is an active work in progress and may have incorrect details - working to make it as accurate as possible.

## Key Descriptions

**Faction**: Which factions can build the units, if neutral may be accessible to both factions but cannot be built in standard missions/multiplayer  
**Unit/structure**: Name of the unit/structure  
**Image**: Image of the unit/structure  
**Cost**: Cost to produce the unit/structure  
**HitPoints**: Number of HitPoints the unit/structure has  
**Speed**: Speed of Unit  
**Power**: Power Production/Cost of the building  
**Weapon**: Name of Primary/Secondary Weapon  
**Sight**: Vision radius of unit/structure  
**Armor**: Class of armor for vehicle/unit. infantry default to 0.

## Armor Types

The armor values in the below tables can be translated as follows:

0: Infantry (no armor)  
1: Wood Armor  
2: Light Armor  
3: Medium Armor  
4: Heavy Armor (is this right? what has this value?)  
5: Invincible  

## Weapon Warheads -v- Armor

Different weapon projectiles deal different percentiles of damage against certain armor types.

Let's start with taking a Humvee as our candidate. We can tell from the tables below (or checking the units.ini file) that Humvee uses a machinegun weapon. If we inspect the corresponding bullets.ini we can see that this type of damage is of warhead type SmallArms.

```
; normal machinegun
[Invisible]
Explosion=PIFF
Warhead=SmallArms
RotationSpeed=0
BulletSpeed=-1
Unknown5=0
Unknown6=0
AA=No
Unknown8=0
Inaccurate=No
NoRotation=Yes
Unknown11=0
SmokeTrail=No
Unknown13=0
Invisible=Yes
Unknown15=0
Arcing=No
High=No
Image=50cal
Unknown19=0
```

If we check the corresponding warheads.ini file under SmallArms we should see:

```
[SmallArms]
Spread=2
TargetWalls=0
TargetWood=0
TargetTiberium=0
InfantryDeath=0
verses=256,128,144,64,64,0
```

A key note here is that in the verses section each value corresponds to an armor type: 256 -> 0, 128 -> 1, 144 -> 2, 64 -> 3, 64 -> 4, 0 -> 5.

This means that in the case of a unit that deals type SmallArms warhead damage:
* a 256/256 [100%] of possible damage is dealt against infantry
* a 128/256 [50%] of possible damage is dealt against wood armor (1)
* a 144/256 [~56%] of possible damage is dealt against light armor (2)
* a 64/256 [25%] of possible damage is dealt against medium armor (3)
* a 64/256 [25%] of possible damage is dealt against heavy armor (4)
* a 0/256 [0%] of possible damage is dealt against invincible units (5)

As a practical example let's takes a Humvee -v- a Minigunner.

A Humvee has a weapon of type 'Machinegun' if we consult the corresponding weapon.ini we can see it has a maximum possible damage of 15hp:

```
; Humvee/buggy/APC gun
[Machinegun]
Projectile=Invisible
Damage=15
ROF=30
Range=4.00
Report=Mgun11
MuzzleFlash=MINIGUN-N
```

If we consult the SmallArms warhead details (as above), we can see that our humvee has a 256/256 [100%] chance of dealing damage against the minigunner (infantry). This would be calculated as a full 15 damage per hit.

As a second example let's take a Humvee -v- a Humvee.

In this case the enemy humvee has an armor type of 2 (light armor) meaning it will only take a 144/256 [~56% of possible max damage] which comes out to around 8.5 damage per hit.

## Unit Template & Descriptions

### Infantry

| Faction |👨 Unit | 🖼️ Image | 💰 Cost | ❤️ HitPoints | ⚡ Speed | 🔫 Weapon | 👀 Sight |
|-|-|-|-|-|-|-|-|
| 🦅 & 🦂 | Rifleman | image | $100 | 50 | 8 | Rifle | 1 |
| 🦅 & 🦂 | Engineer | image | $500 | 25 | 8 | - | 2 |
| 🦅 | Grenadier | image | $160 | 50 | 10 | Grenade | 1 |
| 🦂 | Rocketman | image | $300 | 25 | 6 | Rocket | 2 |
| 🦂 | Flamethrower | image | $200 | 70 | 10 | InfantryFlamer | 1 |
| 🦂 | Chem Trooper | image | $300 | 70 | 8 | ChemSpray | 1 |
| 🦅 & 🦂 | Commando | image | $1000 | 80 | 10 | Sniper | 5 |
| Neutral | Joe | image | $10 | 25 | 10 | Pistol | 0 |
| Neutral | Phil | image | $10 | 5 | 10 | Pistol | 0 |


### Tanks

| Faction |👨 Unit | 🖼️ Image | 💰 Cost | ❤️ HitPoints | 🛡️ Armor | ⚡ Speed | 🔫 Weapon | 👀 Sight |
|-|-|-|-|-|-|-|-|-|
| 🦅 | Humvee | image | $400 | 150 | 2 | 30 | Machinegun | 2 |
| 🦅 | Medium | image | $800 | 400 | 3 | 18 | MediumCannon | 3 |
| 🦅 | Mammoth | image | $1500 | 600 | 3 | 12 | HeavyCannon  MammothTusk | 4 |
| 🦂 | Buggy | image | $300 | 140 | 2 | 30 | Machinegun | 2 |
| 🦂 | Bike | image | $500 | 160 | 1 | 40 | Rocket | 2 |
| 🦂 | Arty | image | $450 | 75 | 2 | 12 | ArtilleryShell | 4 |
| 🦂 | Light | image | $600 | 300 | 3 | 18 | LightCannon | 3 |
| 🦂 | Flame |image | $800 | 300 | 3 | 18 | TankFlamer | 4 |
| 🦂 | Stealth | image | $900 | 110 | 2 | 30 | Rocket | 4 |
| 🦂 | SSM | image | $750 | 120 | 2 | 18 | HonestJohn | 4 |
| 🦅 & 🦂 | Harvester | image | $1400 | 600 | 2 | 12 | - | 2 |
| 🦅 & 🦂 | MLRS | image | $800 | 100 | 2 | 18 | MLRSMissile| 4 |
| 🦅 & 🦂 | APC | image | $700 | 200 | 3 | 35 | Machinegun | 4 |
| 🦅 & 🦂 | MCV | image | $5000 | 600 | 2 | 12 | - | 2 |
| Neutral | MobileHQ | image | $600 | 110 | 2 | 18 | - | - | 5 |
| Neutral | Hovercraft  | image | $300 | 400 | 2 | 30 | - | - | 3 |
| Neutral | Boat | image | $300 | 700 | 3 | 8 | BoatMissile | 5 |

### Aircraft

| Faction |👨 Unit | 🖼️ Image | 💰 Cost | ❤️ HitPoints |  🛡️ Armor | ⚡ Speed | 🔫 Weapon | 👀 Sight |
|-|-|-|-|-|-|-|-|-|
| 🦅 & 🦂 | Chinhook | image | $1500 | 90 | 2 | 30 | - | 0 |
| 🦂 | Apache | image | $1200 | 125 | 3 | 40 | Chaingun | 0 |
| 🦅 | Orca | image | $1200 | 125 | 3 | 40 | Rocket | 0 |
| Neutral | A10 Airstrike | image | $800 | 60 | 2 | 40 | Napalm | 0
| Neutral | C17 Cargo | image | $800 | 25 | 2 | 40 | - | 0 |

---

## Structures

### Buildings

| Faction |👨 Structure | 🖼️ Image | 💰 Cost | ❤️ HitPoints |  🛡️ Armor | 👀 Sight | ⚡ Power |
|-|-|-|-|-|-|-|-|
| 🦂 | Temple of Nod | image | $3000 | 1000 | 2 | 4 | -150 |
| 🦅 | Adv Comm Centre | image | $2800 | 500 | 1 | 10 | -200 |
| 🦅 | Weapons Factory | image | $2000 | 200 [+30%: 260] | 2 | 3 | -30 |
| 🦅 | Guard Tower | image | $500 | 200 | 1 | 3 | -10 |
| 🦅 | Adv Guard Tower | image | $1000 | 300 | 2 | 4 | -20 |
| 🦂 | Obelisk | image | $1500 | 200 | 2 | 5 | -150 |
| 🦂 | Gun Turret | image | $600 | 200 | 3 | 5 | -20 |
| 🦅 & 🦂 | Con Yard | image | $5000 | 400 | 1 | 3 | +15 |
| 🦅 & 🦂 | Refinery | image | $2000 | 450 | 1 | 4 | -40 & +10 |
| 🦅 & 🦂 | Silo | image | $150 | 150 | 1 | 2 | -10 |
| 🦅 & 🦂 | Helipad | image | $1500 | 400 | 1 | 3 | -10 |
| 🦅 & 🦂 | Comm Centre | image | $1000 | 500 | 1 | 10 | -40 |
| 🦂 | Sam Site | image | $750 | 200 | 3 | 3 | -20 |
| 🦂 | Airfield | image | $2000 | 500 | 3 | 5 | -30 |
| 🦅 & 🦂 | Power Plant | image | $300 | 200 | 1 | 2 | +100 |
| 🦅 & 🦂 | Adv Power Plant | image | $700 | 300 | 1 | 2 | +200 |
| 🦅 | Barracks | image | $300 | 400 | 1 | 3 | -20 |
| 🦂 | Hand of Nod | image | $300 | 400 | 1 | 3 | -20 |
| 🦅 & 🦂 | Repair Bay | image | $1200 | 400 | 1 | 3 | -30 |

 ### Walls
| 🧱 Wall | 🖼️ Image | 💰 Cost | ❤️ HitPoints |  🛡️ Armor |
|-|-|-|-|-|
| Sandbag | image | $50 | 1 | 2 |
| Chainlink | image | $75 | 1 | 2 |
| Concrete | image | $100 | 1 | 2 |
| Barbwire Fence | image | $25 | 1 | 2 |
| Wooden Fence | image | $25 | 1 | 2 |
