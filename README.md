Download Link: https://assignmentchef.com/product/solved-cpsc2150-project-2-tic-tac-toe
<br>
For this assignment we will continue to work on our Extended Tic-Tac-Toe  game, but we will be adding new requirements. The old requirements are still required, unless they are replaced by a requirement in this prompt.

<strong>New Requirements</strong>

<ul>

 <li>At the start of each new game the user will be able to provide the number of rows, columns and the number of markers in a row needed to win for the game. These parameters should be passed to the GameBoard class in the constructor. The maximum number of rows and columns for all GameBoards is 100, and the maximum number needed to win will be 25 for all GameBoards. The minimum number or rows, columns, and tokens in a row needed to win are all 3. java must still use a 2D array to represent it’s game board, but it’s ok if most of the array is ignored for smaller boards.

  <ul>

   <li>The user should not be able to provide a “number needed to win” that is larger than the number of rows or the number of columns</li>

   <li>The constructors for the game boards should take parameters in the order of rows, columns, and number to win</li>

  </ul></li>

 <li>Note that the formatting of the displayed board has changed to allow double digit numbers.</li>

 <li>If the users decide to play again, they will be able to change the size and number to win settings from the previous game.</li>

 <li>The program must validate the number of rows, columns, and needed to win that are provided by the user.</li>

 <li>At the start of each new game, the users will be able to specify the number of players for each game. They must enter at least 2 players, and at most 10 players. Note that IGameBoard does not care about the number of players at all, this is just a requirement of GameScreen</li>

 <li>After selecting the number of players, each player will be able to pick what character will represent them in the game. You can assume they will always enter just a character. Always convert the character to upper case. Each player must have their own unique character, and the game should not allow a player to pick a character that is already taken.

  <ul>

   <li>Note: if you have a string, you can call the charAt(0) method to get the first character. If your string only has one character, this is an easy and safe way to convert a string that was provided by user (nextLine() returns a string) and convert it to a character.</li>

   <li>Note: The List interface has a method called contains(Object obj) that will return true if the obj already exists in the List.</li>

  </ul></li>

 <li>At the start of each new game the players can choose whether they want a fast implementation or a memory efficient implementation. The game must check to make sure they entered either f, F, m, or M as a choice at this option.

  <ul>

   <li>Remember, if you use == to compare strings, you will check to see if the memory location is the same. Use the equals() method to check if they have the same abstract value.</li>

  </ul></li>

 <li>The number of players and their characters can change if they choose to start a new game.</li>

 <li>The choice of the fast or memory efficient implementation can be changed if they choose to start a new game.</li>

 <li>Our game must now have two different implementations of our IGameBoard interface o We already have our fast implementation which uses a 2D array. However, we will now be checking to make sure the implementation is efficient. So you should not be checking the entire row if you are looking for the horizontal win, you should be checking starting at the last position played.

  <ul>

   <li>Our memory efficient implementation is detailed below.</li>

   <li>Our GameScreen class should be able to easily switch between these two implementations. Remember, programming to the interface allows for the code to be the same except for the call to the constructor. You should not have essentially 2 different versions of the main function (one for each implementation) but one main function that has an if statement to call the appropriate constructor of your</li>

  </ul></li>

</ul>

IGameBoard object.




<strong>New Implementation </strong>

You will need to provide a new class called GameBoardMem that will extend AbsGameBoard which implements the IGameBoard interface. This new implementation will be slower, but more memory efficient.

