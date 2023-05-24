---
toc: true
layout: post
description: Several 2D arrays and Animations hacks are provided to further learn iteration and data in Python.  The objective is to build a stronger foundation in iteration and data.  Also, it is important to see concepts like printing color and moving objects in terminal, prior to moving to frontend development with JavaScript.
categories: []
title: Python 2D Iteration and Animation
---

## 2D Programming and Resources
> There are lots of applications for 2D data.  Common terms in 2D are tabular data, row/columns, matrix, etc.  Nested iterative loops are often used to find or discover each cell in a 2D array.
- 2D samples and challenges in Jupyter.  wget link: https://raw.githubusercontent.com/nighthawkcoders/APCSP/master/_notebooks/2023-05-16-DS-arrays_lab.ipynb
- Mario animations in JS, these are markdown code examples.
    - Assets  [metadata yml](https://raw.githubusercontent.com/nighthawkcoders/APCSP/master/_data/mario_metadata.yml), wget and place in _data directory;  [sprite](https://github.com/nighthawkcoders/APCSP/blob/master/images/mario_animation.png), download and place in images directory 
    - Code to interact with Sprite Animations [runtime](https://nighthawkcoders.github.io/APCSP/frontend/mario), [wget code](https://raw.githubusercontent.com/nighthawkcoders/APCSP/master/_posts/2022-07-19-PBL-mario-sprite.md)
    - Game starters [runtime](https://nighthawkcoders.github.io/APCSP/frontend/mario2), [wget imperative code](https://raw.githubusercontent.com/nighthawkcoders/APCSP/master/_posts/2022-07-19-PBL-mario-animation.md), [wget oop code](https://github.com/nighthawkcoders/APCSP/blob/master/_posts/2022-07-19-PBL-mario-animation-oop.md)

### Python 2D array
> Example of pre-populating 2D array and printing using 3 different styles
- Candy Challenge: print a christmas tree and trunk


```python
christmasTree = [
    [" ", " ", " ", " ", "^", " ", " ", " ", " ",],
    [" ", " ", " ", '/', "|", "\\", " ", " ", " ",],
    [" ", " ", ' /', "", "|", "", "\\", " ", " ",],
    [" ", '  /', "", "", "|", "", "", "\\", " ",],
    [' ', " ", "^", "^", "|", "^", "^","", " ",],
    [' ', " ", " ", " ", "|", " ", " "," ", " ",]
]

print_matrix1(christmasTree)
```

    Classic nested loops using ij indexes
            ^         
          / | \       
         /  |  \     
        /   |   \   
        ^ ^ | ^ ^    
            |         



```python
"""
* Creator: Nighthawk Coding Society
2D arrays
"""

# Classic nested loops using ij indexes, this shows 2 dimensions
def print_matrix1(matrix):
    print("Classic nested loops using ij indexes")
    for i in range(len(matrix)):  # outer loop (i), built on length of matrix (rows)
        for j in range(len(matrix[i])):  # inner loop (j), built on length of items (columns)
            print(matrix[i][j], end=" ")  # [i][j] is 2D representation, end changes newline to space
        print()


# Enhanced nested for loops, row and col variables
def print_matrix2(matrix):
    print("Enhanced nested for loops")
    for row in matrix:  # short hand row iterator, index is not required
        for col in row:  # short hand column iterator
            print(col, end=" ")
        print()


# For loop with shortcut (*) row expansion
def print_matrix3(matrix):
    print("For loop with shortcut (*) row expansion")
    for row in matrix:
        print(*row)  # pythons has (*) that is one line expansion of row into columns


def test_matrices():
    # setup some text matrices
    keypad = [[1, 2, 3],
              [4, 5, 6],
              [7, 8, 9],
              [" ", 0, " "]]

    keyboard = [["`", 1, " ", 2, " ",3, " ",  4, " ", 5, " ", 6, " ", 7, " ", 8, " ", 9, " ", 0, " ", "-"," ", "="],
                [" ", " ", "Q", " ", "W", " ", "E", " ", "R", " ", "T", " ", "Y", " ", "U", " ", "I", " ", " ", "O", " ", "P", " ", "[", " ", "]", " ", "\\"],
                [" ", " ", " ", "A", " ", "S", " ", "D", " ", "F", " ", "G", " ", "H", " ", "J", " ", "K", " ", "L", " ", ";", " ", "'"],
                [" ", " ", " ", " ", "Z", " ", "X", " ", "C", " ", "V", " ", "B", " ", "N", " ", "M", " ", ",", " ", ".", " ", "/"]]

    numbers = [
            [0, 1], # binary
            [0, 1, 2, 3, 4, 5, 6, 7, 8, 9], # decimal
            [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, "A", "B", "C", "D", "E", "F"] # hexadecimal
            ]
    

    # pack into a list of matrices with titles
    matrices = [
        ["Keypad", keypad], 
        ["Keyboard", keyboard], 
        ["Number Systems", numbers]
    ]

    # loop 2D matrix with returning list in [key, value] arrangement
    for title, matrix in matrices:  # unpack title and matrix as variables
        
        # formatted message with concatenation
        print(title, len(matrix), "x", "~" + str(len(matrix[0])))  
        
        # use three different methods
        print_matrix1(matrix)
        print_matrix2(matrix)
        print_matrix3(matrix)
        # blank link in between
        print()


# tester section
if __name__ == "__main__":
    test_matrices()
```

    Keypad 4 x ~3
    Classic nested loops using ij indexes
    1 2 3 
    4 5 6 
    7 8 9 
      0   
    Enhanced nested for loops
    1 2 3 
    4 5 6 
    7 8 9 
      0   
    For loop with shortcut (*) row expansion
    1 2 3
    4 5 6
    7 8 9
      0  
    
    Keyboard 4 x ~24
    Classic nested loops using ij indexes
    ` 1   2   3   4   5   6   7   8   9   0   -   = 
        Q   W   E   R   T   Y   U   I     O   P   [   ]   \ 
          A   S   D   F   G   H   J   K   L   ;   ' 
            Z   X   C   V   B   N   M   ,   .   / 
    Enhanced nested for loops
    ` 1   2   3   4   5   6   7   8   9   0   -   = 
        Q   W   E   R   T   Y   U   I     O   P   [   ]   \ 
          A   S   D   F   G   H   J   K   L   ;   ' 
            Z   X   C   V   B   N   M   ,   .   / 
    For loop with shortcut (*) row expansion
    ` 1   2   3   4   5   6   7   8   9   0   -   =
        Q   W   E   R   T   Y   U   I     O   P   [   ]   \
          A   S   D   F   G   H   J   K   L   ;   '
            Z   X   C   V   B   N   M   ,   .   /
    
    Number Systems 3 x ~2
    Classic nested loops using ij indexes
    0 1 
    0 1 2 3 4 5 6 7 8 9 
    0 1 2 3 4 5 6 7 8 9 A B C D E F 
    Enhanced nested for loops
    0 1 
    0 1 2 3 4 5 6 7 8 9 
    0 1 2 3 4 5 6 7 8 9 A B C D E F 
    For loop with shortcut (*) row expansion
    0 1
    0 1 2 3 4 5 6 7 8 9
    0 1 2 3 4 5 6 7 8 9 A B C D E F
    


### JavaScript 2D array
> Example below populate a 2D array.  Key concepts are ij loop and assignments.  Observe the object that is created in console.  Learn the basics of iteration through 2D array in JavaScript.
- Candy challenge:  Work of pairs.  Create one of the Python examples (christmas tree, keyboard, ...). Use the element.append to output within the notebook.   As you work on JavaScript make sure your development enviornment is setup like JavaScript programmer.


```python
%%js

/*
* Creator: Nighthawk Coding Society
Construct a two-dimensional array in JS
*/

var arr2D = [];
var rows = 3;
var cols = 4;
 
// Loop to initialize 2D array elements
for (var i = 0; i < rows; i++) {
    arr2D[i]=[];
    for (var j = 0; j < cols; j++) {
        arr2D[i][j] = "r:" + i + "c:" + j;
    }
}
console.log(arr2D);
element.append(arr2D);

for (var i = 0; i < rows; i++){
    for (var j = 0; j < length; j++){
        console.log(arr2D[i][j]);
        console.log("\n")
        element.append(arr2D[i][j]); 
        element.append("\n")
    }
}
```


    <IPython.core.display.Javascript object>


## Monkey Jumpers Poem
> Here are some of the key parts of these arrays
- Build ASCII monkeys, 5 different monkeys using ASCII Art for the "Monkey Jumpers" countdown poem
- ANSII Color codes are added to each Monkey
- Candy Challenge: Print monkeys horizontally versus vertically.


```python
"""
 * Creator: Nighthawk Coding Society
 * Mini Lab Name: Hello Series, featuring Monkey Jumpers Poem
"""

import time # used for delay
from IPython.display import clear_output  # jupyter specific clear

def main():    
    # ANSI Color Codes
    Red = "\u001b[31m"
    Green = "\u001b[32m"
    Yellow = "\u001b[33m"
    Blue = "\u001b[34m"
    Magenta = "\u001b[35m"

    """ 2D array data assignment """
    monkeys = [
        [
            Red,
            "ʕง ͠° ͟ل͜ ͡°)ʔ ",  # [0][0] eyes
            "  \\_⏄_/  ",  # [0][1] chin
            "  --0--   ",  # [0][2] body
            "  ⎛   ⎞   "  # [0][3] legs
        ],
        [
            Green,
            " ʕ༼ ◕_◕ ༽ʔ ",  # [1][0]
            "  \\_⎏_/  ",
            "  ++1++  ",
            "   ⌋ ⌊   "
        ],
        [
            Yellow,
            " ʕ(▀ ⍡ ▀)ʔ",  # [2][0]
            "  \\_⎐_/ ",
            "  <-2->  ",
            "  〈  〉 "
        ],
        [
            Blue,
            "ʕ ͡° ͜ʖ ° ͡ʔ",  # [3][0]
            "  \\_⍾_/  ",
            "  ==3==  ",
            "  _/ \\_  "
        ],
        [
            Magenta,
            "  (◕‿◕✿) ",  # [4][0]
            "  \\_⍾_/ ",  # [4][1]
            "  ==4==  ",  # [4][2]
            "  _/ \\_ "  # [4][3]
        ]
    ]

    """ 2D array program logic """
    # cycles through 2D array backwards
    
    for i in range(len(monkeys), -1, -1):
        line = []
        clear_output(wait=True)
        
        print("Nursery Rhyme")  # identification message

        # this print statement shows current count of Monkeys
        # concatenation (+) of the loop variable and string to form a countdown message
        print(str(i) + " little monkeys jumping on the bed...")

        # cycle through monkeys that are left in poem countdown
        for row in range(i - 1, -1, -1):  # cycles through remaining monkeys in countdown

            # cycles through monkey part by part
            for col in range(len(monkeys[row])):
                # prints specific part of the monkey from the 2D cell
                try:
                    line[col] += ((monkeys[row][col] + "     "))
                except:
                    line.append((monkeys[row][col] + "     "))

            # this new line gives separation between stanza of poem
            
        for i in range(len(line)):
            print(line[i])
        time.sleep(2)

    # out of all the loops, prints finishing messages
    clear_output(wait=True)
    print("No more monkeys jumping on the bed")
    print("0000000000000000000000000000000000")
    print("             THE END              ")


if __name__ == "__main__":
    main()
```

    No more monkeys jumping on the bed
    0000000000000000000000000000000000
                 THE END              


## Animation, the Energetic versus Lazy Programmer methods
> Animation is done like the old Disney films, lots of little images put togehter.  In these examples we eliminate using a 2D array, but simulate int with a sequence of print statements.
- This 1st sequence is a lot of lines of code.
- The 2nd takes the lazy programmer method to do the same.
- Candy challenge: Make you own ASCII art animation.


```python
def guillotine1():
    print("   ____________")
    print("  |____________|_")
    print("   ||--------|| | _________")
    print("   ||- _     || |(HA ha ha!)")
    print("   ||    - _ || | ---------")
    print("   ||       -|| |     //")
    print("   ||        || O\    __")
    print("   ||        ||  \\  (..)")
    print("   ||        ||   \\_|  |_")
    print("   ||        ||    \  \/  )")
    print("   ||        ||     :    :|")
    print("   ||        ||     :    :|")
    print("   ||        ||     :====:O")
    print("   ||        ||     (    )")
    print("   ||__@@@@__||     | `' |")
    print("   || @|..|@ ||     | || |")
    print("   ||O@`=='@O||     | || |")
    print("   ||_@\/\/@_||     |_||_|")
    print(" ----------------   '_'`_`")
    print("/________________\----------\\")
    print("|   GUILLOTINE   |-----------|")
    print("|  OF CASTLE DE SADE         |")
    print("|____________________________|")

def guillotine2():
    print("   ____________")
    print("  |____________|_")
    print("   ||--------|| | _________")
    print("   ||        || |(HA ha ha!)")
    print("   ||- _     || | ---------")
    print("   ||    - _ || |     //")
    print("   ||       -|| O\    __")
    print("   ||        ||  \\  (..)")
    print("   ||        ||   \\_|  |_")
    print("   ||        ||    \  \/  )")
    print("   ||        ||     :    :|")
    print("   ||        ||     :    :|")
    print("   ||        ||     :====:O")
    print("   ||        ||     (    )")
    print("   ||__@@@@__||     | `' |")
    print("   || @|..|@ ||     | || |")
    print("   ||O@`=='@O||     | || |")
    print("   ||_@\/\/@_||     |_||_|")
    print(" ----------------   '_'`_`")
    print("/________________\----------\\")
    print("|   GUILLOTINE   |-----------|")
    print("|  OF CASTLE DE SADE         |")
    print("|____________________________|")

def guillotine3():
    print("   ____________")
    print("  |____________|_")
    print("   ||        || | _________")
    print("   ||--------|| |(HA ha ha!)")
    print("   ||        || | ---------")
    print("   ||- _     || |     //")
    print("   ||    - _ || O\    __")
    print("   ||       -||  \\  (..)")
    print("   ||        ||   \\_|  |_")
    print("   ||        ||    \  \/  )")
    print("   ||        ||     :    :|")
    print("   ||        ||     :    :|")
    print("   ||        ||     :====:O")
    print("   ||        ||     (    )")
    print("   ||__@@@@__||     | `' |")
    print("   || @|..|@ ||     | || |")
    print("   ||O@`=='@O||     | || |")
    print("   ||_@\/\/@_||     |_||_|")
    print(" ----------------   '_'`_`")
    print("/________________\----------\\")
    print("|   GUILLOTINE   |-----------|")
    print("|  OF CASTLE DE SADE         |")
    print("|____________________________|")

def guillotine4():
    print("   ____________")
    print("  |____________|_")
    print("   ||        || | _________")
    print("   ||        || |(HA ha ha!)")
    print("   ||--------|| | ---------")
    print("   ||        || |     //")
    print("   ||- _     || O\    __")
    print("   ||    - _ ||  \\  (..)")
    print("   ||       -||   \\_|  |_")
    print("   ||        ||    \  \/  )")
    print("   ||        ||     :    :|")
    print("   ||        ||     :    :|")
    print("   ||        ||     :====:O")
    print("   ||        ||     (    )")
    print("   ||__@@@@__||     | `' |")
    print("   || @|..|@ ||     | || |")
    print("   ||O@`=='@O||     | || |")
    print("   ||_@\/\/@_||     |_||_|")
    print(" ----------------   '_'`_`")
    print("/________________\----------\\")
    print("|   GUILLOTINE   |-----------|")
    print("|  OF CASTLE DE SADE         |")
    print("|____________________________|")

def guillotine5():
    print("   ____________")
    print("  |____________|_")
    print("   ||        || | _________")
    print("   ||        || |(HA ha ha!)")
    print("   ||        || | ---------")
    print("   ||--------|| |     //")
    print("   ||        || O\    __")
    print("   ||- _     ||  \\  (..)")
    print("   ||    - _ ||   \\_|  |_")
    print("   ||       -||    \  \/  )")
    print("   ||        ||     :    :|")
    print("   ||        ||     :    :|")
    print("   ||        ||     :====:O")
    print("   ||        ||     (    )")
    print("   ||__@@@@__||     | `' |")
    print("   || @|..|@ ||     | || |")
    print("   ||O@`=='@O||     | || |")
    print("   ||_@\/\/@_||     |_||_|")
    print(" ----------------   '_'`_`")
    print("/________________\----------\\")
    print("|   GUILLOTINE   |-----------|")
    print("|  OF CASTLE DE SADE         |")
    print("|____________________________|")

def guillotine6():
    print("   ____________")
    print("  |____________|_")
    print("   ||        || | _________")
    print("   ||        || |(HA ha ha!)")
    print("   ||        || | ---------")
    print("   ||        || |     //")
    print("   ||--------|| O\    __")
    print("   ||        ||  \\  (..)")
    print("   ||- _     ||   \\_|  |_")
    print("   ||    - _ ||    \  \/  )")
    print("   ||       -||     :    :|")
    print("   ||        ||     :    :|")
    print("   ||        ||     :====:O")
    print("   ||        ||     (    )")
    print("   ||__@@@@__||     | `' |")
    print("   || @|..|@ ||     | || |")
    print("   ||O@`=='@O||     | || |")
    print("   ||_@\/\/@_||     |_||_|")
    print(" ----------------   '_'`_`")
    print("/________________\----------\\")
    print("|   GUILLOTINE   |-----------|")
    print("|  OF CASTLE DE SADE         |")
    print("|____________________________|")

def guillotine7():
    print("   ____________")
    print("  |____________|_")
    print("   ||        || | _________")
    print("   ||        || |(HA ha ha!)")
    print("   ||        || | ---------")
    print("   ||        || |     //")
    print("   ||        || O\    __")
    print("   ||--------||  \\  (..)")
    print("   ||        ||   \\_|  |_")
    print("   ||- _     ||    \  \/  )")
    print("   ||    - _ ||     :    :|")
    print("   ||       -||     :    :|")
    print("   ||        ||     :====:O")
    print("   ||        ||     (    )")
    print("   ||__@@@@__||     | `' |")
    print("   || @|..|@ ||     | || |")
    print("   ||O@`=='@O||     | || |")
    print("   ||_@\/\/@_||     |_||_|")
    print(" ----------------   '_'`_`")
    print("/________________\----------\\")
    print("|   GUILLOTINE   |-----------|")
    print("|  OF CASTLE DE SADE         |")
    print("|____________________________|")

def guillotine8():
    print("   ____________")
    print("  |____________|_")
    print("   ||        || | _________")
    print("   ||        || |(HA ha ha!)")
    print("   ||        || | ---------")
    print("   ||        || |     //")
    print("   ||        || O\    __")
    print("   ||        ||  \\  (..)")
    print("   ||--------||   \\_|  |_")
    print("   ||        ||    \  \/  )")
    print("   ||- _     ||     :    :|")
    print("   ||    - _ ||     :    :|")
    print("   ||       -||     :====:O")
    print("   ||        ||     (    )")
    print("   ||__@@@@__||     | `' |")
    print("   || @|..|@ ||     | || |")
    print("   ||O@`=='@O||     | || |")
    print("   ||_@\/\/@_||     |_||_|")
    print(" ----------------   '_'`_`")
    print("/________________\----------\\")
    print("|   GUILLOTINE   |-----------|")
    print("|  OF CASTLE DE SADE         |")
    print("|____________________________|")

def guillotine9():
    print("   ____________")
    print("  |____________|_")
    print("   ||        || | _________")
    print("   ||        || |(HA ha ha!)")
    print("   ||        || | ---------")
    print("   ||        || |     //")
    print("   ||        || O\    __")
    print("   ||        ||  \\  (..)")
    print("   ||        ||   \\_|  |_")
    print("   ||--------||    \  \/  )")
    print("   ||        ||     :    :|")
    print("   ||- _     ||     :    :|")
    print("   ||    - _ ||     :====:O")
    print("   ||       -||     (    )")
    print("   ||__@@@@__||     | `' |")
    print("   || @|..|@ ||     | || |")
    print("   ||O@`=='@O||     | || |")
    print("   ||_@\/\/@_||     |_||_|")
    print(" ----------------   '_'`_`")
    print("/________________\----------\\")
    print("|   GUILLOTINE   |-----------|")
    print("|  OF CASTLE DE SADE         |")
    print("|____________________________|")

def guillotine10():
    print("   ____________")
    print("  |____________|_")
    print("   ||        || | _________")
    print("   ||        || |(HA ha ha!)")
    print("   ||        || | ---------")
    print("   ||        || |     //")
    print("   ||        || O\    __")
    print("   ||        ||  \\  (..)")
    print("   ||        ||   \\_|  |_")
    print("   ||        ||    \  \/  )")
    print("   ||--------||     :    :|")
    print("   ||        ||     :    :|")
    print("   ||- _     ||     :====:O")
    print("   ||    - _ ||     (    )")
    print("   ||__@@@@_-||     | `' |")
    print("   || @|..|@ ||     | || |")
    print("   ||O@`=='@O||     | || |")
    print("   ||_@\/\/@_||     |_||_|")
    print(" ----------------   '_'`_`")
    print("/________________\----------\\")
    print("|   GUILLOTINE   |-----------|")
    print("|  OF CASTLE DE SADE         |")
    print("|____________________________|")





guillotine1()
clear_output(wait=True)
time.sleep(.5)
guillotine2()
clear_output(wait=True)
time.sleep(.5)
guillotine3()
clear_output(wait=True)
time.sleep(.5)
guillotine4()
clear_output(wait=True)
time.sleep(.5)
guillotine5()
clear_output(wait=True)
time.sleep(.5)
guillotine6()
clear_output(wait=True)
time.sleep(.5)
guillotine7()
clear_output(wait=True)
time.sleep(.5)
guillotine8()
clear_output(wait=True)
time.sleep(.5)
guillotine9()
clear_output(wait=True)
time.sleep(.5)
guillotine10()

```

       ____________
      |____________|_
       ||        || | _________
       ||        || |(HA ha ha!)
       ||        || | ---------
       ||        || |     //
       ||        || O\    __
       ||        ||  \  (..)
       ||        ||   \_|  |_
       ||        ||    \  \/  )
       ||--------||     :    :|
       ||        ||     :    :|
       ||- _     ||     :====:O
       ||    - _ ||     (    )
       ||__@@@@_-||     | `' |
       || @|..|@ ||     | || |
       ||O@`=='@O||     | || |
       ||_@\/\/@_||     |_||_|
     ----------------   '_'`_`
    /________________\----------\
    |   GUILLOTINE   |-----------|
    |  OF CASTLE DE SADE         |
    |____________________________|



```python
"""
* Creator: Nighthawk Coding Society
Sailing Ship Animation (long method)
"""

import time # used for delay
from IPython.display import clear_output  # jupyter specific clear

# ANSI Color Codes
Color34 = "\u001b[34m"
Color37 = "\u001b[37m"


# As you can see, its not very optimal 
def ship1():
    print("    |\ ")
    print("    |/ ")
    print("\__ |__/ ")
    print(" \____/ ")
    print("\u001b[34m -------------------------------------------- \u001b[37m")


def ship2():
    print("      |\ ")
    print("      |/ ")
    print("  \__ |__/ ")
    print("   \____/ ")
    print("\u001b[34m ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ \u001b[37m")


def ship3():
    print("        |\ ")
    print("        |/ ")
    print("    \__ |__/ ")
    print("     \____/ ")
    print("\u001b[34m ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ \u001b[37m")


def ship4():
    print("          |\ ")
    print("          |/ ")
    print("      \__ |__/ ")
    print("       \____/ ")
    print("\u001b[34m ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ \u001b[37m")


def ship5():
    print("            |\ ")
    print("            |/ ")
    print("        \__ |__/ ")
    print("         \____/ ")
    print("\u001b[34m -------------------------------------------- \u001b[37m")


def ship6():
    print("              |\ ")
    print("              |/ ")
    print("          \__ |__/ ")
    print("           \____/ ")
    print("\u001b[34m ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ \u001b[37m")


def ship7():
    print("                |\ ")
    print("                |/ ")
    print("            \__ |__/ ")
    print("             \____/ ")
    print("\u001b[34m ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ \u001b[37m")


def ship8():
    print("                  |\ ")
    print("                  |/ ")
    print("              \__ |__/ ")
    print("               \____/ ")
    print("\u001b[34m -------------------------------------------- \u001b[37m")


def ship9():
    print("                    |\ ")
    print("                    |/ ")
    print("                \__ |__/ ")
    print("                 \____/ ")
    print("\u001b[34m ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ \u001b[37m")


def ship10():
    print("                      |\ ")
    print("                      |/ ")
    print("                  \__ |__/ ")
    print("                   \____/ ")
    print("\u001b[34m ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ \u001b[37m")


def ship11():
    print("                        |\ ")
    print("                        |/ ")
    print("                    \__ |__/ ")
    print("                     \____/ ")
    print("\u001b[34m -------------------------------------------- \u001b[37m")


def ship12():
    print("                          |\ ")
    print("                          |/ ")
    print("                      \__ |__/ ")
    print("                       \____/ ")
    print("\u001b[34m ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ \u001b[37m")


def ship13():
    print("                            |\ ")
    print("                            |/ ")
    print("                        \__ |__/ ")
    print("                         \____/ ")
    print("\u001b[34m ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ \u001b[37m")


def ship14():
    print("                              |\ ")
    print("                              |/ ")
    print("                          \__ |__/ ")
    print("                           \____/ ")
    print("\u001b[34m ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ \u001b[37m")


def ship15():
    print("                                |\ ")
    print("                                |/ ")
    print("                            \__ |__/ ")
    print("                             \____/ ")
    print("\u001b[34m -------------------------------------------- \u001b[37m")


def ship16():
    print("                                  |\ ")
    print("                                  |/ ")
    print("                              \__ |__/ ")
    print("                               \____/ ")
    print("\u001b[34m ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ \u001b[37m")


def ship17():
    print("                                    |\ ")
    print("                                    |/ ")
    print("                                \__ |__/ ")
    print("                                 \____/ ")
    print("\u001b[34m -------------------------------------------- \u001b[37m")


def ship18():
    print("                                      |\ ")
    print("                                      |/ ")
    print("                                  \__ |__/ ")
    print("                                   \____/ ")
    print("\u001b[34m ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ \u001b[37m")


def ship19():
    print("                                        |\ ")
    print("                                        |/ ")
    print("                                    \__ |__/ ")
    print("                                     \____/ ")
    print("\u001b[34m -------------------------------------------- \u001b[37m")


def ship20():
    print("                                          |\ ")
    print("                                          |/ ")
    print("                                      \__ |__/ ")
    print("                                       \____/ ")
    print("\u001b[34m -------------------------------------------- \u001b[37m")


clear_output(wait=True)
time.sleep(.1)
ship1()
time.sleep(.5)
clear_output(wait=True)
ship2()
time.sleep(.5)
clear_output(wait=True)
ship3()
time.sleep(.5)
clear_output(wait=True)
ship4()
time.sleep(.5)
clear_output(wait=True)
ship5()
time.sleep(.5)
clear_output(wait=True)
ship6()
time.sleep(.5)
clear_output(wait=True)
ship7()
time.sleep(.5)
clear_output(wait=True)
ship8()
time.sleep(.5)
clear_output(wait=True)
ship9()
time.sleep(.5)
clear_output(wait=True)
ship10()
time.sleep(.5)
clear_output(wait=True)
ship11()
time.sleep(.5)
clear_output(wait=True)
ship12()
time.sleep(.5)
clear_output(wait=True)
ship13()
time.sleep(.5)
clear_output(wait=True)
ship14()
time.sleep(.5)
clear_output(wait=True)
ship15()
time.sleep(.5)
clear_output(wait=True)
ship16()
time.sleep(.5)
clear_output(wait=True)
ship17()
time.sleep(.5)
clear_output(wait=True)
ship18()
time.sleep(.5)
clear_output(wait=True)
ship19()
time.sleep(.5)
clear_output(wait=True)
ship20()
time.sleep(.5)
```

                                              |\ 
                                              |/ 
                                          \__ |__/ 
                                           \____/ 
    [34m -------------------------------------------- [37m



```python
"""
* Creator: Nighthawk Coding Society
Sailing Ship Animation (programatic method)
"""

import time # used for delay
from IPython.display import clear_output  # jupyter specific clear


# ANSI Color Codes
OCEAN_COLOR = u"\u001B[34m\u001B[2D"
SHIP_COLOR = u"\u001B[35m\u001B[2D"
RESET_COLOR = u"\u001B[0m\u001B[2D"

def ship_print(position):  # print ship with colors and leading spaces according to position
    clear_output(wait=True)
    print(RESET_COLOR)
    
    sp = " " * position
    print(sp + "    |\   ")
    print(sp + "    |/   ")
    print(SHIP_COLOR, end="")
    print(sp + "\__ |__/ ")
    print(sp + " \____/  ")
    if position % 4 == 1 or position % 4 == 2:
        print(OCEAN_COLOR + "--"*32 + RESET_COLOR)
    else:
        print(OCEAN_COLOR + "~~"*32 + RESET_COLOR)


def ship():  # ship function, loop/controller for animation speed and times
    # loop control variables
    start = 0  # start at zero
    distance = 60  # how many times to repeat
    step = 1  # count by 2

    # loop purpose is to animate ship sailing
    for position in range(start, distance, step):
        ship_print(position)  # call to function with parameter
        time.sleep(.2)

        
ship() # activate/call ship function
```

    [0m[2D
                                                                   |\   
                                                                   |/   
    [35m[2D                                                           \__ |__/ 
                                                                \____/  
    [34m[2D~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~[0m[2D



```python

```
