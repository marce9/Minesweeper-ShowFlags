# **Minesweeper-ShowFlags**

Patching the old Minesweeper, so when a new game starts the cells which hide mines will show flags.

The game was reveresed using IDA Pro and OllyDbg.

Strategy:
----------
Understand when the board is being drawn:
0x10026A7 - Changing the board cells

Determine which code is being called when you press a cell button (doesn't matter left mouse click (mine) or right click(flag))
0x1002690 - value of function that change cell once it was clicked

Once you click on a cell with a mine, determine where the check if the cell hides a mine occur:
No check - the answer lies with a bitwise 'AND' between the cell value and 0x1F.
The instruction is at: 0x10026E9


Important Functions:
---------------------
GetDC - get the board for changes

BitBlt - Change cell icon


Importent Values:
-----------------
0x1005A20 - value of hdcSrc - start of icons array in memory

0x0F - value of blank cell

0x8E - value of colored flag

0x8F - value of mine (hidden)

0xCC - value of mine (pressed - not hidden)

0x40 - value of empty cell

0x41 - value of '1', etc...(1,2,3... = 41,42,43...)

0x1F - Every cell value gets bitwise 'AND'

Result of 'AND':

0x0000000E - set Flag

0x0000000F - set blank cell

0x00000000 - set empty cell
