---
title: Home automation should be boring
tags:
  - seedling
  - home-automation
  - systems
---

The best smart home is one nobody in the house notices. If people have to think about the automation, it has failed.

## The litmus test

> [!question] Could a guest use your house?
> If a visitor can't turn on the lights without an app, a voice command, or an explanation, the system is too clever.

## Principles

1. **Physical controls always work.** Wall switches must keep working when Wi-Fi, the hub, or the cloud is down. Automation adds to manual control. It never replaces it.
2. **Local first.** Prefer devices that work without a vendor's cloud (Zigbee, Z-Wave, Matter over Thread). Cloud services get shut down. Your light switch shouldn't depend on a company's business model.
3. **Automate around presence and time, not commands.** Lights that come on at sunset or when someone arrives beat lights you ask for.
4. **Fail toward normal.** If a sensor dies, the room should behave like a normal room, not stay dark or keep the heating on.
5. **Change one thing at a time.** A home is a complex system that has to keep working while you change it, which is [[ideas/Gall's law|Gall's law]] in action.

## Good first automations

- Hallway light at low brightness when there's motion at night.
- Notify when the washing machine finishes (watch its power draw drop).
- Turn everything off when the last person leaves.

## Bad first automations

- Anything involving the front door lock.
- Anything that takes three integrations and a template to express.
- Anything your partner didn't agree to.

*This note is a seedling. It'll grow as I find out which automations survive a year of daily use.*
