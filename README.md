PML (Protocol Markup Language) Specification Rev.1

PML is a markup language designed for the sole task of defining functional protocols, typically encapsulated within Websockets.

The goal of this project is to develop a fully-functional language that can, on it's own, be used to develop web protocols with minimal need for programming in a 
language such as Node.js, Python, ectera. 

The current specification defines a standard command is written as follows:

[position] | [Cause-and-effect block] |     [Variable assignment]      | [parameter handling block];

   SRV     |     JCH > ACS            | (character[^.*], channel[^.*]) | (+sys.channel (^.*):^.character);

In this example, we are defining a server-side command named "ACS" which is triggered after the "JCH" command is recieved. Upon triggering, the command grabs 
paramters from the parent command (referenced by ^ instead of a variable name with * referencing the name of the variable being filled) to fill out the resulting response. Additionally, the command also updates server data
with the appropriate information. Since we're joining we are saying we wish to add a user to sys.channel[parrent.character] through the use of a + symbol.

To further clarify the use of the * symbol, this is explictly used to add an associated variable's name to the path of a referenced data source. For example:

character[^.*] translates to character[^.character]

Likewise channel[^.*] translates to channel[^.channel]

Defining variable types is not settled currently, but I imagine that it would be done in either a seperate file or with a keyword prepending a line to discern 
variable from command definitions.
