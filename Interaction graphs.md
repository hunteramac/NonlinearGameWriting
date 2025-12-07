Interaction graphs are specifically written to work in conjunction with a more open ended 'game sim'

The game sim handles player actions which have high degrees of infinite variation. Eg movement, attacks, the specific choice of which snatch from a chest.
 *The exact degree a door is opened such that the rogue can peer into the room beyond (and the resulting simulation based checks for any NPCs within, to determine if the rogue is spotted)*

The interaction graph is deliberately separated from this infinite variation using an abstraction. The Sim and the graph communication via an **interface** that involves the sim, and the graph sending events to each other. And handlers on each respective side.

The interaction's graph purpose is to represent specific low variation occurrences, and possible player character actions that accompany them. Eg Character Dialog and resulting player character actions possible. 

The goal is to abstract the sim, so the actual writing of the igraph can proceed without being overwhelmed by needing to directly specify handling for infinite branching. While also keeping the writing generic, and possible to implement in virtually any specific game.

# Definition

The interaction graph is defined using obsidian.md files as follows

1. **Sim Events**
   These are communications from the Sim, to the interaction graph. The actual production is abstraction - unknown from the graph. The graph just knows that these can be created and received. 
   Ex The sim is defined to generate [[Zoltan spots Geralt's approach]], ideally when the player character walks up to the group outside the inn.

2. **Interaction graph state**
   What happens on receiving an event? SimEvents generally will connect to resulting state. Eg *Zoltan greets Geralt*
   State has assumptions around influencing the player character perception, and thus should generally lead into
	1. **Context Actions**
	   Specific precanned responses the player character can take to the interaction graphs state.
	   An action is made of
		1. **Action Declaration**
		   The exact representation of the possible action that player will be shown, to make their choice during a decision point involving context actions
		   2. **Resulting State**
		      The new resulting interaction graph state resulting from the action being performed by the player character
		      It may very well be defined as having variation Eg the classic mechanic of a speech check


3. **Interaction Graph Events**
   Certain occurrences within the graph should be able cause a change within the game sim. 
   Eg If an NPC bids PC farewell, and as the graph, we know they should depart. We need the sim to execute this in an opened manner, if, for example, it should be possible for the player character to interfere with it in some open ended way.

