---
toc: true
layout: post
description: Working with Data Structures and manipulating data.
categories: []
title: Sorting Algorithms
---


```python
import random

numbers = []
for i in range(1000):
    numbers.append(random.randint(0,1000))
print("Random List")
print(numbers)
```

    Random List
    [575, 698, 687, 758, 915, 12, 554, 223, 143, 55, 549, 122, 985, 754, 573, 369, 925, 455, 215, 177, 272, 374, 119, 152, 643, 899, 386, 798, 440, 417, 523, 226, 880, 155, 212, 430, 824, 892, 412, 17, 432, 630, 949, 953, 33, 266, 601, 84, 186, 628, 890, 696, 160, 296, 606, 201, 345, 145, 593, 462, 446, 448, 112, 726, 568, 360, 568, 118, 81, 962, 376, 932, 889, 761, 663, 71, 282, 456, 772, 123, 551, 461, 319, 397, 665, 864, 262, 604, 270, 866, 809, 115, 779, 220, 713, 164, 968, 532, 474, 399, 884, 467, 577, 971, 663, 201, 660, 669, 413, 959, 401, 919, 111, 133, 960, 651, 885, 570, 659, 418, 303, 957, 878, 977, 889, 253, 753, 143, 384, 15, 160, 704, 280, 634, 888, 177, 387, 595, 474, 216, 178, 845, 91, 432, 321, 713, 406, 298, 548, 496, 967, 244, 381, 40, 429, 80, 765, 949, 513, 45, 613, 843, 745, 352, 376, 209, 910, 995, 267, 776, 676, 759, 785, 567, 77, 854, 91, 83, 977, 508, 835, 442, 598, 622, 473, 389, 878, 6, 426, 749, 884, 521, 811, 196, 749, 689, 995, 388, 504, 113, 275, 597, 653, 547, 999, 934, 929, 817, 124, 685, 93, 155, 208, 334, 69, 856, 856, 618, 43, 211, 462, 821, 604, 64, 302, 583, 83, 158, 46, 509, 671, 495, 93, 825, 876, 392, 644, 128, 298, 601, 472, 215, 388, 825, 328, 780, 906, 910, 136, 391, 839, 879, 135, 149, 742, 996, 697, 456, 764, 28, 869, 355, 905, 381, 614, 186, 883, 754, 911, 266, 266, 401, 92, 54, 485, 722, 31, 130, 314, 23, 673, 594, 284, 903, 860, 777, 811, 167, 626, 166, 281, 634, 82, 449, 193, 380, 542, 640, 680, 636, 605, 694, 787, 157, 234, 546, 945, 751, 427, 312, 155, 933, 102, 931, 537, 307, 80, 98, 471, 752, 860, 598, 757, 235, 978, 936, 324, 664, 812, 617, 10, 953, 921, 496, 10, 177, 10, 755, 646, 875, 65, 751, 518, 967, 119, 722, 999, 694, 739, 344, 311, 973, 392, 678, 24, 634, 490, 890, 603, 105, 565, 662, 618, 86, 609, 233, 654, 513, 793, 122, 700, 836, 626, 5, 307, 282, 539, 503, 714, 693, 478, 606, 809, 298, 369, 412, 19, 747, 101, 641, 278, 84, 638, 675, 884, 463, 680, 705, 3, 985, 759, 997, 779, 85, 751, 615, 513, 139, 64, 656, 346, 306, 283, 180, 161, 880, 294, 356, 910, 282, 188, 383, 871, 255, 94, 294, 688, 575, 464, 72, 426, 120, 841, 676, 315, 211, 463, 460, 581, 623, 89, 562, 177, 355, 607, 496, 69, 185, 915, 454, 720, 891, 115, 724, 326, 204, 66, 372, 747, 648, 254, 284, 104, 243, 59, 428, 2, 193, 202, 109, 329, 379, 44, 15, 639, 942, 967, 803, 559, 74, 407, 803, 195, 111, 362, 552, 266, 353, 504, 524, 706, 251, 802, 68, 497, 15, 151, 747, 693, 523, 285, 733, 692, 788, 51, 280, 943, 550, 317, 504, 822, 35, 982, 203, 473, 636, 848, 223, 327, 202, 923, 954, 610, 127, 707, 272, 259, 705, 242, 17, 488, 77, 584, 63, 864, 545, 84, 773, 555, 4, 172, 695, 630, 33, 925, 98, 836, 437, 136, 846, 552, 374, 278, 424, 505, 770, 855, 232, 868, 715, 127, 864, 438, 786, 216, 322, 653, 914, 53, 250, 510, 266, 621, 617, 38, 888, 488, 965, 250, 252, 749, 816, 968, 198, 86, 720, 818, 329, 447, 537, 654, 620, 660, 919, 467, 919, 710, 877, 234, 682, 52, 909, 221, 227, 378, 771, 622, 305, 696, 222, 1000, 520, 346, 558, 150, 577, 791, 409, 913, 340, 133, 545, 505, 582, 671, 691, 160, 166, 782, 541, 734, 33, 264, 805, 561, 314, 62, 115, 439, 595, 629, 32, 784, 322, 744, 731, 819, 233, 648, 74, 167, 292, 617, 332, 565, 812, 246, 183, 217, 728, 434, 93, 136, 342, 255, 640, 219, 32, 967, 253, 755, 578, 315, 313, 13, 510, 841, 652, 609, 586, 989, 837, 23, 970, 904, 119, 37, 991, 842, 180, 734, 99, 907, 949, 112, 130, 666, 140, 951, 897, 158, 894, 699, 56, 247, 662, 244, 709, 840, 22, 997, 673, 136, 795, 229, 628, 920, 766, 249, 384, 906, 734, 251, 991, 574, 307, 639, 947, 544, 645, 49, 357, 798, 416, 859, 817, 645, 340, 883, 709, 640, 78, 832, 407, 394, 448, 173, 94, 343, 693, 181, 974, 590, 196, 303, 322, 290, 284, 10, 583, 742, 748, 346, 924, 772, 91, 823, 507, 577, 724, 263, 774, 316, 673, 5, 673, 107, 555, 136, 230, 882, 341, 277, 447, 870, 304, 26, 517, 733, 904, 165, 314, 750, 488, 452, 726, 509, 909, 718, 207, 211, 417, 871, 87, 689, 928, 734, 187, 482, 27, 830, 464, 57, 206, 743, 620, 104, 606, 457, 824, 563, 46, 485, 362, 92, 801, 493, 331, 851, 83, 124, 599, 623, 932, 538, 37, 800, 444, 340, 594, 7, 336, 594, 929, 596, 71, 48, 839, 630, 516, 761, 34, 397, 49, 165, 632, 265, 504, 129, 739, 451, 503, 982, 273, 758, 43, 731, 912, 435, 621, 112, 960, 681, 472, 591, 98, 824, 16, 815, 304, 949, 186, 331, 50, 359, 983, 674, 539, 172, 710, 903, 571, 908, 77, 918, 244, 351, 122, 58, 109, 590, 481, 255, 937, 893, 257, 548, 159, 271, 961, 899, 671, 774, 131, 770, 446, 975, 457, 253, 105, 755, 382, 165, 992, 758, 860, 223, 501, 445, 389, 699, 223, 104, 8, 570, 702, 219, 257, 468, 47, 715, 480, 268, 661, 314, 258, 458, 426, 721, 137, 557, 321, 105, 25, 511, 84, 675, 688, 835, 238, 517, 255, 191, 431, 805, 557, 989, 995, 466, 296, 108, 520, 229, 873, 205, 370, 912, 380, 488, 533, 828, 725, 52, 198, 887, 228, 95, 167, 471, 806, 619, 938, 954, 135, 303, 931, 143, 892, 772, 870]


