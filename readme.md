MSP430 Assembly Syntax Support
==============================

This language file provides basic syntax support within Sublime Text 2 for the MSP430x assembly file.

Features
* Syntax support for instructions and registers
* Support for different address modes
* Labels are identified as entity.name.function for the purpose of code browsing

Special Comment Syntax
----------------------

Additionally, special comments can take one of the following 3 forms:
* ; arg: paramName @ R12
* ; add: variableName @ R12
* ; del: variableName @ R12
For comments in this form the register (e.g R12) will be highlighted as a register. If "arg" or "add" is used the variable name will be given a scope of `variable.other.declaration.msp430x`. If "del" is used the scope will be `variable.other.undeclaration.msp430x` (note "undeclaration"). You can optionally add the following scopes to your color scheme (tmTheme file) to highlight these in green and red respsectively. 

<!-- language: lang-xml -->
	<dict>
		<key>name</key>
		<string>Variable declaration</string>
		<key>scope</key>
		<string>variable.other.declaration.msp430x</string>
		<key>settings</key>
		<dict>
			<key>foreground</key>
			<string>#060</string>
			<key>fontStyle</key>
			<string>bold</string>
		</dict>
	</dict>
	<dict>
		<key>name</key>
		<string>Variable undeclaration</string>
		<key>scope</key>
		<string>variable.other.undeclaration.msp430x</string>
		<key>settings</key>
		<dict>
			<key>foreground</key>
			<string>#600</string>
			<key>fontStyle</key>
			<string>bold</string>
		</dict>
	</dict>

The idea is that when you use a register, you name the variable that the register contains and notify readers that the variable has entered scope by commenting `; add: variableName @ R5`. When the variable is no longer needed, you can notify readers that variable is no longer in scope by commenting `; del: variableName @ R5`. Then when you need a spare register later on you just have to look for the last deleted variable that doesn't have a corresponding new variable in the same register. The initial variables are the arguments, and should be commented at the beginning of a function by `; arg: paramName @ R12`.