To represent the game board you will use a Map.  Map is another Generic collection that uses a key – value pair. The key field of our Map will be a Character that represents the player, so each player will get their own entry in the Map. The Value associated with that player will be a List of BoardPositions that the player occupies on the board. If a player has not placed a token yet, then there will be no key or List in the Map to represent that player. Do NOT create a key for the blank space with a List of BoardPositions that are blank. The memory efficiency of this implementation comes from the fact that and empty board does not use up any space in memory. When a player adds their first token, then you add the key for that player and a List with that BoardPosition in it. As more tokens are added by a player, you add the BoardPosition onto the List for that player.        There is a video available on Canvas that discusses some Maps in more detail, and discusses how to declare and work with Maps. It describes many useful methods in the Map class as well.                While this may seem like a lot of work to create this new implementation, remember that your new implementation only needs to provide code for your primary methods, and the constructor. All of your secondary methods can be handled by default implementations in the interface, and toString is provided by AbsGameBoard. However, we will want to override one of the default implementations.     While this representation of a game board will be more memory efficient, it will be slower. With a 2D array, if we want to know what is in row 2, column 3, we can access that position in the array directly. However, we can no longer do that with our data representation in a Map. If we want to know what’s at row 2, column 3, we need to look in each key-value entry in the Map. If row 2, column 3 exists in the List (our value in the map) then the player who’s character is the key is at that position. If the position does not exist in any list, then the space is blank.

Now consider if instead of wanting to know what’s at position 2, 3 we just need to know if ‘X’ is at position 2, 3. Now instead of needing to check every List, we just need to check the List that has

‘X’ as it’s key. This is why our <em>interface</em> has the two separate methods whatsAtPos and isPlayerAt. When we were using a 2D array, they were implemented in the same way, but now that we are using a Map, the implementations are quite different. Our interface didn’t care about how it was implemented, we just knew that asking “what’s at this position?” and “is X at this position?” are different questions, and should be asked in different ways. This means we can override the default isPlayerAt method in our GameBoardMem implementation to make a more efficient implementation for that particular data structure. After doing so, make sure your code is making sure to call isPlayerAt when it is appropriate to do so, and not just rely on whatsAtPos.




<strong>Example Board </strong>

Consider the following Board:




| 0| 1| 2| 3| 4| 5| 6| 7| 8|

0|  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |

2|  |  |  |X |X |X |O |  |  |

3|  |  |  |  |T |  |T |  |  |

4|  |  |  |O |O |T |  |  |  |

5|  |  |  |  |  |  |W |  |  |

6|  |  |  |  |  |  |W |  |  |

7|  |  |  |  |  |  |  |  |  |




In our implementation from Homework 2, this board would be represented in memory as an 8 by 8 2D array of characters. Blank spaces in the board are represented by that position in the array containing a ‘ ‘ character. While we can quickly access any place on the board by jumping to that index in the array, our board takes a lot of memory because it is always storing 64 characters. Now consider what this board would look like in our memory efficient implementation.

In our memory efficient implementation we would have a Map&lt;Character,

List&lt;BoardPostion&gt;&gt; with our key being the player that represents a character. We currently only have 4 players (X, O, T, W) so those will be the only keys in our Map. For our 4 players, we will have keys and matching Lists. So if we asked our Map to return the value for key W it would return a List of BoardPositions (Row, Column) with &lt;(5,6), (6,6)&gt; in it. As player W places more markers, we can add more BoardPostions to the List.




Our Key Value pairs for this board would be as follows:

<table width="623">

 <tbody>

  <tr>

   <td width="312">Key</td>

   <td width="312">Value</td>

  </tr>

  <tr>

   <td width="312">X</td>

   <td width="312">&lt;(2,3), (2,4), (2,5)&gt;</td>

  </tr>

  <tr>

   <td width="312">O</td>

   <td width="312">&lt;(4,3), (4,4), (2,6)&gt;</td>

  </tr>

  <tr>

   <td width="312">T</td>

   <td width="312">&lt;(3,4), (4,5), (3,6)&gt;</td>

  </tr>

  <tr>

   <td width="312">W</td>

   <td width="312">&lt;(5,6), (6,6)&gt;</td>

  </tr>

 </tbody>

</table>










<strong>Contracts and Comments</strong>

All methods (except for the main) must have preconditions and post-conditions specified in the

