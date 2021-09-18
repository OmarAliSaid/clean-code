
# Clean Code Book Summary ( By Robert C. Martin )

# Foreword 

In about 1951, a quality approach called Total Productive Maintenance (TPM) came on the Japanese scene. Its focus is on maintenance rather than on production. One of the major pillars of TPM is the set of so-called  **5S principles :**  

-   **_Seiri_**, or  **organization**  : Knowing where things are—using approaches such as suitable naming—is crucial. You think naming identifiers isn’t important? well it’s  **IMPORTANT**.
-   **_Seiton_**, or  **tidiness**  : _A place for everything, and everything in its place_. A piece of code should be where you expect to find it—and, if not, you should re-factor to get it there.
-   **_Seiso_**, or  **cleaning**  : Keep the workplace free of hanging wires, grease, scraps, and waste. what is the use of commented-out code lines that capture history or wishes for the future? Get rid of them.
-   **_Seiketsu_**, or  **standardization**: The group agrees about how to keep the workplace clean. they put standards ? Where do those standards come from? we will find that later on
-   **_Shutsuke_**, or  **discipline**  (_self_-discipline) : This means having the discipline to follow the practices and to frequently reflect on one’s work and be willing to change.


# Chapter 1 - Clean Code
### what does Bjarne Stroustrup says about clean code ?
I like my code to be elegant and efficient. The logic should be straightforward to make it hard for bugs to hide, the dependencies minimal to ease maintenance, error handling complete according to an articulated strategy, and per- formance close to optimal so as not to tempt people to make the code messy with unprinci- pled optimizations. Clean code does one thing well.
### How To Defend Your Clean Code Responsability Against Your Managers
what if you were a doctor and had a patient who demanded that you stop all the silly hand-washing in preparation for surgery because it was taking too much time?2 Clearly the patient is the boss; and yet the doctor should absolutely refuse to comply. Why? Because the doctor knows more than the patient about the risks of dis- ease and infection. It would be unprofessional (never mind criminal) for the doctor to comply with the patient.  
So too it is unprofessional for programmers to bend to the will of managers who don’t understand the risks of making messes.

# Chapter 2 - Meaningful Names

## 1 - Use Intention-Revealing Names
use names that actually reveals your intention of using that variable 
Say that we’re working in a mine sweeper game. We find that the board is a list of cells called `theList`. Let’s rename that to `gameBoard`.  
Each cell on the board is represented by a simple array. We further find that the zeroth subscript is the location of a status value and that a status value of 4 means “flagged.” Just by giving these concepts names we can improve the code considerably:With these simple name changes, it’s not difficult to understand what’s going on. This is the power of choosing good names.
#### BAD CODE
``` java
public List<int[]> getThem() {  
	List<int[]> list1 = new ArrayList<int[]>(); 
	for (int[] x : theList)
	if (x[0] == 4)
		list1.add(x);
	return list1;
}
```
#### GOOD CODE
``` java
public List<int[]> getFlaggedCells() {  
	List<int[]> flaggedCells = new ArrayList<int[]>(); 
	for (int[] cell : gameBoard)
		if (cell[STATUS_VALUE] == FLAGGED) 
			flaggedCells.add(cell);
	return flaggedCells; 
}
```
#### GREAT CODE
``` java
public List<Cell> getFlaggedCells() {  
	List<Cell> flaggedCells = new ArrayList<Cell>(); 
	for (Cell cell : gameBoard)
		if (cell.isFlagged()) 
			flaggedCells.add(cell);
	return flaggedCells; 
}
```
## 2 - Avoid Disinformation

Do not refer to a grouping of accounts as an `accountList` unless it’s actually a List. The word `list` means something specific to programmers. If the container holding the accounts is not actually a `List`, it may lead to false conclusions. So `accountGroup` or  
`bunchOfAccounts` or just plain `accounts` would be better.NOTE : even if the container _is_ a `List`, it’s probably better not to encode the container type into the name.

## 3 - Make Meaningful Distinctions

It is not sufficient to add number series or noise words, even though the compiler is satisfied. If names must be different, then they should also mean something different.  
Consider, for example, the truly hideous practice of creating a variable named `klass` just because the name `class` was used for something else OR `user, user_1 , user_2`

## 4 - Use Pronounceable Names

A significant part of our brains is dedicated to the concept of words. And words are, by definition, pronounceable. It would be a shame not to take advantage of that huge portion of our brains.

## 5 - **Use Searchable Names**
use names that are easy to search for in your code

## 6 - ****Avoid Encodings****
avoid encoding types in your variable names something like : <br/>`PhoneNumber phoneString; // name not changed when type changed!` 
Or name interfaces like `IShapeFactory` in that case `ShapeFactory` should be better 

## 7 - **Avoid Mental Mapping**
Readers shouldn't have to mentally translate your names into other names they already know.
### General Rules For Class And Method Names
 - Avoid words like  `Manager`,  `Processor`,  `Data`, or  `Info`  in the name of a class.
 - Methods should have verb or verb phrase names like  `postPayment`,  `deletePage`, or  `save`.
 -  When constructors are overloaded, use static factory methods with names that describe the arguments.<br/>   
 ```java
    Complex fulcrumPoint = Complex.FromRealNumber(23.0);
 ```
 is better than<br/>
  ```java
    Complex fulcrumPoint = new Complex(23.0);
 ```

## 8 - ******Don’t Be Cute******
If names are too clever, they will be memorable only to people who share the author’s sense of humor.  
-   Avoid using function named  `BigBang`  to mean  `DeleteItems`

## 9 - **Pick One Word per Concept**
Avoid  having `fetch`, `retrieve`, and `get` as equivalent methods of different classes as it’s confusing.  
Likewise, it’s confusing to have a `controller` and a `manager` classes , what will be the difference ?

## 10 - **Don’t Pun**
Avoid using the same word for two purposes. Using the same term for two different ideas is essentially a pun.
For example :  
if we r using `insert` function to insert records into our database and we have another class that has a function that puts value into a collection then using `insert` as a function name will be a pun and in that case `add` or `append` will be better function name.

## 11 - **Use Solution Domain Names**
Remember that the people who read your code will be programmers. So go ahead and use computer science (CS) terms, algorithm names, pattern names, math terms, and so forth.<br/>
The name `AccountVisitor` means a great deal to a programmer who is familiar with the `VISITOR` pattern. What programmer would not know what a `JobQueue` was? There are lots of very technical things that programmers have to do. Choosing technical names for those things is usually the most appropriate course.

## 12 - **Use Problem Domain Names**
The code that has more to do with problem domain concepts should have names drawn from the problem domain.<br/>
**insertUser** -> Problem Domain
**pubbleSortUsers** -> Soluation Domain

## 13 - **Add Meaningful Context**
Imagine that you have variables named `firstName`, `lastName`, `street`, `houseNumber`, `city`, `state`, and `zipcode`. Taken together it’s pretty clear that they form an address.<br/>
create a class named `Address`. Then, even the compiler knows that the variables belong to a bigger concept.

## 14 - **Don’t Add Gratuitous Context**
In an imaginary application called “Gas Station Deluxe,” it is a bad idea to prefix every class or function with `GSD`
