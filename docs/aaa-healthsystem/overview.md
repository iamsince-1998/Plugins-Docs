---
id: overview
title: Overview
sidebar_position: 1
---

# AAA_HealthSystem

You can use this plugin with any version of Unreal Engine. Just download it and build it.

The plugin provides a reusable health system that can be added as a component to any actor and automatically triggers events on death and health changes.

**Multiplayer Ready**.

If you need any feature, reach out on Discord:
- https://discord.gg/vxn4gadpwC

## New Update v1.5

- More server-authoritative approach
- UE 5.7 support

To get the demo project, switch to the `project` branch and download it.

## Features

- ✅ Simple and easy to use
- ✅ Armor and health work in sync
- ✅ Add health component to any actor
- ✅ On Health Changed event
- ✅ On MaxHealth Changed event
- ✅ On Update HealthBar event (returns a 0-1 value)
- ✅ On Update MaxHealthBar event (returns a 0-1 value)
- ✅ Multiplayer ready
- ✅ Network replicated (see demo project on `project` branch)
- ✅ Full Blueprint access

### Preview Images

![Health System UI](https://github.com/user-attachments/assets/10fd2d60-9289-40a3-b5ce-19eaafb87ff3)

![Health and Armor](https://github.com/user-attachments/assets/ab57210e-66f4-4f1b-ab3a-a8add924dffd)

## Step-by-Step Guide

### Step 1. Install Plugin via Epic Launcher or GitHub

Using Epic Launcher:

![Install from Epic Launcher](https://github.com/user-attachments/assets/6ea4dd78-4e81-4340-bd54-11c2ff3f4ff3)

Using GitHub:

![Install from GitHub](https://github.com/user-attachments/assets/5d267dcd-ba93-4d6a-85fa-919253bbcfd0)

### Step 2. GitHub installation notes

If you are using the Epic Launcher version, skip this step.

If using GitHub, make sure you have a C++ project. If not, create a C++ class once. Then create a `Plugins` folder in your project and add the downloaded plugin.

![GitHub plugin folder setup](https://github.com/user-attachments/assets/e5373a00-6cc4-457c-b3b9-adc142d7f623)

Expected path example:

`D:\GitHub\AAA_HealthSystem\Plugins\AAA_HealthSystem`

![Plugin path example](https://github.com/user-attachments/assets/433363f1-a58d-47af-b17e-8178624deb69)

Now generate project files and build.

### Step 3. Add component to your actor

Add the `AAA_HealthSystem` component to your actor class (for example, your `PlayerCharacter`).

![Add component](https://github.com/user-attachments/assets/8b58b6f7-8bc4-4a0d-b57a-6a4f589a65d5)

### Step 4. Configure component settings

Select the component in the Details panel to access settings.

![Details panel](https://github.com/user-attachments/assets/7ae52056-ac29-4146-aa7b-ae25efa89e64)

### Step 5. Modify Health settings

![Health settings](https://github.com/user-attachments/assets/bb0dbf06-f83a-4079-8aea-e6f20a92e8da)

- `Health`: current health.
- `MaxHealth`: maximum health cap.
- `HealthBarPercentage`: helper value for progress bars (`Health / HealthBarPercentage`).

### Step 6. Modify Armor settings

![Armor settings](https://github.com/user-attachments/assets/8ffef254-9fad-43a3-a6c3-18a1a2cea7c2)

- `HasArmor`: enables armor.
- `ArmorDamageMultiplier`: default `1`, controls armor drain rate.
- `RegenerateArmor`: regenerates armor (after health if both are enabled).

### Step 7. Apply damage

![Damage actor](https://github.com/user-attachments/assets/f6775b9b-2636-48c4-ba5a-83ede0acfd11)

Use your own damage logic as needed.

### Step 8. Use AnyDamage event

![AnyDamage event](https://github.com/user-attachments/assets/342ef9ef-09b1-47b0-967b-27379dc464a1)

This event tells you the actor was damaged. With armor enabled, armor is consumed first, then health.

### Step 9. Regenerate health

![Regenerate health](https://github.com/user-attachments/assets/24313210-9b64-4109-b13c-70bc36dee018)

Regeneration can be used while alive, and armor can regenerate as well when enabled.

- `InTime`: repetition interval.
- `HealthToRegin`: amount regenerated per interval.

### Step 10. Event dispatchers for UI

Select the `AAA_HealthSystem` component in Details to access dispatchers.

![Dispatchers list](https://github.com/user-attachments/assets/e4d041ef-1f07-4769-a383-5fa91b2e124a)

Use these to bind health and armor progress bar updates.

![Bind progress bars](https://github.com/user-attachments/assets/2f562a8c-df2e-4eee-9a49-5e90c8c2154e)

### Step 11. Additional helper functions

For health:

![Health helper functions](https://github.com/user-attachments/assets/b29ac1c6-5be2-4606-85f2-0ca07388e8d6)

For armor:

![Armor helper functions](https://github.com/user-attachments/assets/46e031b1-9515-4af0-bd30-d17c6514cbf1)

Additional dispatchers:

![More event dispatchers](https://github.com/user-attachments/assets/e11e13e3-9a16-49df-b6b3-1c5b02f80c60)

## Demo Project

You can find the demo project in the same repo. Choose the `project` branch and download it.

![Demo project branch](https://github.com/user-attachments/assets/f8b4780a-8058-429e-9d75-641d814a7534)

If you face any issues, feel free to DM on Discord.

Contributions are welcome.