Javadoc contracts. All methods (except for main) must also have the params and returns specified in the Javadoc comments as well. You must include a complete interface specification in IGameBoard, and write the contracts not included in the interface specification in the GameBoard class. You must provide correspondences and invariants in your GameBoard class.

You code must be well commented. The Javadoc comments will only be enough for very simple methods. Remember, your comments will help the grader understand what you are trying to do in your code. If they don’t understand what you are trying to do, you will lose points.




<strong>Input and Output</strong>

Remember, the TAs will be grading this assignment using scripts as much as possible. You can make this easier on them by using the correct format for input and output. If their scripts don’t work because you do not follow the input and output standards a few things will happen:

<ol>

 <li>Grading and feedback will take longer</li>

 <li>The TA will be mad at you, which you never want when they are grading your assignment</li>

 <li>The TA will have to spend more time manually using and inspecting your code, which means they are more likely to find minor issues and deduct points.</li>

 <li>You will lose points for not following the instructions.</li>

</ol>




This is what my input and output looks like. Notice how it handles more than 10 columns, Notice that row and column are asked for separately and in that order.




<strong>General Notes: </strong>

<ul>

 <li>If it does not compile, it is a zero. Make sure it will compile on Unix</li>

 <li>Name your package cpsc2150.extendedTicTacToe</li>

 <li>Remember our “best practices” that we’ve discussed in class. Use good variables, avoid magic numbers, etc.</li>

 <li>Hide as much information as possible. Remember, you don’t want a house with an absurd number of doors.</li>

 <li>Start early. You have time to work on this assignment, but you will need time to work on it. – Starting early means more opportunities to go to TA or instructor office hours for help – This is an individual assignment; you may not work with a partner.</li>

 <li>There are other ways you could use maps to implement the IGameBoard interface, but I am asking for a very specific representation. You must use that representation</li>

 <li>The project report should be one organized document</li>

 <li>You must include a makefile with your program. We should be able to run your program by unzipping your directory and using the make and make run commands.</li>

 <li>Remember, this class is about more than just functioning code. Your design and quality of code is very important. Remember the best practices we are discussing in class. Your code should be easy to change and maintain. You should not be using magic numbers. You should be considering Separation of Concerns, Information Hiding, Encapsulation, and</li>

</ul>

Programming to the interface when designing your code. You should also be following the idea and rules of design by contract.

<ul>

 <li>A new game should always start with player 1</li>

 <li>Your code should be well formatted and consistently formatted. This includes things like good variable names and consistent indenting style.</li>

 <li>You should not have any dead code in your program. Dead code is commented out code.</li>

 <li>Your code must be able to run on the school Unix machines. Usually there is no issue with moving code from intelliJ to Unix, but some times there can be issues, especially if you try to import any uncommon java libraries.</li>

 <li>Code that does not compile will receive a 0.</li>

 <li>Your UML Diagrams must be made electronically. I recommend the freely available program draw.io, but if you have another diagramming tool your prefer feel free to use that.</li>

 <li>While you need to validate all input from the user, you can assume that they are entering numbers or characters when appropriate. You do not need to check to see that they entered 6 instead of “six.”</li>

 <li>Your code needs to more than just functioning, it needs to be efficient.</li>

 <li>The List interface has a method called contains. It will be very helpful. Note: it relies on the equals method being properly overridden.</li>

 <li>IGameBoard does not know how many players are playing the game, and it does not care.</li>

</ul>




<strong>The Project Report </strong>

Along with your code you must submit a well formatted report with the following parts:

<h1>Requirements Analysis</h1>

Fully analyze the requirements of this program. Express all functional requirements as user stories. Remember to list all non-functional requirements of the program as well.

<h1>Design</h1>

