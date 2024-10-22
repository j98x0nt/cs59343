java c
ENGGEN  131 – Semester Two – 2024
C Programming Project
BOXED IN
Deadline:  11:59pm, Saturday  19th   October
Worth:  12% of your final grade
A little background
Who knew that pushing boxes around could be so much fun!
Sokoban (which means “warehouse keeper” in Japanese) is a classic puzzle game that was
originally developed as a video game in 1982 by Hiroyuki Imabayashi.  The game became an instant hit, and it has captivated players around the world with its blend of simple mechanics  (literally pushing boxes) and deep strategy.
In this project, you are going to develop a version of the Sokoban game called “Boxed In” .
The gameplay involves the player controlling a person in a warehouse depicted as a 2-dimensional grid of
floor (i.e. empty space) and wall (i.e. immovable
barrier) squares. Some floor squares contain boxes,
while others are marked as storage locations (i.e.
targets). The goal is pretty straightforward: move all of  the boxes onto the targets.  Sounds simple, right?  Well, the challenge lies in the player’s ability to only push
boxes – and never pull boxes!   This means care must be taken to avoid trapping boxes in corners or blocking a    crucial path and creating unwinnable scenarios.
Sokoban puzzles aren’tjust fun – they’ve also been
studied in computer science. The problem of solving Sokoban has been proven to be “NP-hard”, which
means the problems are difficult to solve because there is no known quick or efficient way to find a solution.
These problems get much harder as they get bigger, with the number of required moves growing exponentially.
In this project, you will be implementing – step by step – the required functionality for the “Boxed In” game.
Once you have completed the game, you can spend hours and hours playing it, all throughout the summer holidays.
Have fun!
An important note before we begin …
Welcome to the C Programming project for ENGGEN 131 2024!
This project is organized as a series of related tasks.  When combined, the tasks will complete
the implementation for the game.  For each task there is a problem description, and you must
implement one required function to solve that problem.  In addition to the required function, you may define other optional functions which the required function calls upon (i.e. so-called helper  functions).  Using helper functions is often a useful way to organize your code, as several simpler functions can be easier to read and understand than one complex function.
Do your very best, but don’t worry if you cannot complete every task.   You will get credit for each task that you do solve.
IMPORTANT - Read carefully
This project is an assessment for the ENGGEN  131 course.  It is an individual project.  You do not need to complete all of the tasks, but the tasks you do complete should be an accurate
reflection of your capability and effort.  You may discuss ideas in general with other students,
but writing code must be done by yourself.  No exceptions.   You must not give any other student a copy of your code in any form. – and you must not receive code from any other source (friends, students, AI language models, etc.) in any form.  There are absolutely NO EXCEPTIONS to this rule.
Please follow this advice while working on the project – the penalties for academic misconduct (which include your name being recorded on the misconduct register for the duration of your     degree, and/or a period of suspension from Engineering or expulsion from the University) are    simply not worth the risk.

