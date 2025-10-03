# Finite-State-Machine
A lightweight and extensible finite state machine for Roblox, with hooks, guards, and predictable transitions.

# 🧭 FiniteStateMachine (FSM)

A lightweight and extensible finite state machine for Roblox, with hooks, guards, and predictable transitions.

---

## ✨ Features
- 🔒 **Controlled state changes** — States can only change via `:changeState`
- 🪝 **Hooks for every stage** of the lifecycle (before/after enter/leave)
- 🚫 **Invalid/redundant transition prevention**
- 🔀 **Specific transition callbacks** (e.g., only run when moving from `Idle → Attack`)
- ⚡ **Lightweight and fast** — works on both client and server

---

## 📖 Use Cases
- 🗡 Combat phases  
- 🤖 AI behavior states  
- 🎞 Animation flows  
- ⏳ Ability cooldowns  
- 🖥 UI screen navigation  

---

## 🚀 Getting Started

### 1. Create an FSM
```lua
local FSM = require(path.to.FSM)

local states = { "Idle", "Attack", "Recover" }
local fsm = FSM.new(states)

fsm.currentState = "Idle"
```
2. Add Hooks
```lua
table.insert(fsm.beforeLeave["Idle"], function()
    print("Leaving Idle state...")
end)

table.insert(fsm.afterEnter["Attack"], function()
    print("Entered Attack state!")
end)
```
3. Change States
```lua
fsm:changeState("Attack") -- Runs Idle → Attack hooks in order
```
## 🔄 Lifecycle & Hook Order
When calling :changeState(newState):

beforeLeave[oldState]

beforeEnter[newState]

specificTransitions[oldState][newState]

afterLeave[oldState]

afterEnter[newState]

## ❌ A transition will not occur if:

newState is not valid

newState == currentState

isInvalid[oldState][newState] is set

## ✅ Benefits
Predictable, clear state management

Extensible with transition guards & hooks

Prevents invalid/redundant transitions

Works on both client and server

Ideal for scalable systems like AI, abilities, and UI
