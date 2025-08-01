# StatsManager

The role of our stats manager and how we approach stats. (I will also have another file that is the ‘stats dictionary’ which lays out the order, etc.)

## ROLES

### → LOAD STATS from CSV or other source

- I think it might make sense to manage the stats in a table especially given the number of fields. It will be easier to drag them around, reorder etc.

### → STORE STATS

- Hierarchy including primary and secondary e.g.
  - player.stats.p will store Primary Stats. These are the core stats that help a player grow (e.g. maxHP, moveSpeed, meleeDmg)
  - player.stats.s will store Secondary Stats. These are supportive stats such as an increase in pickup radius.
  - It will be broken down further for primary and secondary:
    - baseStats: the amount that the player starts with
    - levelUpStats: stat increases from Level Up selections
    - gearStats: stat increases from items/equipment
    - totalStats: calculated sum of stats from base amount, from level up, and from gear
  - player.stats.game (other core stats) will store Level, current XP, XP to next level, and Soma
      - hp (current hp)
      - xp (current amount)
      - xp for next level (cumulative amount necessary to reach next level)
      - soma (currency; dropped when enemies die)

### → SET DEFAULT STATS at the start of the game

### → XP

- Eventually, I will have a table of experience points necessary to progress.



### → LEVEL UP

- Called in Game.ts by checkSomaPickup which calls statsManager.gainXP

### → UPDATE STATS

- (called by Game.ts)
- When to update stats:
  - On Wave End
  - On Wave Start
  - On Pause
  - On Level Up selections
  - On Equipment changes
  - On Shop End

### → DISPLAY STATS

- Stats are displayed in a StatsPanel. There will be three StatPanels displayed in the UI. One of them is the “master” stats panel that has its data updated, and the other two are cloned from it on every update
  - StatsPanel 1 (master): in ShopScreen
  - StatsPanel 2: PauseScreen
  - StatsPanel 3: LevelUpScreen
- Every time stats are updated:
  - Master StatsPanel DOM is updated (the one in ShopScreen)
  - PauseScreen and LevelUpScreen’s respective StatPanels will be replaced by the content of the Master StatsPanel