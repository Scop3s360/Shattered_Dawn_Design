# ShatteredDawn - Battle Process Step-by-Step

## Combat Flow Overview

ShatteredDawn uses a turn-based combat system with initiative order, multiple action types, and strategic depth through spells, positioning, and status effects.

## Pre-Combat Phase

### 1. Combat Initiation
- Player encounters enemy in exploration mode
- Combat screen transitions with battlefield setup
- Enemy and player sprites positioned on battlefield
- Combat UI elements become active

### 2. Initiative Calculation
**Formula:** `Speed + Random(0-20)`
- Each participant rolls initiative
- Turn order determined from highest to lowest
- Ties broken by base Speed stat
- Turn order displayed in combat UI

### 3. Combat Setup
- Player and enemy health/mana bars displayed
- Available actions populated based on character class
- Spell list generated based on character level and mana
- Status effects initialized (if any carry over)

## Combat Round Structure

### Turn Phase 1: Action Selection
**Available Actions:**
1. **Attack** - Basic physical attack
2. **Spell** - Cast magic spell (if mana available)
3. **Redemption** - Redemptive attack (special ability)
4. **Defend** - Reduce incoming damage, build defensive stance
5. **Retreat** - Attempt to flee combat (success chance based)

### Turn Phase 2: Action Resolution

#### Physical Attack Resolution
1. **Hit Chance Calculation**
   - Formula: `Accuracy / (Accuracy + Defender Speed)`
   - Range clamped to 5-95%
   - Roll d100 against hit chance

2. **Damage Calculation** (if hit)
   - Formula: `((Strength - Defense) - 5) × 2.5`
   - Minimum damage: 1 point
   - Critical hit check: 5% base chance for 1.5× damage

3. **Damage Application**
   - Subtract damage from target's current health
   - Update health bar and display damage number
   - Check for death condition

#### Spell Casting Resolution
1. **Mana Check**
   - Verify sufficient mana for spell cost
   - Deduct mana cost from caster's pool

2. **Spell Hit Calculation**
   - Base hit chance + 10% spell bonus
   - Formula: `(Accuracy + 10) / (Accuracy + 10 + Defender Speed)`
   - Range: 15-95% (higher than physical attacks)

3. **Spell Effect Application**
   - **Damage Spells**: Calculate damage using spell's base damage + scaling
   - **Healing Spells**: Restore health, cannot exceed maximum
   - **Buff Spells**: Apply positive status effects with duration
   - **Debuff Spells**: Apply negative status effects to target
   - **Utility Spells**: Special effects (reveal stats, dispel, etc.)

4. **Status Effect Processing**
   - Add new status effects to target's effect list
   - Set duration counters
   - Apply immediate effects if applicable

#### Redemptive Attack Resolution
1. **Special Ability Check**
   - Verify redemptive attack is available (not on cooldown)
   - Check any special requirements (target type, conditions)

2. **Effect Application**
   - Unique effects per redemptive attack type
   - May include damage, healing, status effects, or special mechanics
   - Often have thematic narrative descriptions

3. **Cooldown Application**
   - Set cooldown timer for redemptive attack
   - Update UI to show unavailable state

#### Defend Action Resolution
1. **Defensive Stance**
   - Reduce incoming damage by 50% until next turn
   - May provide status effect resistance
   - Builds defensive momentum for some classes

2. **Counter-Attack Preparation**
   - Some defensive stances enable counter-attacks
   - Prepare retaliation for next incoming attack

#### Retreat Attempt Resolution
1. **Success Calculation**
   - Base success chance varies by character class and enemy type
   - Speed differential affects success rate
   - Some enemies may prevent retreat

2. **Opportunity Attack**
   - Failed retreat may trigger enemy opportunity attack
   - Successful retreat ends combat immediately
   - No experience or rewards gained from retreat

### Turn Phase 3: Status Effect Processing
1. **Damage Over Time Effects**
   - Apply poison, burning, or other DoT effects
   - Reduce effect duration by 1 turn

2. **Healing Over Time Effects**
   - Apply regeneration or other HoT effects
   - Reduce effect duration by 1 turn

3. **Stat Modification Effects**
   - Maintain buff/debuff effects on stats
   - Reduce effect duration by 1 turn

4. **Effect Expiration**
   - Remove effects with duration = 0
   - Display expiration messages
   - Restore modified stats to base values

### Turn Phase 4: Turn Transition
1. **Death Check**
   - Check if any participant has health ≤ 0
   - If player dies: Game Over or revival mechanics
   - If enemy dies: Proceed to victory resolution

2. **Turn Order Advancement**
   - Move to next participant in initiative order
   - Cycle back to first participant after last turn
   - Update UI to show active participant

3. **Round Counter**
   - Increment round counter for tracking
   - Some effects may trigger on specific rounds

## Post-Combat Resolution

### Victory Conditions
**Player Victory:**
- All enemies reduced to 0 health
- Enemy retreats successfully
- Special victory conditions met (redemption, etc.)

**Defeat Conditions:**
- Player character reduced to 0 health
- Forced retreat with consequences
- Special defeat conditions (time limits, etc.)

### Victory Rewards Processing
1. **Experience Calculation**
   - Base XP from enemy type and level
   - Bonus XP for combat performance
   - Bonus XP for using redemptive attacks

2. **Hope Points Generation**
   - Combat victories generate hope points
   - Bonus points for compassionate choices
   - Companion presence may modify generation

3. **Loot Distribution**
   - Equipment drops based on enemy type
   - Consumable items (healing potions, etc.)
   - Special items from boss encounters

4. **Level Up Check**
   - Compare total XP to level requirements
   - Trigger level up sequence if threshold met
   - Unlock new spells and abilities

### Post-Combat Narrative
1. **Victory Message Display**
   - Thematic victory text based on combat type
   - Redemption success/failure messages
   - Hope point gain notifications

2. **Settlement Impact**
   - Combat outcomes may affect settlement reputation
   - Companion reactions to combat choices
   - Long-term consequence tracking

3. **Return to Exploration**
   - Transition back to exploration mode
   - Update world state based on combat results
   - Continue story progression

## Special Combat Mechanics

### Environmental Effects
- Terrain modifiers affect movement and accuracy
- Weather conditions impact spell effectiveness
- Positioning affects damage and spell targeting

### Multi-Phase Boss Battles
- Horsemen bosses have 3-4 phases
- Phase transitions trigger special abilities
- Different strategies required per phase

### Combination Attacks (with Companions)
- Require high companion loyalty
- Consume mana from multiple participants
- Devastating effects with unique animations
- Long cooldown periods

### Charge Attacks
- Multi-turn attacks with increasing damage
- Can be interrupted by enemy actions
- Risk/reward mechanic for high damage output

### Status Effect Interactions
- Some effects stack (multiple poisons)
- Some effects cancel each other (fire vs ice)
- Immunity effects prevent specific status types
- Dispel effects remove multiple status effects at once