# Metadata

- CTF: CyberSphere Advanced CTF
- Category: Misc (game pwn)  
- Author: Ahmed Limam 

# Overview 

In this challenge, we are given a `game.exe` file.

# Thought process 
## The game

A custom goofy game made by the author, developed using the open-source Godot Engine.

![[01-game-overview.png]]

I noticed a platform at the top of the map, but it is clearly unreachable.

![[02-game-overview.png]]
## Vulnerability detection:

We need to reach the platform at the top, so we need infinite mid-air jumps. It's a common technique. I'm going to show you how to do it.

# Exploit process

Achieving infinite jumps with Cheat Engine involves scanning for the memory address that tracks whether the player is in the air (typically a boolean 0 for air, 1 for ground) or finding the jump count/height variable.

By changing this value to, or freezing it at, `0` (grounded) while in the air, you can bypass jump limits.

> *Notice : In this game, boolean `1` is associated with being grounded and `0` with being in the air.

![[cheat-engine-overview.png]]

We select the process related to the game.

![[cheat-engine-process-list.png]]

We start our first scan with:

- Scan Type : Exact value 
- Value Type : Hex 
- Hex : `1` (since  the player is on the ground)

Next scans: 

- Scan Type : Exact value 
- Value Type : Hex 
- Hex : `1` (while the player is on the ground)

- Scan Type : Exact value 
- Value Type : Hex 
- Hex : `0` (while the player is in mid-air)


> *Notice : Enable Speedhack and decrease the value so you can launch your scan in sync with the player's movement.

![[final-scan.png]]

Repeating this process multiple times helps identify the correct address associated with the boolean value that indicates whether the character is currently in the air or on the ground.

We freeze the value and there we go we are flying!

![[01-flying-poc.png]]

![[02-flying-poc.png]]

**THE GAME IS PWNED! 

The challenge is not finished yet because we didn't find a flag we found a hex key instead.

![[hex-key.png]]

Small equation:

**HEX KEY + EXE file = project recovery with [GDRETools](https://github.com/GDRETools)

![[gdre-command.png]]

I opened the game folder with Godot. I browsed the objects and found some hidden ones. I enabled them, and now I can read the flag clearly. 

![[game-in-godot.png]]

![[flag.png]]

# Conclusion 

I hope you guys learned something new reading this writeup. Shoutout to the author **Ahmed Limam** for this challenge. I really had fun.


