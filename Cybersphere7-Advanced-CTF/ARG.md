# Metadata

- CTF: CyberSphere Advanced CTF
- Category: Misc (game pwn)  
- Author: Ahmed Limam 

# Overview 

In this challenge, we are given a zip file containing files for a game.

# Thought process 

## The game

Cave Story is a 2004 Metroidvania game for Microsoft Windows. *Doukutsu Monogatari*

![01-game-info](screenshots/01-game-info.png)


## Vulnerability detection:

The game's objective is exploring and escaping, protecting the mimigas, and combat and upgrading. But to be honest, I don't care. I noticed that the flag is made with 2D objects on the screen, but it's unreachable because the camera focuses on the player and reading the flag is impossible. 


![flag-noticing](screenshots/flag-noticing.png)

So I thought of manipulating the camera movements to be able to read the flag.

# Exploit process 

To achieve this, we must modify the camera values inside the game. To do this I will be using Cheat Engine. 

![cheat-engine-overview](screenshots/cheat-engine-overview.png)

The way Cheat Engine works is that we look for a value in an address that changes as expected. This address could contain the value for our camera movements. 

To access the addresses in the game, I chose the process related to the game. We can choose the target process from the menu in the upper left corner with flashing borders.

![process-list](screenshots/process-list.png)

Now we look for a value in an address that changes as expected. So I launch a First Scan
Scan Type : Unknown initial value 
Value Type : Float 

![First-scan](screenshots/First-scan.png)


I found around 14k Address. So we start the filtering with moving the camera to the right and changing the Scan type to Increased value then moving the camera to the left and changing the Scan type to Decreased value. 

We repeat this process a couple of times to identify the right Address 


![scan-increased](screenshots/scan-increased.png)

![scan-decreased](screenshots/scan-decreased.png)

When I found the Address associated to the camera right and left movement. I selected the item and gave it a huge value so the camera moves to the top right of the screen so i be able to read the flag clearly. 

THE GAME IS PWNED! 
![flag-1](screenshots/flag-1.png)

![flag-2](screenshots/flag-2.png)

# Conclusion 

I really enjoyed playing this challenge. Respect to the author **Ahmed Limam** for this great challenge. This writeup represents my own way solving this challenge so no need to mention that there is many ways to solve this challenge .


