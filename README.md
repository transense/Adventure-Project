# Adventure
## Shreyas Desai - sdesai33@stevens.edu
## Vaibhavi Shah - vshah6@stevens.edu

### Github Repo: [Project 2 - Adventure](https://github.com/shreyas-desai/Adventure-Project)

### Estimated Hours Spent: 10-12

### Testing of code
A `test.py` file was created which looked for the `*.in` files in the `test` directory and compared the files with `*.out` files. The input files were created by copying the contents from the command line for the program after it was run with the same commands given in canvas and output files contained the output given on canvas.</br></br>
__*The test directory and `test.py` file have not been pushed to github to keep the working directory clean.*__

### Known Bugs or Issues
None
### Resolved Issues
Passing of testcases - 
1. The testcases on Gradescope were not being passed because the code was exiting the system for `quit` verb using `sys.exit('Goodbye!')`. Resolved this issue by using `quit()` instead.
    
2. A few testcases passed after the above change. For the rest of testcases to pass, the code was modularized and encapsulation was used. A class for the game engine was declared and object was created in the *`__init__`* method.</br></br>

Resolving arbitrary spaces in the commands -     
1. The working of the game when given arbitrary spaces in between verbs and nouns (game commands), was fixed by stripping the command from both sides and splitting the the commands with any type of space in between (*`\r,\t,\n`*).</br>

### Extensions
#### 1. `help` verb</br>
This verb shows the help string for all the verbs declared inside the game, including the new added extensions</br>

To keep the working of the verb dynamic, every callable function has a simple docstring which explains the working of function(verb) in short. The help function prints these docstrings. </br>
Hence even if a new function is added (unless it does not have a docstring) the `help` verb will show the help for that function.

##### Usage
```
$ python3 adventure.py ambig2.map
> A white room

You are in a simple room with white walls.

Exits: north northwest

What would you like to do? help
drop 
            -- Drop items from the inventory in current room
get ... 
            -- Get a specified item.
go ... 
            -- Go in a particular direction. [east, west, south, north, northeast, northwest, southeast, southwest]
help
            -- How to play?
inventory
            -- Show the inventory.
look
            -- Look around the current room.
What would you like to do?
```

#### 2. `drop` verb
This verb drops the items present in the inventory. If there is no *`item`* inside the inventory, it shows an error message.
##### Usage
```
$ python3 adventure.py ambig2.map
> A white room

You are in a simple room with white walls.

Exits: north northwest

What would you like to do? go northwest
You go northwest.

> A green room

You are in a simple room, with bright green walls.

Items: banana, bandana, bellows, deck of cards

Exits: east southeast

What would you like to do? get banana
You pick up the banana.
What would you like to do? get bandana
You pick up the bandana.
What would you like to do? inventory
Inventory:
  banana
  bandana
What would you like to do? drop banana
You dropped banana.
What would you like to do? inventory
Inventory:
  bandana
What would you like to do? drop banana
You are not carrying banana.
What would you like to do? 
```
#### 3. Locked doors
This functionality does not include a verb for usage (per se). It is more like a kind of state the game is in.</br> 

The logic behind this extension is as follows:</br>
a. Let's say there is a direction in which you want to go, you use the `go` verb to do that. </br>
b. If the door, which you want to enter requires some items and you dont have those items in your inventory, you cannot enter the room.</br>
c. So you roam around the world to find those items, `get` them in your inventory, and then go back to the room which you want to enter.</br>
d. Now, if you have the correct set of item(s), you can enter the room as usual.
##### Usage

```
$ python3 adventure.py ambig2.map
> A white room

You are in a simple room with white walls.

Exits: north northwest

What would you like to do? go north
You need bandana, bellows to pass through this door.
What would you like to do? go northwest
You go northwest.

> A green room

You are in a simple room, with bright green walls.

Items: banana, bandana, bellows, deck of cards

Exits: east southeast

What would you like to do? get bellows
You pick up the bellows.
What would you like to do? go east ## East in this room and north in the white room point at the same door.
You need bandana to pass through this door.
What would you like to do? get bandana
You pick up the bandana.
What would you like to do? inventory
Inventory:
  bandana
  bellows
What would you like to do? go east 
You go east.

> A blue room

This room is simple, too, but with blue walls.

Items: green potion, blue potion, black potion

Exits: west south

What would you like to do? go south
You need green potion to pass through this door.
What would you like to do? get green potion
You pick up the green potion.
What would you like to do? go south
You go south.

> A black room

You are in a dark room, smells of mystery here.

Exits: north northeast

What would you like to do? 
```

2 new maps, `ambig2.map` and `loop2.map` have beed added to check the working of the extensions.

#### 4. `Winning and Losing conditions` 

This functionality does not include a verb. It is new feature in the game for adventurous purposes.</br> 

The logic behind this extension is as follows:</br>
a. In the map danger, the villain 'Night King' has been added to the map. </br>
b. The villain is located in the north, We need to kill the villain to win the game. When the user attempt to go to north , danger message will displayed and ask user if they want to continue. </br>
c. The user can get the items from golden room and the iron room.</br> 
d. To defeat the villain play required a weapon, if player enter without weapon, villain will kill the player and game will end.</br>
e. If player has the weapon they can enter the room and killed the villain after entering the room north, win the game.

##### Usage
```
$ python3 adventure.py danger.map
> A white room

You are in a simple room with white walls.

Exits: north northwest south

What would you like to do? north
Danger!
Do you wish to continue?(Y/n)y
The Night King killed you..
You died!


python .\adventure.py .\danger.map
> A white room

You are in a simple room with white walls.

Exits: north northwest south

What would you like to do? south
You go south.

> A golden room

Somebody cooked here !!

Items: frog potion, bat potion, chameleon potion

Exits: west north

What would you like to do? get frog potion
You pick up the frog potion.
What would you like to do? go west
You go west.

> An iron room

The Nights are getting longer, winter is coming......

Items: longclaw, needle, oathkeeper, heartsbane

Exits: north

What would you like to do? get longclaw
You pick up the longclaw.
What would you like to do? go north
Danger!
Do you wish to continue?(Y/n)y
You go north.

> The NIGHTFORT

The Long Night...

Exits: north northeast

You killed the Night King.
The wall stands..
```

#### 5. `Directions` verb
In this extension, players can now directly use directions as verbs to navigate. Previously, entering only a direction resulted in an error since the "go" verb wasn't added. However, with this extension, players can move in any direction by simply typing the direction itself.
##### Usage
```
$  python .\adventure.py .\danger.map
> A white room

You are in a simple room with white walls.

Exits: north northwest south

What would you like to do? northwest
You go northwest.

> An iron room

The Nights are getting longer, winter is coming......

Items: longclaw, needle, oathkeeper, heartsbane

Exits: north

What would you like to do? north
Danger! 
```