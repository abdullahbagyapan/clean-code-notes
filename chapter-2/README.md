# Chapter 2 - Meaningful Names

Names are everywhere in software. We name our variables, our functions, our arguments,
classes, and packages.

What follows are some simple rules for creating good names.

### Use Intention-Revealing Names

The name of a variable, function, or class, should answer all the big questions.
It should tell you <b><i>why it exists, what it does, and how it is used</i></b>.

If a name requires a comment, then the name <b>does not</b> reveal its intent.

```java
int d; // elapsed time in days
```

We should choose a name that specifies what is being measured and the unit of that measurement:

```java
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModification;
int fileAgeInDays;
```

Choosing names that reveal intent can make it much easier to understand and change code.
What is the purpose of this code? 

```java
public List<int[]> getThem() {
    List<int[]> list1 = new ArrayList<int[]>();
    for (int[] x : theList)
        if (x[0] == 4)
        list1.add(x);
    return list1;
}
```

Why is it hard to tell what this code is doing?

The problem isn’t the simplicity of the code but the <b>implicity</b> of the code.
The code implicitly requires that we know the answers to questions such as:


- What kinds of things are in theList?
- What is the significance of the zeroth subscript of an item in theList?
- What is the significance of the value 4?
- How would I use the list being returned?

```java
public List<int[]> getFlaggedCells() {
    List<int[]> flaggedCells = new ArrayList<int[]>();
    for (int[] cell : gameBoard)
        if (cell[STATUS_VALUE] == FLAGGED)
        flaggedCells.add(cell);
    return flaggedCells;
}
```

Notice that the simplicity of the code has not changed. But the code has become much more explicit.

With these simple name changes, it’s not difficult to understand what’s going on. This is the <b><i>power of choosing good names</i></b>.

### Avoid Disinformation

We should avoid words whose entrenched meanings vary from our intended meaning.

Beware of using names which vary in small ways.

```
XYZControllerForEfficientHandlingOfStrings
XYZControllerForEfficientStorageOfStrings 
```

The words have frightfully similar shapes.

A truly awful example of disinformative names would be the use of lower-case L or uppercase O as variable names.

```java
int a = l;
if ( O == l )
    a = O1;
else
    l = 01;
```

### Make Meaningful Distinctions

Noise words are <b>redundant</b>.
The word variable should never appear in a variable name.

```java
public static void copyChars(char a1[], char a2[]) {
    for (int i = 0; i < a1.length; i++) {
        a2[i] = a1[i];
    }
}
```

They are noninformative,they provide no clue to the author’s intention.
This function reads much better when source and destination are used for the argument names.

> Note: There is nothing wrong with using prefix conventions like '<i>a</i>' and '<i>the</i>' so long as they make a meaningful distinction.

The problem comes in when you decide to call a variable '<i>theZork</i>' because you already have another variable named '<i>zork</i>'.

```java
getActiveAccount();
getActiveAccounts();
getActiveAccountInfo();
```

How are the programmers in this project supposed to know which of these functions to call?

In the absence of specific conventions,
- The variable '<i>moneyAmount</i>' is indistinguishable from '<i>money</i>',
- '<i>customerInfo</i>' is indistinguishable from '<i>customer</i>',
- '<i>accountData</i>' is indistinguishable from '<i>account</i>',
- '<i>theMessage</i>' is indistinguishable from '<i>message</i>'. 