Task One: “Let’s design a box!”                                                                                           (10 marks)Before we start developing the “Boxed In” game, let’s design a simple text-version of a box.   A box should be rectangular, and it should have some marking at the exact center position, so that the person pushing the box knows where to push!
For this task, you must define a function called MakeBox() which takes three inputs: a string     into which the characters will be stored, the width of the box (an integer), and the height of the  box (also an integer).   The MakeBox() function should generate a string representing the box.  A box will simply be represented as a rectangle where the hash character (‘#’) is used to denote
the edges.  In addition, the exact center of the box must be denoted using the character  ‘X’ (to help the person push the box in the correct place).
If the width and height of the box are both odd numbers, then there will be a single center
position which can be denoted with a single ‘X’ .  If the width and the height are both even
numbers, then the center position will have to be denoted with a small square of four  ‘X’
characters.  If only one of the width or height is an odd number, and the other is an even number, then two ‘X’ characters will be needed to denote the center position.   The examples below illustrate these three possibilities:
Note: the length of the output string will be exactly (width + 1) * height characters.  This is
because there is a single new line character appearing at the end of each line (including the last line).
For Task One, you must define a function called MakeBox():
void MakeBox(char *design, int width, int height)
You can assume that both width and height will be at least  1.  Note, the smallest box size for
which you will need to include the center position is 3 (if the width or height is 2 or less, it is not possible to include the center position so there will be no ‘X’ characters in the string in that case).
To illustrate how this function should work, consider the examples below: Example:char box1[1000] = {0}; char box2[1000] = {0}; char box3[1000] = {0};
MakeBox(box1, 12, 5);  MakeBox(box2, 15, 15); MakeBox(box3, 4, 4);printf("Box 1 = \n%s\n", box1); printf("Box 2 = \n%s\n", box2); printf("Box 3 = \n%s\n", box3);
printf("Checking string lengths = %d %d %d\n", strlen(box1),strlen(box2), strlen(box3));
Expected output:
Box 1 =
############ #            # #    XX    # #            # ############
Box 2 =
############### #             # #             # #             # #             # #             # #             # #      X       # #             # #             # #             # #             # #             # #             # ###############
Box 3 = ####
#XX# #XX# ####
Checking string lengths = 65 240 20
Note: the string lengths are exactly (width + 1) * height
Task Two: “Let’s see the warehouse!”                                                                                 (10 marks)
Let’s now move on to the “Boxed In” game.  The first thing we need to do is display the
warehouse.  The locations of the walls, the empty spaces on the floor, the person pushing the boxes, the targets, and the boxes will be represented using a two-dimensional array (of type   int). Two pre-defined constants are provided which specify the size of this array:
#define ROWS 9 #define COLS 8
These constants determine the number of rows and columns in the 2-dimensional array.  You do not need to define these constants yourself when submitting a function for marking – they will    always be defined for you.  You can simply use “ROWS” and “COLS” in your program (and in  your function prototype declarations).
For this task, you should write a function that prints to the screen the game board represented by the two-dimensional array.
Each value in the underlying array will be an integer between 0 – 6 (inclusive).   The following    six constants are provided to indicate what is represented by each value, and these constants will always be defined for you – you do not need to define these yourself:
#define SPACE 0 #define WALL 1
#define TARGET 2 #define BOX 3
#define BOX_ON_TARGET 4 #define PERSON 5
#define PERSON_ON_TARGET 6
In the example above, all values (except for PERSON_ON_TARGET) are illustrated.  In
particular, note that when a box is not on a target (i.e. BOX) it is displayed as a capital ‘o’:  ‘O’ . However, when a box is on top of a target cell (i.e. BOX_ON_TARGET) then it is displayed as an ‘@’ character.
The person is always displayed as an ‘X’, regardless of whether or not they are on a target.  In other words, the values PERSON and PERSON_ON_TARGET will always be shown as ‘X’ .
For Task Two, you must define a function called PrintRoom():
void PrintRoom(int room[ROWS][COLS])
which takes a 2-dimensional array of integers as input.  The function should display the corresponding game area for the “Boxed In” game.To illustrate how this function should work, consider the example below (in this case, you can assume that the constants ROWS and COLS are set to 9 and 8 respectively, and that the other  constants shown above have been defined):
void TestPrintRoom(void) {
int room[ROWS][COLS] =
{{0,0,1,1,1,1,1,0},  {1,1,1,0,0,0,1,0},  {1,2,5,3,0,0,1,0},  {1,1,1,0,3,2,1,0},  {1,2,1,1,3,0,1,0},  {1,0,1,0,2,0,1,1},  {1,3,0,4,3,3,2,1},  {1,0,0,0,2,0,0,1},  {1,1,1,1,1,1,1,1}};
PrintRoom(room); }
If you have defined the PrintRoom() function correctly, the output from this code would be as follows:
#####  ###   #  #*XO  #  ### O*#  #*##O #  # # * ## #O @OO*# #   *  # ########
Here is one 代 写ENGGEN 131 – Semester Two – 2024 C Programming Project
代做程序编程语言more example.  This time the constants ROWS and COLS have both been set to  10:
void TestPrintRoom(void) {
int room[ROWS][COLS] =
{{0,0,1,1,1,1,1,0,0,0},
{1,1,1,0,0,6,1,0,0,0},  {1,0,0,3,2,0,1,1,0,0},  {1,0,0,2,3,2,0,1,0,0},  {1,1,1,0,3,3,0,1,0,0},  {0,0,1,0,0,0,1,1,0,0},  {0,0,1,1,1,1,1,1,1,1},  {0,0,1,1,1,0,0,1,1,1},  {0,0,1,1,1,0,0,0,1,1},  {0,0,1,1,1,0,0,0,0,1}};
PrintRoom(room); }
If you have defined the PrintRoom() function correctly, the output from this code would be as follows:
#####  ###  X#  #  O* ## #  *O* #
### OO #
#   ##
######## ###  ### ###   ## ###    #
Notes:
.     In writing your solution to this task, you should make use of the pre-defined constants (e.g. SPACE, WALL, TARGET, …) described earlier.
.     Each line should end with a single new line character.  There should be no extra space characters printed on the ends of lines.
Task Three: “Configuring the room”                                                                                   (10 marks)
In order to play the game using different configurations of the puzzle, we will want to be able to initialize the two-dimensional array in different ways.
One convenient format to represent a configuration of the warehouse would be a string (consisting of characters between ‘0’ and ‘6’) as follows:
char layout[] = "0011111011100010125300101110321
01211301010102011130433211000200111111111";
For Task Three, you should write a function which takes two inputs: the two-dimensional array (representing the warehouse) and a string in the format shown above.  This function should
initialise the two-dimensional array to store the corresponding integer values.
void InitialiseRoom(int room[ROWS][COLS], char *layout)To illustrate how this function should work, consider the example below (in this case, you can  assume that the constants ROWS and COLS are set to 5 and 7 respectively, and that Task Two has been completed):
void TestInitialiseRoom(void) {
char layout[] = "11111111000001105230110000011111111"; int room[ROWS][COLS];
InitialiseRoom(room, layout); PrintRoom(room);
}
If you have defined the  InitialiseRoom() function correctly, the output from this code would be as follows:####### #      # # X*O # #      # #######
Please note: you cannot assume that the string passed as input to the function is the correct
length (i.e. the number of characters may not be equal to the product of ROWS and COLS).   If
the number of characters in the string is less than the number of elements in the two-dimensional array, then any uninitialized array elements should be set to WALL (i.e.  1).  If the number of
characters in the string is greater than the number of elements in the two-dimensional array, then  you must take care to only assign the appropriate number of characters from the string, and to not overwrite any memory outside the bounds of the array.
For example, consider this case where ROWS and COLS are set to 5 and 7 respectively, and the number of characters in the string is less than the number of elements in the two-dimensional
array:
void TestInitialiseRoom(void) {
char layout[] = "11111111000"; int room[ROWS][COLS];
InitialiseRoom(room, layout); PrintRoom(room);
}
In this case, the output should be:####### #   ### ####### ####### #######

Task Four: “Where are you?”                                                                                                (10 marks)

It will be useful to be able to locate the person in the warehouse.  For example, if the player
attempts to move the person, we will need to find where the person is located in order to update their position correctly.  For this task, you must write a function called LocatePerson():
void LocatePerson(int room[ROWS][COLS], int *row, int *col)
which takes three inputs: the configuration of the warehouse, a pointer to an integer for storing  the row position of the person, and a pointer to an integer for storing the column position of the
person.  Note, the location of the person is always represented as either PERSON or PERSON_ON_TARGET.
To illustrate how this function should work, consider the example below (in this case, you can assume that the constants ROWS and COLS are set to 10 and 10 respectively):
void TestLocatePerson(void) {
char layout[] = "001111100011100510001003
2011001002320100111043010  0001000110000111110000011 00000000110000000011110000";
int room[ROWS][COLS]; int row, col;
InitialiseRoom(room, layout); PrintRoom(room);
LocatePerson(room, row, col);
printf("The person is located at (%d, %d)\n", row, col); }
If you have defined the LocatePerson() function correctly, the output would be:
#####  ###  X#  #  O* ## #  *O* # ### @O #
#   ## #####  ##
##
####
The person is located at (1, 5)


Task Five: “Get moving”                                                                                                        (10 marks)
It is time to implement the movement of the person in the warehouse.  The player will control the movement using the ‘w’,  ‘a’, ‘s’ and ‘d’ keys on the keyboard (corresponding to up, left, down
and right).  These keys are commonly used to control a character’s movement in computer
games.  In addition to updating the position of the player, it will also be useful to keep track of the list of moves that the player has made since the beginning of the game.
For this task, you need to define a function called MakeMove().   The MakeMove() function will take three inputs: the two-dimensional array (representing the warehouse), a characterrepresenting the direction key that was pressed by the player (either ‘w’, ‘a’,  ‘s’ or ‘d’), and a string that will be used to keep track of the sequence of moves that the person makes as they   move throughout the warehouse.
For Task Five, you can assume that the warehouse will only contain walls and empty spaces.
There will be no boxes in the warehouse for the marking of Task Five.  You can also assume
that it will not be possible for the player to move outside the bounds of the two-dimensional
array (i.e. you can assume that the warehouse will be configured such that the player is
completely enclosed within the walls, and they should not be allowed to move through those walls).  The rules for moving are as follows:
1)   if there is a space in front of the person in the direction of movement, they should move to that empty position
2)   the person cannot move if there is a wall in front of them (if an invalid move is provided, it should be ignored and the array will simply not be updated, nor will the list of moves)
You should define the MakeMove() function as follows:
void MakeMove(int room[ROWS][COLS], char move, char *allMoves)
To illustrate how this function should work, consider the example below (in this case, you can assume that the constants ROWS and COLS are set to 6 and 6 respectively):
void TestMove(void) {
char layout[] = "111111100001100001100501100001111111";
char moves[100] = {0}; int room[ROWS][COLS];
InitialiseRoom(room, layout);

PrintRoom(room);
MakeMove(room, 'w', moves); PrintRoom(room);
printf("Person moved: %s", moves); }
If you have defined the MakeMove() function correctly, the output would be:###### #    # #    # #  X # #    # ###### ###### #    # #  X # #    # #    # ######
Person moved: w0
Notice that when the warehouse was first printed, the person was at location (3, 3).   After the    MakeMove() function has executed (with an input move of ‘w’, or up), when the warehouse is printed a second time, the person is at location (2, 3).
The third input to the MakeMove() function is a string.  This string is used to record the moves    that the person makes in the warehouse.  For now, every time the player moves, you should add    two characters to this string: (1) the direction of movement; and (2) the number zero (‘0’).  Later, once boxes are introduced to the warehouse, this second number will be used to keep track of
whether or not a box was moved when the player moved.
Here is another example:
In this resulting state (see the figure on right above), a downward move (‘s’) would be illegal
because there is a wall preventing the person from moving.  If an illegal move is provided as
input to the function, it should be ignored (i.e. the state of the array, and list of moves, should not change).
Here is one last example which illustrates multiple moves being made.
void TestMove(void) {
char layout[] = "111111100001100001100501100001111111"; char moves[100] = {0};
int room[ROWS][COLS];
InitialiseRoom(room, layout);

PrintRoom(room);
MakeMove(room, 'w', moves); PrintRoom(room);MakeMove(room, 'a', moves); MakeMove(room, 'a', moves); MakeMove(room, 's', moves); MakeMove(room, 'a', moves); MakeMove(room, 'a', moves); PrintRoom(room);
printf("Person moved: %s", moves); }
This time, the output is as follows (note that the final two attempted moves are not recorded, and do not affect the location of the person, because they are illegal):###### #    # #    # #  X # #    # ###### ###### #    # #  X # #    # #    # ###### ###### #    # #    # #X   # #    # ######
Person moved: w0a0a0s0



         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
