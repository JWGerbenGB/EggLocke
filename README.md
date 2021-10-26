# EggLocke
A tool used to generate Egglocke save files.
Simply load your save, change the settings to what you desire and click on "Generate Egglocke" to generate the new Egglocke save file.

Due to the way, this is coded, this works for most of the third-generation pokemon games.
However, one needs to configure their own Pokedex and Movedex, in order to tell the Egglocke maker which pokemon it can use and what moves it should give them.

I have created such Pokedexes/Movedexes for the following pokemon Rom hacks:

-Pokemon Emerald EX Speedchoice (Pokemon Emerald with all 898 pokemon, is randomizeable with a custom version of the UPR)  
-Pokemon Last Fire Red (Hard Pokemon Firered rom hack, utilizing the CFRU Engine)  
-Pokemon Radical Red (Hard Pokemon Firered rom hack, utilizing the CFRU Engine)  
-Pokemon GS Chronicles (Pokemon HG/SS remake, utilizing the CFRU Engine)  
-Pokemon Altered (Pokemon Firered rom hack, all pokemon are type-swapped)   
-Pokemon Sors (Pokemon Firered rom hack, using all gen 1 - 7 mon, new region, using Leons base)  
-Pokemon Firered 809 Randomizeable (Pokemon Firered rom hack, using all gen 1 - 7 mon, using Leons base, UPR compatible)  
-Pokemon Inclement Emerald (Emerald Decomp Difficulty/enhancement hack, using all gen 1 - 7 mon)  
Note: For those who don't know, UPR stands for Universal Pokemon Randomizer.

If you want to add your own rom hack, simply make your own XML file and place it in the Pokedex folder. 
If you use the CFRU engine, be sure to place the (CFRU), right before .xml.
If you use LEON's base, be sure to place the (LEON), right before .xml.
![image](https://user-images.githubusercontent.com/58632052/136632902-bf1f52cb-7f86-4326-b400-100e353bc07f.png)

# How do I add support for a new Gen 3 rom hack?
First of all, you need to make an Egglocke Pokedex, this will take quite a few hours so be warned!  
Starting off you need to create an xml document.  
If the game you want to add an egglocke to is a game utilizing the CFRU engine, then you need to name your xml file something ending in (CFRU).xml, or else corrupted saves will be created later on.  
If the game you want to add an egglocke to is a game utilizing LEON's base, then you need to name your xml file something ending in (LEON).xml, or else corrupted saves will be created later on.  

The first line in your xml document should be: &lt;?xml version="1.0" encoding="UTF-8"?>  
The second line in your xml document should be: &lt;pokedex>  
The last line in your xml document should be: &lt;/pokedex>  

Now, between the second and last line you need to insert all the pokemon that you want to be able to be generated, these are usually all first-stage pokemon.
Below I have given a snippet from one of the Pokedex as an example, the eggpokedexentry tag signals one entry into the egg Pokedex. Usually, every entry has one pokemon, however, some pokemon have multiple forms like Rotom and deerling. For those pokemon, multiple eggpokemon are clustered into one eggpokedexentry, otherwise, these pokemon forms would be treated as separate pokemon, and they would show up more often than others.

Every eggpokemon is comprised of a few parameters:  

-Name:  
This is the name of the first-stage pokemon, include the form name if applicable (like Rotom Heat).  

-internalId:   
This is the id the pokemon holds in the games' memory, this is usually not equal to the Pokedex id and must be manually determined.  

-egglocketypes:   
These hold all the tags of the first-stage pokemon's evolution line. This is used in the case that someone wants to do a themed run, generally speaking, these should include all the last stage pokemon types and any other miscellaneous tags that may apply to the pokemon's evolution line like Fossil, Starter, etc.  
Note: Only use the types listed in types.txt 

-firststagetypes:   
These are the types of the first-stage Pokemon, in order to give that pokemon the appropriate starting moveset.   
 
``` 
  <eggpokedexentry>
		<eggpokemon>
			<name>Bulbasaur</name>
			<internalid>1</internalid>
			<weight>1</weight>
			<egglocketypes>
				<type>Grass</type>
				<type>Poison</type>
				<type>Gen. 1 (Kanto)</type>
				<type>Starter</type>
			</egglocketypes>
			<firststagetypes>
				<type>Grass</type>
				<type>Poison</type>
			</firststagetypes>
		</eggpokemon>
	</eggpokedexentry>
	<eggpokedexentry>
		<eggpokemon>
			<name>Charmander</name>
			<internalid>4</internalid>
			<weight>1</weight>
			<egglocketypes>
				<type>Fire</type>
				<type>Flying</type>
				<type>Gen. 1 (Kanto)</type>
				<type>Starter</type>
			</egglocketypes>
			<firststagetypes>
				<type>Fire</type>
			</firststagetypes>
		</eggpokemon>
	</eggpokedexentry>
	<eggpokedexentry>
		<eggpokemon>
			<name>Squirtle</name>
			<internalid>7</internalid>
			<weight>1</weight>
			<egglocketypes>
				<type>Water</type>
				<type>Gen. 1 (Kanto)</type>
				<type>Starter</type>
			</egglocketypes>
			<firststagetypes>
				<type>Water</type>
			</firststagetypes>
		</eggpokemon>
	</eggpokedexentry>
```

When this is done, the movedex must be created. This is relatively simple compared to the previous task.  
I recommend duplicating an existing movedex, the content of which should look like this:

```
<?xml version="1.0" encoding="UTF-8"?>
<movedex>
	<bugmoveid>41</bugmoveid>
	<bugmovepp>20</bugmovepp>
...
	<standardmoveoneid>45</standardmoveoneid>
	<standardmoveonepp>40</standardmoveonepp>
	<standardmovetwoid>1</standardmovetwoid>
	<standardmovetwopp>35</standardmovetwopp>
</movedex>
```

For every type, there is a move id, which is the move id of the move that a first-stage pokemon with that type will be given in their starting moveset.  
The movepp is the pp of the aforementioned move. Pokemon can only have 2 types, so they can get a maximum of 2 moves from their types, as such the last 2 moves are dedicated to 2 moves every pokemon has in their starting move set. I usually choose Tackle and Growl for those moves.

# How do I find pokemon or move ids
For this, there are several DEV options baked into the egglocke maker tool.
For pokemon ids, you have to select the following:  
-[DEV]Test all possible pokemon  
-[DEV]Create pokemon instead of eggs  
-Pokemon in correct order  
-(optional): You can add an offset to the id in the Pokemon Generator Offset field.

When that's done, generate your save file, head over to your pc, and in box 1 slot 1 sits the pokemon with id 1 (assuming no offset).  
In box 1 slot 2 there is pokemon with id 2, and so on. Box 1 contains all pokemon with ids 1 - 30. Box 2 contains all pokemon with ids 31 - 60.  

As for Move ids, the process is similar, but for that, you also need to set the Pokemon Egg Move Preset to "[DEV] test", then box 1 slot 1 will have a pokemon with move id 1, etc.  
and just like the pokemon, you can add an offset. 

You might be asking "is there an easier way?", and the answer is "usually no" unless you can get support from the rom hack maker directly, this is the easiest way.
