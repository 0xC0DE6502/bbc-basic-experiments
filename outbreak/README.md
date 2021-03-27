# BASIC 10 LINER CONTEST 2021: OUTBREAK


## Entry

Title: Outbreak

Author: [0xC0DE](https://twitter.com/0xC0DE6502)

Category: PUR-80

Platform: Acorn Electron, BBC Micro

Language: BBC BASIC 2

![Outbreak Screenshot](https://github.com/0xC0DE6502/bbc-basic-experiments/blob/master/outbreak/outbreak-screenshot.png?raw=true)


## Instructions

Break down the wall of 112 coloured bricks with your bat and ball. Move your bat left and right with the left arrow and right arrow keys respectively. You have 3 lives to score as many points as possible. There is an infinite number of brick walls so you had better get started!


## Running the game

Outbreak should be played on a real Acorn Electron or BBC Micro of course. For your convenience, it will also work in an emulator like [Electrem](http://electrem.emuunlim.com/Downloads.html), [Beebem](https://github.com/stardot/beebem-windows) or [jsbeeb](https://bbc.godbolt.org/). 

Download the [disk image](https://github.com/0xC0DE6502/bbc-basic-experiments/blob/master/outbreak/outbreak.ssd) and open it with one of the emulators. In the emulator, hold `SHIFT` and tap `BREAK` (usually key `F12`) to automatically boot the disk image and start playing Outbreak.


## Game listing (with proof of PUR-80)

```
REM01234567890123456789012345678901234567890123456789012345678901234567890123456789
REM0         1         2         3         4         5         6         7

   0MO.2:A=-1:V.23;8202;0;0;0;23,A,A;A;A;A;:X=7:Y=28:R=3:Q=0:F=31:S=32:T=64:@%=&505
   1V.4,12:MOV.0,Y:F.K=1TOS:V.4-(K=S),A:P.SP.18;:V.A:N.:V.4,F,11,30:P.Q;" ";R:M=79
   2F.K=4TO11:V.F,3,K:F.L=1TO14:C.RND(7):V.A:N.,:C.7:V.F,2,30:P."OUTBREAK":G=112
   3B=X+2:C=5:V=.2*RND(4)-.5:W=1:GC.3,7:MOV.B*T,C*S:V.5,M:IFR<3A.G<112SO.0,-10,6,5
   4X=X+(INKEY-26A.X>0)-(INKEY-122A.X<15):V.4,F,X,Y,-S*(X>0),X<1,A,A:O=B:IFG=0G.1
   5V.A,-S*(X<15),5:P=C:B=B+V:C=C+W:IFB<1B=1:V=-V:EL.IFB>18:B=18:V=-V:ME$="0xC0DE"
   6I=O*T+S:J=P*S-16:IFC=5A.B>=X+.3A.B<=X+3.7W=-W:V=(B-X-2)*.4:SO.1,-10,80,1
   7Z=PO.I,J):IFC>S:C=S-W:W=-W:EL.IFC<-1R=R-1:V.4,F,17,30:P.;R:G.-3*(R>0):YEAR=2021
   8D=C>5A.Z:IFD:SO.1,-10,150,1:MOV.T*(I DIVT),S*(J DIVS)+28:GC.3,Z:V.A:Q=Q+Z:C=P-W
   9GC.3,7:MOV.O*T,P*S:V.M:MOV.B*T,C*S:V.M:IFD:W=-W:G=G-1:V.4,F,11,30:P.Q:G.4EL.G.4

REM01234567890123456789012345678901234567890123456789012345678901234567890123456789
REM0         1         2         3         4         5         6         7
```


## Explanation per line

```
0MO.2:A=-1:V.23;8202;0;0;0;23,A,A;A;A;A;:X=7:Y=28:R=3:Q=0:F=31:S=32:T=64:@%=&505
```

Initialisation. Switch to graphics MODE 2 (160x256x8), disable the cursor (for cosmetic reasons) and create user defined graphics character 255 (UDG). This is a solid block used for the walls on the left and right, for the brick wall itself, and for the player bat. Initialise lives (R) and score (Q). Define the initial position for the player bat (X and Y). Define a few constants (F, S, T) to keep the program as short as possible. Finally, make sure we print numbers in the correct format (@%).

```
1V.4,12:MOV.0,Y:F.K=1TOS:V.4-(K=S),A:P.SP.18;:V.A:N.:V.4,F,11,30:P.Q;" ";R:M=79
```

Start level. Switch to text mode, clear the screen and draw the wall on the left and on the right. That is 32 (S) text lines. Show initial score (Q) and lives (R) at text position (11,30) at the bottom of the screen. Define constant M as 79, which just happens to be the code for the letter "O" also known as the ball.

```
2F.K=4TO11:V.F,3,K:F.L=1TO14:C.RND(7):V.A:N.,:C.7:V.F,2,30:P."OUTBREAK":G=112
```

Draw brick wall. The wall is made of 14x8 (=112) coloured bricks (UDG 255). Each brick is randomly assigned one of the 7 colours: red, green, yellow, blue, magenta, cyan and white. The name of the game (Outbreak) is shown at text position (2,30) and brick counter (G) is initialised to 112 (=14x8 bricks). We need this to determine if all bricks have been smashed or not.

```
3B=X+2:C=5:V=.2*RND(4)-.5:W=1:GC.3,7:MOV.B*T,C*S:V.5,M:IFR<3A.G<112SO.0,-10,6,5
```

Start ball. Set initial position (B,C) of the ball ('O') in the middle of and just above the bat. Set initial (randomized) horizontal speed (V) and (fixed) vertical speed (W) of the ball. Draw the ball in colour white. Play a 'crash' sound if we have just lost a life.

```
4X=X+(INKEY-26A.X>0)-(INKEY-122A.X<15):V.4,F,X,Y,-S*(X>0),X<1,A,A:O=B:IFG=0G.1
```

Move and draw bat. Update horizontal position (X) of the bat by checking the left and right arrow keys. Draw the left part of the bat. Remember the current horizontal position of the ball (O) so we know where to erase it later. If we have smashed all 112 bricks, rebuild the wall and continue playing (line 1).

```
5V.A,-S*(X<15),5:P=C:B=B+V:C=C+W:IFB<1B=1:V=-V:EL.IFB>18:B=18:V=-V:ME$="0xC0DE"
```

Move ball. Draw the right part of the bat. Remember the current vertical position of the ball (P) so we know where to erase it later. Update the ball position using horizontal and vertical speed (V,W). If the ball hits the left wall or the right wall, we need to invert its horizontal speed to create a bounce effect. Easter egg: my alias 0xC0DE.

```
6I=O*T+S:J=P*S-16:IFC=5A.B>=X+.3A.B<=X+3.7W=-W:V=(B-X-2)*.4:SO.1,-10,80,1
```

Hit ball. Calculate the graphics position of the center of the ball. This is used in the next lines for collision detection. If the ball is just above the bat, invert its vertical speed for a bounce effect. Additionally, adjust its horizontal speed according to where the ball hit the bat exactly. This ensures different bounce angles from the bat. Play a sound to show the bat hit the ball upwards again.

```
7Z=PO.I,J):IFC>S:C=S-W:W=-W:EL.IFC<-1R=R-1:V.4,F,17,30:P.;R:G.-3*(R>0):YEAR=2021
```

Vertical bounds. First, get the colour (Z) of the pixel in the center of the ball. This is a crude collision detection between ball and brick, used in the next line. If the ball has reached the top of the screen, invert its vertical speed for a bounce effect. If the ball has reached the bottom of the screen, you lose a life. Update the number of lives (R) shown on the screen. If you still have some lives left, continue playing from line 3. If lives has reached zero, it's game over and the game starts again from line 0. Easter egg: the year this game was made by me.

```
8D=C>5A.Z:IFD:SO.1,-10,150,1:MOV.T*(I DIVT),S*(J DIVS)+28:GC.3,Z:V.A:Q=Q+Z:C=P-W
```

Hit brick. If the ball is anywhere on the screen above the bat and the colour (Z) in the center of the ball is anything other than black, we have hit a brick! Play a sound to show this and erase that brick. Increase your score according to the colour of the brick: red +1, green +2, yellow +3, blue +4, magenta 5, cyan +6 and white +7.

```
9GC.3,7:MOV.O*T,P*S:V.M:MOV.B*T,C*S:V.M:IFD:W=-W:G=G-1:V.4,F,11,30:P.Q:G.4EL.G.4
```

Redraw ball. Erase the ball at its old position (O,P) and draw it at its new position (B,C). If we hit a brick (as checked in the previous line), decrement the total brick counter (G) and update the your score (Q) as shown on the screen. Finally, continue playing from line 4.


Outbreak - Copyright (C) 2021 [0xC0DE](https://twitter.com/0xC0DE6502)