Create a UML class diagram for each class and interface in the program. Also create UML Activity diagrams for every method in your GameScreen class and every method in your GameBoard or GameBoardMem class . If a method is defined as a default method in the interface, you need to update the diagrams to remove any mention of the 2D array or other private data of the GameBoard class, and instead refer to primary methods. If a method is provided only as a default method in the interface you only need to provide an Activity Diagram for the default method, you do not need to include the diagram for each implementation as well. If you provide a default method in the interface, but override it in the implementation you need to include an activity diagram for each method. Your diagram for toString should not reference private data since it will exist in the abstract class.

<h1>Deployment</h1>

Provide instructions about how your program can be compiled and run. Since you are required to submit a makefile with your code, this should be pretty simple.




<strong>Checklist:</strong>

Use this Checklist to ensure you are completing your assignment. Note: this list does not cover all possible reasons you could miss points, but should cover a majority of them. I am not intentionally leaving anything out, but I am constantly surprised by some of the submissions we see that are wildly off the mark. For example, I am not listing “Does my program play Tic Tac Toe?” but that does not mean that if you turn in a program that plays Checkers you can say “But it wasn’t on the checklist!” The only complete list that would guarantee that no points would be lost would be an incredibly detailed and complete set of instructions that told you exactly what code to type, which wouldn’t be much of an assignment.

<ul>

 <li>Can I set the size of my game board?</li>

 <li>Can I set the number needed in a row to win?</li>

 <li>Does my game have 2 players? – Do my classes have invariants?</li>

 <li>Did I add an interface?</li>

 <li>Is my interface specification complete?</li>

 <li>Did I add correspondences?</li>

 <li>Does my game allow for players to play again?</li>

 <li>When players choose to play again can they change the settings of the game?</li>

 <li>Are my methods reasonably efficient? You don’t need to take this to the extreme, but obvious inefficiencies should be corrected.</li>

 <li>Does my game take turns with the players?</li>

 <li>Does my game correctly identify wins?</li>

 <li>Does my game correctly identify tie games?</li>

 <li>Does my game run without crashing?</li>

 <li>Does my game validate user input?</li>

 <li>Did I protect my data by keeping it private, except for public static final variables?</li>

 <li>Did I encapsulate my data and functionality and include them in the correct classes?</li>

 <li>Did I follow Design By Contract?</li>

 <li>Did I provide contracts for my methods?</li>

 <li>Did I comment my code?</li>

 <li>Did I provide Javadoc comments for each method?</li>

 <li>Did I avoid using magic numbers?</li>

 <li>Did I use good variable names?</li>

 <li>Did I follow best practices?</li>

 <li>Did I remove “Dead Code.” Dead Code is old code that is commented out.</li>

 <li>Did I make any additional helper functions I created private?</li>

 <li>Did I use the static keyword correctly?</li>

 <li>Did I express all functional requirements as user stories? – Did I create my activity diagrams for all methods?</li>

 <li>Did I create a class diagram for each class and interface?</li>

 <li>Did I provide a working make file?</li>

 <li>Does my code compile and run on Unix?</li>

 <li>Is my program written in Java?</li>

 <li>Does my output look like the provided examples?</li>

</ul>




<strong>Sample Input and Output: </strong>

How many players?

12

Must be 10 players or fewer How many players?

1

Must be at least 2 players How many players?

4

Enter the character to represent player 1 x

Enter the character to represent player 2 x

X is already taken as a player token! Enter the character to represent player 2 o

Enter the character to represent player 3 t

Enter the character to represent player 4

F

How many rows?

0

Rows must be between 3 and 100

How many rows?

150

Rows must be between 3 and 100

How many rows?

12

How many columns?

0

Columns must be between 3 and 100

How many columns?

150

Columns must be between 3 and 100

How many columns?

15

How many in a row to win? 5

