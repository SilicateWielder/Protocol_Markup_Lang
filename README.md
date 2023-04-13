# Protocol Markup Language (PML) Proposal.

Protocol Markup Language (PML) is a domain-specific language designed for the express purpose of fast-tracking protocol development and implementation.

This particular revision of the language was created out of thin air while trying to find a way to re-implement the F-chat client's protocols from scratch. It's purpose is to allow developers to define protocols in a single file. However currently I see at least a temporary need for mapping files to supplement PLM definitions, perhaps in the form of PVM or PVML files. These would likely follow their own DSL (Domain-specific Language)

As of this revision it is currently considred that each line is it's own definition. A command definition is as-follows:

``(NUL > OB ! PIN) PIN {} // Ping command, requires PIN in response.``

This definition was made referencing the resources over on wiki.f-list.net and as the command (borrowed from javascript) implies, this is a simple ping command.

We can break the command into three parts.

(*CAUSE-AND-EFECT*) *IDENTIFIER* { *PARAMETER DEFINTION* }

##CAUSE-AND-EFFECT BLOCK:
------------


The Cause and effect block defines the triggers and qeues this block has. It is always wrapped in parenthesis.

**OB** commonly refers to an outbound command, send to another system. and is seperated by a colon. However other key tags such as **IB** or **BI** can also 
exist. **BI** would be theoretical at this point in time, as I'm unsure how useful it is in practice. 



**NUL** is a reserved keyword that symbolizes the command has no qeue to follow, it cannot be chained like in this example where two commands are 
to be immediately sent in response:

``(OB > CDS+JCL)``

You could also require two commands, or have the option of triggering this command when one of two commands are recieved:
(JCH+PIN > OB) SOM // Must recieve JCH and PIN to send SOM
(JCH/PIN > OB) SOM // Either JCH or PIN can be recieved to send SOM 

##IDENTIFIER:

------------


The idenfifier is a section that is seperates from the rest of the definition with a space on either side. Only Alphanumberical values can be 
used to define it, however in the event that a payload may follow a different format, you can append an underscore and a number. It is generally good to assume 
that the first version is also a variant and must start at 0.

    (OB > NUL) AAA_0 { time }
    (OB > NUL) AAA_1 { time, year }

##PARAMATER TABLE:
------------

As you've seen in the last section with the identifier of a command. The parameter table is very basic at the moment, and needs further 
development. Simply add the variables you need seperated by commas. Ideally these should be unique to make for variable-mapping easier later.
