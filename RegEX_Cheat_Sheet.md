#Regular Expressions (Regex) Cheat Sheet
Special Characters in Regular Expressions & their meanings

Character | Meaning | Example 
--- | --- | ---
* | Match zero, one or more of the previous | Ah* matches "Ahhhhh" or "A"
? | Match zero or one of the previous	| Ah? matches "Al" or "Ah"
+ | Match one or more of the previous	| Ah+ matches "Ah" or "Ahhh" but not "A"
\ | Used to escape a special character	| Hungry\? matches "Hungry?"
.	| Wildcard character, matches any character	| do.* matches "dog", "door", "dot", etc.
( )	| Group characters	| See example for |
[ ]	| Matches a range of characters	| [cbf]ar matches "car", "bar", or "far" <br \>[0-9]+ matches any positive integer <br \>[a-zA-Z] matches ascii letters a-z (uppercase and lower case) <br \>[^0-9] matches any character not 0-9.,  
\| | Matche previous OR next character/group	| (Mon)\|(Tues)day matches "Monday" or "Tuesday"
{ }	| Matches a specified number of occurrences of the previous	| [0-9]{3} matches "315" but not "31" <br \>[0-9]{2,4} matches "12", "123", and "1234" <br \>[0-9]{2,} matches "1234567..."
^ | Beginning of a string. Or within a character range [] negation. |	^http matches strings that begin with http, such as a url. <br \>[^0-9] matches any character not 0-9.
$ | End of a string.	| ing$ matches "exciting" but not "ingenious"



#Regular Expressions (Regex) Character Classes Cheat Sheet
POSIX Character Classes for Regular Expressions & their meanings

Character Class | Meaning
--- | --- 
[:alpha:]	| Any letter, [A-Za-z]
[:upper:]	| Any uppercase letter, [A-Z]
[:lower:]	| Any lowercase letter, [a-z]
[:digit:]	| Any digit, [0-9]
[:alnum:]	| Any alphanumeric character, [A-Za-z0-9]
[:xdigit:]	| Any hexadecimal digit, [0-9A-Fa-f]
[:space:]	| A tab, new line, vertical tab, form feed, carriage return, or space
[:blank:]	| A space or a tab.
[:print:]	| Any printable character
[:punct:]	| Any punctuation character: ! ' # S % & ' ( ) * + , - . / : ; < = > ? @ [ / ] ^ _ { | } ~
[:graph:]	| Any character defined as a printable character except those defined as part of the space character class
[:word:]	| Continuous string of alphanumeric characters and underscores.
[:ascii:]	| ASCII characters, in the range: 0-127
[:cntrl:]	| Any character not part of the character classes: [:upper:], [:lower:], [:alpha:], [:digit:], [:punct:], [:graph:], [:print:], [:xdigit:]
