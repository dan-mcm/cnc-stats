#Armor Types

See [Nyerguds docs](http://nyerguds.arsaneus-design.com/cnc95upd/inirules/warheads.ini) for reference.

0: Infantry  
1: Wood Armor  
2: Light Armor  
3: Medium Armor  
4: Heavy Armor???  
5: Invincible  

## Example

```
[SmallArms]
Spread=2
TargetWalls=0
TargetWood=0
TargetTiberium=0
InfantryDeath=0
verses=256,128,144,64,64,0
```

So smallarms (minigunner, apc, buggy, humvee) does   
* 100% vs infantry,   [256] (armor type: 0)
* 50% vs wood armour, [128] (armor type: 1)
* 55%-ish (i forget exactly how much) vs light armour, [144] (armor type: 2)
* and then 25% vs heavy armour  [64] (armor type: 3)
* [64]? (armor type: 4 -> what has this? what is it?)
*[0] (armor type: 5 -> invincibility)