# Warm Up

> Discuss with a partner... 
What are some strategies you would use to sort this list? (Don't worry about writing code for now)
- There are a few ways to sort the list. A very basic one would be to just compare each number to the one after it and if the one next is smaller. Then you could repeat this until all of the numbers are in the right spot. 

# Explore

Get into groups of 3

We will be focusing on 4 algorithms today.

We will look at the first one together, Bubble Sort

![](images/bubble-sort.png)

What is happening with this sort?

In your groups you will each choose to be an expert on a sorting algorithm. Merge, Selection, and Insertion.
Take about 5 minutes to read about your algorithm (Geek for Geeks linked below) and be ready to explain it to your other group members. 

[Merge](https://www.geeksforgeeks.org/merge-sort/#)

[Selection](https://www.geeksforgeeks.org/selection-sort/)

[Insertion](https://www.geeksforgeeks.org/insertion-sort/)

## Practice

[75, 17, 46, 80, 67, 45, 69, 79, 40, 0]

How would you sort this list with... 
- Bubble Sort
- Selection Sort
> I would use selection sort because it would switch 0 and 75, which would sort the list faster. 

[88, 39, 53, 39, 58, 43, 74, 81, 71, 51]

How would you sort this list with... 
- Merge Sort
- Insertion Sort
> I would use insertion sort because it has a better time complexity. 


# Sorting Words
> Sorting strings works in the same way as integers. Using your expertise algorithm, sort the following list of random words.


```python
import nltk
import random
from nltk.corpus import words
nltk.download('words')  # Download the word list (only required once)
english_words = words.words()

def new_words():
    # You can now use the 'english_words' list in your code
    random_words = []
    for i in range(10):
        random_words.append(english_words[random.randint(0,len(english_words))])
    return random_words
        

print("Random List")
print(new_words())
```

    [nltk_data] Downloading package words to
    [nltk_data]     /Users/tobyleeder/nltk_data...


    Random List
    ['wisehearted', 'rebring', 'postclassic', 'overflowing', 'expressional', 'hydrophiloid', 'Trentepohliaceae', 'billfold', 'revetment', 'windclothes']


    [nltk_data]   Unzipping corpora/words.zip.


## Bubble Sort Poopcorn Hack
> Mortensen did this hack in class.


```python
words = new_words()
print(words)
def bubbleSort(list):
    n = len(list) - 1  # list are indexed 0 to n-1, len is n
    
    # Traverse through list with i index
    for i in range(n):
        swapped = False  # optimize code, so it exits if now swaps on inner loop

        # Inner traversal using j index
        for j in range(n-i):  # n-i as positions on right are in order in bubble
 
            # Swap if the element KeyN is greater KeyN1
            keyN = list[j]
            keyN1 = list[j+1]
            if keyN > keyN1:
                swapped = True
                list[j], list[j + 1] = list[j + 1], list[j]  # single line swap
         
        if not swapped:  # if no swaps on inner pass, list is sorted
            return  # exit function
        
bubbleSort(words)
print(words)
```

    ['semihyperbolical', 'samesome', 'paradoxidian', 'pyruline', 'gangliocyte', 'reckoning', 'intertubular', 'copelate', 'cered', 'amyloid']
    ['amyloid', 'cered', 'copelate', 'gangliocyte', 'intertubular', 'paradoxidian', 'pyruline', 'reckoning', 'samesome', 'semihyperbolical']


## Selection Sort Poopcorn Hack
> Mortensen did this hack in class.


```python
words = new_words()
print(words)
def selectionSort(list):
    n = len(list)  # length is n
    
    # List is traversed from index 0 to n-1, n elements
    for i in range(n):
        smallI = i  # small index is captured
        smallV = list[i]

        # Inner traversal looks at elements after i
        for j in range(i+1, n):
            # Save reference if less
            keyV = list[j]
            if keyV < smallV:
                smallI = j  # small index is replaced
                smallV = keyV
        
        # swap smallest to current i positon, sorting left to right
        list[i], list[smallI] = list[smallI], list[i]  # single line swap 
        
selectionSort(words)
print(words)
```

    ['ainoi', 'accipient', 'marvelry', 'rampageously', 'unpalatial', 'diaminogen', 'Pacht', 'tweak', 'faddism', 'elegant']
    ['Pacht', 'accipient', 'ainoi', 'diaminogen', 'elegant', 'faddism', 'marvelry', 'rampageously', 'tweak', 'unpalatial']


## Discuss 
Answer the following with your group.

- When should you use each algorithm? What makes an algorithm the right choice?
- Given the following lists...
    - [0, 2, 6, 4, 8, 10]
    - [Elephant, Banana, Cat, Dog, Apple]
    - [29, 13, 83, 47, 32, 78, 100, 60, 65, 15, 24, 9, 40, 68, 53, 8, 90, 58, 39, 32, 34, 91, 74, 94, 49, 87, 34, 87, 23, 17, 27, 2, 38, 58, 84, 15, 9, 46, 74, 40, 44, 8, 55, 28, 81, 92, 81, 88, 53, 38, 19, 21, 9, 54, 21, 67, 3, 41, 3, 74, 13, 71, 70, 45, 5, 36, 80, 64, 97, 86, 73, 74, 94, 79, 49, 32, 20, 68, 64, 69, 1, 77, 31, 56, 100, 80, 48, 75, 85, 93, 67, 57, 26, 56, 43, 53, 59, 28, 67, 50]
Select the algorithm you believe is best for each, explain.

## HACKS
> Provided below is a Bubble Sort Algorithm sorting a list of dictionaries based off of selected key.

- Now it's time to do some coding...

- Run code and then research and answer these questions...
    - Is a list and/or dictionary in python considered a primitive or collection type?  Why?
    > Both lists and dictionaries are considered collection types, because of the ways that these are stored. 
    - Is the list passed into bubble sort "pass-by-value" or "pass-by-reference? Describe why in relation to output.
    > The list is passed into bubble sort by reference because in python, that's how a variable is passed into a function as an argument. 

- Implement new cell(s) and/or organize cells to do the following.
    - Create your own list
    - Use your expertise sorting algorithm (selection, insertion, merge). Note, I got my bubble sort from Geek for Geeks and made modifications. Each student in a group should have a unique algorithm.
    - Test your list with my bubble sort
    - Test my list with your new sort
    - Research analysis on sorting: comparisons, swaps, time.  Build this into your hacks.
    - Find a better way to print the data, key first, then other elements in viewable form.

Use the code below to help guide your adventure


```python
import time

def selectionSort(array):
    size = len(array)
    for ind in range(size):
        min_index = ind
 
        for j in range(ind + 1, size):
            # select the minimum element in every iteration
            if array[j] < array[min_index]:
                min_index = j
         # swapping the elements to sort the array
        (array[ind], array[min_index]) = (array[min_index], array[ind])
    
    return array

randList = [575, 698, 687, 758, 915, 12, 554, 223, 143, 55, 549, 122, 985, 754, 573, 369, 925, 455, 215, 177, 272, 374, 119, 152, 643, 899, 386, 798, 440, 417, 523, 226, 880, 155, 212, 430, 824, 892, 412, 17, 432, 630, 949, 953, 33, 266, 601, 84, 186, 628, 890, 696, 160, 296, 606, 201, 345, 145, 593, 462, 446, 448, 112, 726, 568, 360, 568, 118, 81, 962, 376, 932, 889, 761, 663, 71, 282, 456, 772, 123, 551, 461, 319, 397, 665, 864, 262, 604, 270, 866, 809, 115, 779, 220, 713, 164, 968, 532, 474, 399, 884, 467, 577, 971, 663, 201, 660, 669, 413, 959, 401, 919, 111, 133, 960, 651, 885, 570, 659, 418, 303, 957, 878, 977, 889, 253, 753, 143, 384, 15, 160, 704, 280, 634, 888, 177, 387, 595, 474, 216, 178, 845, 91, 432, 321, 713, 406, 298, 548, 496, 967, 244, 381, 40, 429, 80, 765, 949, 513, 45, 613, 843, 745, 352, 376, 209, 910, 995, 267, 776, 676, 759, 785, 567, 77, 854, 91, 83, 977, 508, 835, 442, 598, 622, 473, 389, 878, 6, 426, 749, 884, 521, 811, 196, 749, 689, 995, 388, 504, 113, 275, 597, 653, 547, 999, 934, 929, 817, 124, 685, 93, 155, 208, 334, 69, 856, 856, 618, 43, 211, 462, 821, 604, 64, 302, 583, 83, 158, 46, 509, 671, 495, 93, 825, 876, 392, 644, 128, 298, 601, 472, 215, 388, 825, 328, 780, 906, 910, 136, 391, 839, 879, 135, 149, 742, 996, 697, 456, 764, 28, 869, 355, 905, 381, 614, 186, 883, 754, 911, 266, 266, 401, 92, 54, 485, 722, 31, 130, 314, 23, 673, 594, 284, 903, 860, 777, 811, 167, 626, 166, 281, 634, 82, 449, 193, 380, 542, 640, 680, 636, 605, 694, 787, 157, 234, 546, 945, 751, 427, 312, 155, 933, 102, 931, 537, 307, 80, 98, 471, 752, 860, 598, 757, 235, 978, 936, 324, 664, 812, 617, 10, 953, 921, 496, 10, 177, 10, 755, 646, 875, 65, 751, 518, 967, 119, 722, 999, 694, 739, 344, 311, 973, 392, 678, 24, 634, 490, 890, 603, 105, 565, 662, 618, 86, 609, 233, 654, 513, 793, 122, 700, 836, 626, 5, 307, 282, 539, 503, 714, 693, 478, 606, 809, 298, 369, 412, 19, 747, 101, 641, 278, 84, 638, 675, 884, 463, 680, 705, 3, 985, 759, 997, 779, 85, 751, 615, 513, 139, 64, 656, 346, 306, 283, 180, 161, 880, 294, 356, 910, 282, 188, 383, 871, 255, 94, 294, 688, 575, 464, 72, 426, 120, 841, 676, 315, 211, 463, 460, 581, 623, 89, 562, 177, 355, 607, 496, 69, 185, 915, 454, 720, 891, 115, 724, 326, 204, 66, 372, 747, 648, 254, 284, 104, 243, 59, 428, 2, 193, 202, 109, 329, 379, 44, 15, 639, 942, 967, 803, 559, 74, 407, 803, 195, 111, 362, 552, 266, 353, 504, 524, 706, 251, 802, 68, 497, 15, 151, 747, 693, 523, 285, 733, 692, 788, 51, 280, 943, 550, 317, 504, 822, 35, 982, 203, 473, 636, 848, 223, 327, 202, 923, 954, 610, 127, 707, 272, 259, 705, 242, 17, 488, 77, 584, 63, 864, 545, 84, 773, 555, 4, 172, 695, 630, 33, 925, 98, 836, 437, 136, 846, 552, 374, 278, 424, 505, 770, 855, 232, 868, 715, 127, 864, 438, 786, 216, 322, 653, 914, 53, 250, 510, 266, 621, 617, 38, 888, 488, 965, 250, 252, 749, 816, 968, 198, 86, 720, 818, 329, 447, 537, 654, 620, 660, 919, 467, 919, 710, 877, 234, 682, 52, 909, 221, 227, 378, 771, 622, 305, 696, 222, 1000, 520, 346, 558, 150, 577, 791, 409, 913, 340, 133, 545, 505, 582, 671, 691, 160, 166, 782, 541, 734, 33, 264, 805, 561, 314, 62, 115, 439, 595, 629, 32, 784, 322, 744, 731, 819, 233, 648, 74, 167, 292, 617, 332, 565, 812, 246, 183, 217, 728, 434, 93, 136, 342, 255, 640, 219, 32, 967, 253, 755, 578, 315, 313, 13, 510, 841, 652, 609, 586, 989, 837, 23, 970, 904, 119, 37, 991, 842, 180, 734, 99, 907, 949, 112, 130, 666, 140, 951, 897, 158, 894, 699, 56, 247, 662, 244, 709, 840, 22, 997, 673, 136, 795, 229, 628, 920, 766, 249, 384, 906, 734, 251, 991, 574, 307, 639, 947, 544, 645, 49, 357, 798, 416, 859, 817, 645, 340, 883, 709, 640, 78, 832, 407, 394, 448, 173, 94, 343, 693, 181, 974, 590, 196, 303, 322, 290, 284, 10, 583, 742, 748, 346, 924, 772, 91, 823, 507, 577, 724, 263, 774, 316, 673, 5, 673, 107, 555, 136, 230, 882, 341, 277, 447, 870, 304, 26, 517, 733, 904, 165, 314, 750, 488, 452, 726, 509, 909, 718, 207, 211, 417, 871, 87, 689, 928, 734, 187, 482, 27, 830, 464, 57, 206, 743, 620, 104, 606, 457, 824, 563, 46, 485, 362, 92, 801, 493, 331, 851, 83, 124, 599, 623, 932, 538, 37, 800, 444, 340, 594, 7, 336, 594, 929, 596, 71, 48, 839, 630, 516, 761, 34, 397, 49, 165, 632, 265, 504, 129, 739, 451, 503, 982, 273, 758, 43, 731, 912, 435, 621, 112, 960, 681, 472, 591, 98, 824, 16, 815, 304, 949, 186, 331, 50, 359, 983, 674, 539, 172, 710, 903, 571, 908, 77, 918, 244, 351, 122, 58, 109, 590, 481, 255, 937, 893, 257, 548, 159, 271, 961, 899, 671, 774, 131, 770, 446, 975, 457, 253, 105, 755, 382, 165, 992, 758, 860, 223, 501, 445, 389, 699, 223, 104, 8, 570, 702, 219, 257, 468, 47, 715, 480, 268, 661, 314, 258, 458, 426, 721, 137, 557, 321, 105, 25, 511, 84, 675, 688, 835, 238, 517, 255, 191, 431, 805, 557, 989, 995, 466, 296, 108, 520, 229, 873, 205, 370, 912, 380, 488, 533, 828, 725, 52, 198, 887, 228, 95, 167, 471, 806, 619, 938, 954, 135, 303, 931, 143, 892, 772, 870]

def bubbleSort2(arr):
    n = len(arr)

    swapped = False

    for i in range(n-1):
        for j in range(0, n-i-1):

            if arr[j] > arr[j + 1]:
                swapped = True
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
         
        if not swapped:
            print("bruh")
            return

selectStart = time.time()
selectionSort(randList)
selectTime = time.time() - selectStart

randList = [575, 698, 687, 758, 915, 12, 554, 223, 143, 55, 549, 122, 985, 754, 573, 369, 925, 455, 215, 177, 272, 374, 119, 152, 643, 899, 386, 798, 440, 417, 523, 226, 880, 155, 212, 430, 824, 892, 412, 17, 432, 630, 949, 953, 33, 266, 601, 84, 186, 628, 890, 696, 160, 296, 606, 201, 345, 145, 593, 462, 446, 448, 112, 726, 568, 360, 568, 118, 81, 962, 376, 932, 889, 761, 663, 71, 282, 456, 772, 123, 551, 461, 319, 397, 665, 864, 262, 604, 270, 866, 809, 115, 779, 220, 713, 164, 968, 532, 474, 399, 884, 467, 577, 971, 663, 201, 660, 669, 413, 959, 401, 919, 111, 133, 960, 651, 885, 570, 659, 418, 303, 957, 878, 977, 889, 253, 753, 143, 384, 15, 160, 704, 280, 634, 888, 177, 387, 595, 474, 216, 178, 845, 91, 432, 321, 713, 406, 298, 548, 496, 967, 244, 381, 40, 429, 80, 765, 949, 513, 45, 613, 843, 745, 352, 376, 209, 910, 995, 267, 776, 676, 759, 785, 567, 77, 854, 91, 83, 977, 508, 835, 442, 598, 622, 473, 389, 878, 6, 426, 749, 884, 521, 811, 196, 749, 689, 995, 388, 504, 113, 275, 597, 653, 547, 999, 934, 929, 817, 124, 685, 93, 155, 208, 334, 69, 856, 856, 618, 43, 211, 462, 821, 604, 64, 302, 583, 83, 158, 46, 509, 671, 495, 93, 825, 876, 392, 644, 128, 298, 601, 472, 215, 388, 825, 328, 780, 906, 910, 136, 391, 839, 879, 135, 149, 742, 996, 697, 456, 764, 28, 869, 355, 905, 381, 614, 186, 883, 754, 911, 266, 266, 401, 92, 54, 485, 722, 31, 130, 314, 23, 673, 594, 284, 903, 860, 777, 811, 167, 626, 166, 281, 634, 82, 449, 193, 380, 542, 640, 680, 636, 605, 694, 787, 157, 234, 546, 945, 751, 427, 312, 155, 933, 102, 931, 537, 307, 80, 98, 471, 752, 860, 598, 757, 235, 978, 936, 324, 664, 812, 617, 10, 953, 921, 496, 10, 177, 10, 755, 646, 875, 65, 751, 518, 967, 119, 722, 999, 694, 739, 344, 311, 973, 392, 678, 24, 634, 490, 890, 603, 105, 565, 662, 618, 86, 609, 233, 654, 513, 793, 122, 700, 836, 626, 5, 307, 282, 539, 503, 714, 693, 478, 606, 809, 298, 369, 412, 19, 747, 101, 641, 278, 84, 638, 675, 884, 463, 680, 705, 3, 985, 759, 997, 779, 85, 751, 615, 513, 139, 64, 656, 346, 306, 283, 180, 161, 880, 294, 356, 910, 282, 188, 383, 871, 255, 94, 294, 688, 575, 464, 72, 426, 120, 841, 676, 315, 211, 463, 460, 581, 623, 89, 562, 177, 355, 607, 496, 69, 185, 915, 454, 720, 891, 115, 724, 326, 204, 66, 372, 747, 648, 254, 284, 104, 243, 59, 428, 2, 193, 202, 109, 329, 379, 44, 15, 639, 942, 967, 803, 559, 74, 407, 803, 195, 111, 362, 552, 266, 353, 504, 524, 706, 251, 802, 68, 497, 15, 151, 747, 693, 523, 285, 733, 692, 788, 51, 280, 943, 550, 317, 504, 822, 35, 982, 203, 473, 636, 848, 223, 327, 202, 923, 954, 610, 127, 707, 272, 259, 705, 242, 17, 488, 77, 584, 63, 864, 545, 84, 773, 555, 4, 172, 695, 630, 33, 925, 98, 836, 437, 136, 846, 552, 374, 278, 424, 505, 770, 855, 232, 868, 715, 127, 864, 438, 786, 216, 322, 653, 914, 53, 250, 510, 266, 621, 617, 38, 888, 488, 965, 250, 252, 749, 816, 968, 198, 86, 720, 818, 329, 447, 537, 654, 620, 660, 919, 467, 919, 710, 877, 234, 682, 52, 909, 221, 227, 378, 771, 622, 305, 696, 222, 1000, 520, 346, 558, 150, 577, 791, 409, 913, 340, 133, 545, 505, 582, 671, 691, 160, 166, 782, 541, 734, 33, 264, 805, 561, 314, 62, 115, 439, 595, 629, 32, 784, 322, 744, 731, 819, 233, 648, 74, 167, 292, 617, 332, 565, 812, 246, 183, 217, 728, 434, 93, 136, 342, 255, 640, 219, 32, 967, 253, 755, 578, 315, 313, 13, 510, 841, 652, 609, 586, 989, 837, 23, 970, 904, 119, 37, 991, 842, 180, 734, 99, 907, 949, 112, 130, 666, 140, 951, 897, 158, 894, 699, 56, 247, 662, 244, 709, 840, 22, 997, 673, 136, 795, 229, 628, 920, 766, 249, 384, 906, 734, 251, 991, 574, 307, 639, 947, 544, 645, 49, 357, 798, 416, 859, 817, 645, 340, 883, 709, 640, 78, 832, 407, 394, 448, 173, 94, 343, 693, 181, 974, 590, 196, 303, 322, 290, 284, 10, 583, 742, 748, 346, 924, 772, 91, 823, 507, 577, 724, 263, 774, 316, 673, 5, 673, 107, 555, 136, 230, 882, 341, 277, 447, 870, 304, 26, 517, 733, 904, 165, 314, 750, 488, 452, 726, 509, 909, 718, 207, 211, 417, 871, 87, 689, 928, 734, 187, 482, 27, 830, 464, 57, 206, 743, 620, 104, 606, 457, 824, 563, 46, 485, 362, 92, 801, 493, 331, 851, 83, 124, 599, 623, 932, 538, 37, 800, 444, 340, 594, 7, 336, 594, 929, 596, 71, 48, 839, 630, 516, 761, 34, 397, 49, 165, 632, 265, 504, 129, 739, 451, 503, 982, 273, 758, 43, 731, 912, 435, 621, 112, 960, 681, 472, 591, 98, 824, 16, 815, 304, 949, 186, 331, 50, 359, 983, 674, 539, 172, 710, 903, 571, 908, 77, 918, 244, 351, 122, 58, 109, 590, 481, 255, 937, 893, 257, 548, 159, 271, 961, 899, 671, 774, 131, 770, 446, 975, 457, 253, 105, 755, 382, 165, 992, 758, 860, 223, 501, 445, 389, 699, 223, 104, 8, 570, 702, 219, 257, 468, 47, 715, 480, 268, 661, 314, 258, 458, 426, 721, 137, 557, 321, 105, 25, 511, 84, 675, 688, 835, 238, 517, 255, 191, 431, 805, 557, 989, 995, 466, 296, 108, 520, 229, 873, 205, 370, 912, 380, 488, 533, 828, 725, 52, 198, 887, 228, 95, 167, 471, 806, 619, 938, 954, 135, 303, 931, 143, 892, 772, 870]

bubbleStart = time.time()
bubbleSort2(randList)
bubbleTime = time.time() - bubbleStart

print("Select Time", selectTime)
print("Bubble Time", bubbleTime)

# Based on the prints above it looks like bubble takes twice as long as select sort


```

    Select Time 0.04163193702697754
    Bubble Time 0.0959169864654541



```python
"""
* Creator: Nighthawk Coding Society
Bubble Sort of a List of Dictionaries with optimizations, every key in row 0 is used to sort and resort list.
"""

# bubble sorts a list of dictionaries, base off of provided key
def bubbleSort(list, key):
    n = len(list) - 1  # list are indexed 0 to n-1, len is n
    
    # Traverse through list with i index
    for i in range(n):
        swapped = False  # optimize code, so it exits if now swaps on inner loop

        # Inner traversal using j index
        for j in range(n-i):  # n-i as positions on right are in order in bubble
 
            # Swap if the element KeyN is greater KeyN1
            keyN = list[j].get(key)
            keyN1 = list[j+1].get(key)
            if keyN > keyN1:
                swapped = True
                list[j], list[j + 1] = list[j + 1], list[j]  # single line swap
         
        if not swapped:  # if no swaps on inner pass, list is sorted
            return  # exit function
    

if __name__ == "__main__":
    # list/dictionary sample
    list_of_people = [
    {"name": "Risa", "age": 18, "city": "New York"},
    {"name": "John", "age": 63, "city": "Eugene"},
    {"name": "Shekar", "age": 18, "city": "San Francisco"},
    {"name": "Ryan", "age": 21, "city": "Los Angeles"}
    ]
    
    # assuming uniform keys, pick 1st row as source of keys
    key_row = list_of_people[0]

    # print list as defined
    print("Original")
    print(list_of_people)
    
    for key in key_row:  # finds each key in the row
        print(key)
        bubbleSort(list_of_people, key)  # sort list of people
        print(list_of_people)
```

    Original
    [{'name': 'Risa', 'age': 18, 'city': 'New York'}, {'name': 'John', 'age': 63, 'city': 'Eugene'}, {'name': 'Shekar', 'age': 18, 'city': 'San Francisco'}, {'name': 'Ryan', 'age': 21, 'city': 'Los Angeles'}]
    name
    [{'name': 'John', 'age': 63, 'city': 'Eugene'}, {'name': 'Risa', 'age': 18, 'city': 'New York'}, {'name': 'Ryan', 'age': 21, 'city': 'Los Angeles'}, {'name': 'Shekar', 'age': 18, 'city': 'San Francisco'}]
    age
    [{'name': 'Risa', 'age': 18, 'city': 'New York'}, {'name': 'Shekar', 'age': 18, 'city': 'San Francisco'}, {'name': 'Ryan', 'age': 21, 'city': 'Los Angeles'}, {'name': 'John', 'age': 63, 'city': 'Eugene'}]
    city
    [{'name': 'John', 'age': 63, 'city': 'Eugene'}, {'name': 'Ryan', 'age': 21, 'city': 'Los Angeles'}, {'name': 'Risa', 'age': 18, 'city': 'New York'}, {'name': 'Shekar', 'age': 18, 'city': 'San Francisco'}]