Would you like a Fast Game (F/f) or a Memory Efficient Game (M/m? g

Please enter F or M

Would you like a Fast Game (F/f) or a Memory Efficient Game (M/m? m

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

5|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

6|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

7|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player X Please enter your ROW

4

Player X Please enter your COLUMN

7

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |  |  |X |  |  |  |  |  |  |  |

5|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

6|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

7|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player O Please enter your ROW

6

Player O Please enter your COLUMN

2

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |  |  |X |  |  |  |  |  |  |  |

5|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

6|  |  |O |  |  |  |  |  |  |  |  |  |  |  |  |

7|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player T Please enter your ROW

13

Player T Please enter your COLUMN

17

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |  |  |X |  |  |  |  |  |  |  |

5|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

6|  |  |O |  |  |  |  |  |  |  |  |  |  |  |  |

7|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




That space is unavailable, please pick again

Player T Please enter your ROW

8

Player T Please enter your COLUMN

5

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |  |  |X |  |  |  |  |  |  |  |

5|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

6|  |  |O |  |  |  |  |  |  |  |  |  |  |  |  |

7|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player F Please enter your ROW

8

Player F Please enter your COLUMN

8

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |  |  |X |  |  |  |  |  |  |  |

5|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

6|  |  |O |  |  |  |  |  |  |  |  |  |  |  |  |

7|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player X Please enter your ROW

4

Player X Please enter your COLUMN

6

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |  |X |X |  |  |  |  |  |  |  |

5|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

6|  |  |O |  |  |  |  |  |  |  |  |  |  |  |  |

7|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player O Please enter your ROW

6

Player O Please enter your COLUMN

3

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |  |X |X |  |  |  |  |  |  |  |

5|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

6|  |  |O |O |  |  |  |  |  |  |  |  |  |  |  |

7|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | 11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player T Please enter your ROW

6

Player T Please enter your COLUMN

5

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |  |X |X |  |  |  |  |  |  |  |

5|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

6|  |  |O |O |  |T |  |  |  |  |  |  |  |  |  |

7|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player F Please enter your ROW

4

Player F Please enter your COLUMN

8

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |  |X |X |F |  |  |  |  |  |  |

5|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

6|  |  |O |O |  |T |  |  |  |  |  |  |  |  |  |

7|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player X Please enter your ROW

6

Player X Please enter your COLUMN

1

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |  |X |X |F |  |  |  |  |  |  |  5|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

6|  |X |O |O |  |T |  |  |  |  |  |  |  |  |  |

7|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player O Please enter your ROW

4

Player O Please enter your COLUMN

5

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |O |X |X |F |  |  |  |  |  |  |

5|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

6|  |X |O |O |  |T |  |  |  |  |  |  |  |  |  |

7|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player T Please enter your ROW

10

Player T Please enter your COLUMN

5

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |O |X |X |F |  |  |  |  |  |  |

5|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

6|  |X |O |O |  |T |  |  |  |  |  |  |  |  |  |

7|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player F Please enter your ROW

5

Player F Please enter your COLUMN

8

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |O |X |X |F |  |  |  |  |  |  |

5|  |  |  |  |  |  |  |  |F |  |  |  |  |  |  |

6|  |X |O |O |  |T |  |  |  |  |  |  |  |  |  |

7|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player X Please enter your ROW

6

Player X Please enter your COLUMN

8

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |O |X |X |F |  |  |  |  |  |  |

5|  |  |  |  |  |  |  |  |F |  |  |  |  |  |  |

6|  |X |O |O |  |T |  |  |X |  |  |  |  |  |  |

7|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player O Please enter your ROW

5

Player O Please enter your COLUMN

4

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |O |X |X |F |  |  |  |  |  |  |

5|  |  |  |  |O |  |  |  |F |  |  |  |  |  |  |

6|  |X |O |O |  |T |  |  |X |  |  |  |  |  |  |

7|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  | 11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player T Please enter your ROW

7

Player T Please enter your COLUMN

5

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |O |X |X |F |  |  |  |  |  |  |

5|  |  |  |  |O |  |  |  |F |  |  |  |  |  |  |

6|  |X |O |O |  |T |  |  |X |  |  |  |  |  |  |

7|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player F Please enter your ROW

9

Player F Please enter your COLUMN

5

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |O |X |X |F |  |  |  |  |  |  |

5|  |  |  |  |O |  |  |  |F |  |  |  |  |  |  |

6|  |X |O |O |  |T |  |  |X |  |  |  |  |  |  |

7|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |F |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player X Please enter your ROW

3

Player X Please enter your COLUMN

5

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |X |  |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |O |X |X |F |  |  |  |  |  |  |  5|  |  |  |  |O |  |  |  |F |  |  |  |  |  |  |

6|  |X |O |O |  |T |  |  |X |  |  |  |  |  |  |

7|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |F |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player O Please enter your ROW

3

Player O Please enter your COLUMN

6

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |X |O |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |O |X |X |F |  |  |  |  |  |  |

5|  |  |  |  |O |  |  |  |F |  |  |  |  |  |  |

6|  |X |O |O |  |T |  |  |X |  |  |  |  |  |  |

7|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |F |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player T Please enter your ROW

5

Player T Please enter your COLUMN

7

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |X |O |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |O |X |X |F |  |  |  |  |  |  |

5|  |  |  |  |O |  |  |T |F |  |  |  |  |  |  |

6|  |X |O |O |  |T |  |  |X |  |  |  |  |  |  |

7|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |F |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player F Please enter your ROW

7

Player F Please enter your COLUMN

2

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|  0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |X |O |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |O |X |X |F |  |  |  |  |  |  |

5|  |  |  |  |O |  |  |T |F |  |  |  |  |  |  |

6|  |X |O |O |  |T |  |  |X |  |  |  |  |  |  |

7|  |  |F |  |  |T |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |F |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player X Please enter your ROW

2

Player X Please enter your COLUMN

4

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |X |  |  |  |  |  |  |  |  |  |  |

3|  |  |  |  |  |X |O |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |O |X |X |F |  |  |  |  |  |  |

5|  |  |  |  |O |  |  |T |F |  |  |  |  |  |  |

6|  |X |O |O |  |T |  |  |X |  |  |  |  |  |  |

7|  |  |F |  |  |T |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |F |  |  |  |  |  |  |  |  |  |

10|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  |

11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Player O Please enter your ROW

2

Player O Please enter your COLUMN

7

Player O wins!

0| 1| 2| 3| 4| 5| 6| 7| 8| 9|10|11|12|13|14|

0|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

1|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

2|  |  |  |  |X |  |  |O |  |  |  |  |  |  |  |

3|  |  |  |  |  |X |O |  |  |  |  |  |  |  |  |

4|  |  |  |  |  |O |X |X |F |  |  |  |  |  |  |

5|  |  |  |  |O |  |  |T |F |  |  |  |  |  |  |

6|  |X |O |O |  |T |  |  |X |  |  |  |  |  |  |

7|  |  |F |  |  |T |  |  |  |  |  |  |  |  |  |

8|  |  |  |  |  |T |  |  |F |  |  |  |  |  |  |

9|  |  |  |  |  |F |  |  |  |  |  |  |  |  |  | 10|  |  |  |  |  |T |  |  |  |  |  |  |  |  |  | 11|  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |




Would you like to play again? Y/N

y

How many players?

3

Enter the character to represent player 1 w

Enter the character to represent player 2 y

Enter the character to represent player 3 r

How many rows?

5

How many columns?

5

How many in a row to win?

3

Would you like a Fast Game (F/f) or a Memory Efficient Game (M/m? f

0| 1| 2| 3| 4|

0|  |  |  |  |  |

1|  |  |  |  |  |

2|  |  |  |  |  |

3|  |  |  |  |  |

4|  |  |  |  |  |




Player W Please enter your ROW

…


