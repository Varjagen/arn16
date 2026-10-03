# Unreachable reducer actions

61 of 251 reducer cases are never dispatched.

A `case` with no dispatcher is a feature with an engine and no door. Most
appear in app.js exactly once - as the case label - and are referenced only
from tests, which means **the suite certifies them as working**.

Unreachable is not the same as missing: some are superseded by a path that
does the same job.

## Two lessons this table has already cost

**Check for a sibling path before choosing a bucket.** GRAPPLE_ATTEMPT and
SHOVE_ATTEMPT were bucketed "unfinished - engine, no door". The Actions
drawer reached both through CONTEST_RESOLVE. Building the recommended door
would have made a third path to grappling.

**Before deleting a superseded case, diff it against the survivor CLAUSE BY
CLAUSE, not test by test.** The deleted grapple and shove paths had four
advantages over the live one. Retargeting their tests found two, because
only two had tests: the live path also applied conditions as a TOGGLE (so a
second application removed them) and ignored a refused economy spend (so a
creature that had used its action could grapple for free). Both shipped, and
both were found by a reader, not by the port. A green suite after a
retarget means the clauses that had tests survived. It says nothing about
the ones that did not.

Regenerate with `node tools/list-dead-actions.js`.

| action | in app.js | referenced by tests | bucket |
|---|---|---|---|
| `CHAT_CLEAR` | 1 | - | untriaged (no tests) |
| `CORRECTION_UNDO` | 1 | turn-corrections.test.js | untriaged (tests certify it) |
| `ECONOMY_ATTACK` | 1 | action-economy.test.js, weapon-effects.test.js | untriaged (tests certify it) |
| `ECONOMY_CAST_SPELL` | 1 | casting-time.test.js | untriaged (tests certify it) |
| `ECONOMY_RESET` | 1 | - | untriaged (no tests) |
| `ECONOMY_TAKE_ACTION` | 1 | action-economy.test.js, standard-actions.test.js | untriaged (tests certify it) |
| `ECONOMY_TAKE_ACTION_LEGACY` | 1 | - | untriaged (no tests) |
| `ECONOMY_TRIGGER_READY` | 1 | action-economy.test.js, action-service.test.js | untriaged (tests certify it) |
| `ECONOMY_USE_SLOT` | 1 | action-economy.test.js | untriaged (tests certify it) |
| `EFFECT_CLEAR_CASTER` | 1 | effect-scheduler.test.js | untriaged (tests certify it) |
| `EFFECT_CLEAR_FIRES` | 1 | - | untriaged (no tests) |
| `EFFECT_ESCAPE` | 1 | control-spells.test.js, effect-scheduler.test.js | untriaged (tests certify it) |
| `EFFECT_MOVE_AREA` | 1 | control-spells.test.js | untriaged (tests certify it) |
| `EFFECT_UNSCHEDULE` | 1 | - | untriaged (no tests) |
| `ENTITY_REPAIR` | 1 | hp-invariants.test.js | **unfinished** - no control exists yet |
| `ENTITY_RESURRECT` | 1 | hp-invariants.test.js | **unfinished** - no control exists yet |
| `ENTITY_TEMP_HP_GRANT` | 1 | temp-hp.test.js | **internal** - granted by spell effects |
| `ENTITY_TEMP_HP_SET` | 1 | temp-hp.test.js | **internal** - applied by rest and spell effects |
| `EXHAUSTION_SET` | 2 | exhaustion.test.js | **shared** - falls through with EXHAUSTION_ADJUST, which is dispatched - the block is live |
| `HP_MAX_BONUS_REMOVE` | 1 | healing-spells.test.js | untriaged (tests certify it) |
| `INTENT_CANCEL` | 1 | intent-lifecycle.test.js | untriaged (tests certify it) |
| `INTENT_CLEAR_SETTLED` | 1 | intent-lifecycle.test.js | untriaged (tests certify it) |
| `INTENT_FORGET` | 1 | - | untriaged (no tests) |
| `MAGE_ARMOR_END` | 1 | followups.test.js | untriaged (tests certify it) |
| `MAP_PATCH` | 1 | - | untriaged (no tests) |
| `MEDICINE_STABILIZE` | 1 | followups.test.js, stabilize-nonlethal.test.js | untriaged (tests certify it) |
| `MODIFIER_CLEAR_SOURCE` | 1 | roll-modifiers.test.js | untriaged (tests certify it) |
| `MODIFIER_CONSUME` | 1 | - | untriaged (no tests) |
| `MODIFIER_REMOVE` | 1 | - | untriaged (no tests) |
| `MONSTER_ABILITY` | 1 | monsters.test.js | untriaged (tests certify it) |
| `MOUNT_CLEAR` | 1 | movement-transaction.test.js, positioning.test.js | untriaged (tests certify it) |
| `MOUNT_SET` | 1 | movement-transaction.test.js, positioning.test.js | untriaged (tests certify it) |
| `OPPORTUNITY_PENDING` | 1 | live-combat.test.js | untriaged (tests certify it) |
| `REMINDER_MOVE` | 1 | - | untriaged (no tests) |
| `SPELL_AID` | 1 | healing-spells.test.js | untriaged (tests certify it) |
| `SPELL_APPLY_MODIFIERS` | 1 | named-spells.test.js | untriaged (tests certify it) |
| `SPELL_CONSUME_MATERIAL` | 1 | spell-requirements.test.js | untriaged (tests certify it) |
| `SPELL_DELAYED_BLAST_DETONATE` | 1 | remaining-spells.test.js | untriaged (tests certify it) |
| `SPELL_DELAYED_BLAST_GROW` | 1 | remaining-spells.test.js | untriaged (tests certify it) |
| `SPELL_HEAL` | 1 | healing-spells.test.js | untriaged (tests certify it) |
| `SPELL_MAGE_ARMOR` | 1 | followups.test.js, timed-effects.test.js | untriaged (tests certify it) |
| `SPELL_MAGIC_MISSILE` | 1 | remaining-spells.test.js | untriaged (tests certify it) |
| `SPELL_SLEEP` | 1 | sleep-spell.test.js | untriaged (tests certify it) |
| `SPELL_VAMPIRIC_TOUCH` | 1 | remaining-spells.test.js | untriaged (tests certify it) |
| `STAND_UP` | 1 | followups.test.js | untriaged (tests certify it) |
| `SURPRISE_CLEAR` | 1 | - | untriaged (no tests) |
| `SURPRISE_SET` | 1 | action-economy.test.js | untriaged (tests certify it) |
| `TOKEN_FORCE_MOVE` | 1 | effect-scheduler.test.js, positioning.test.js, scheduler-integration.test.js | untriaged (tests certify it) |
| `TOKEN_GROUP_SET_MEMBERS` | 1 | - | untriaged (no tests) |
| `TOKEN_TELEPORT` | 1 | effect-scheduler.test.js, positioning.test.js, scheduler-integration.test.js | untriaged (tests certify it) |
| `UI_CHAT_RECOUNT` | 1 | dock-panels.test.js, player-ui-state.test.js | untriaged (tests certify it) |
| `UI_DISCARD_DRAFT` | 1 | - | untriaged (no tests) |
| `UI_DRAFT_REQUEST` | 1 | player-ui-state.test.js | untriaged (tests certify it) |
| `UI_HOVER` | 1 | player-ui-state.test.js | untriaged (tests certify it) |
| `UI_RESET` | 1 | - | untriaged (no tests) |
| `UI_SET_FOCUS` | 1 | - | untriaged (no tests) |
| `UI_SET_SHEET_MODE` | 1 | player-ui-state.test.js | untriaged (tests certify it) |
| `UI_SUBMIT_DRAFT` | 1 | player-ui-state.test.js | untriaged (tests certify it) |
| `UI_UPDATE_MOVEMENT` | 1 | player-ui-state.test.js | untriaged (tests certify it) |
| `UI_WORKFLOW_CLEAR_RESULT` | 1 | - | untriaged (no tests) |
| `WAKE_CREATURE` | 1 | sleep-spell.test.js | untriaged (tests certify it) |

## Progress

- untriaged: 56
- unfinished: 2
- internal: 2
- shared: 1
