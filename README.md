

# Clean Code Book Summary ( By Robert C. Martin )
## Table of contents
- [Foreword](#foreword)
- [Chapter 1 - Clean Code](#chapter1)
- [Chapter 2 - Meaningful Names](#chapter2)
- [Chapter 3 - Functions](#chapter3)

<a name="foreword">
<h1>Foreword</h1> 
</a>
In about 1951, a quality approach called Total Productive Maintenance (TPM) came on the Japanese scene. Its focus is on maintenance rather than on production. One of the major pillars of TPM is the set of so-called 5S principles

-   **_Seiri_**, or  **organization**  : Knowing where things are—using approaches such as suitable naming—is crucial. You think naming identifiers isn’t important? well it’s  **IMPORTANT**.
-   **_Seiton_**, or  **tidiness**  : _A place for everything, and everything in its place_. A piece of code should be where you expect to find it—and, if not, you should re-factor to get it there.
-   **_Seiso_**, or  **cleaning**  : Keep the workplace free of hanging wires, grease, scraps, and waste. what is the use of commented-out code lines that capture history or wishes for the future? Get rid of them.
-   **_Seiketsu_**, or  **standardization**: The group agrees about how to keep the workplace clean. they put standards ? Where do those standards come from? we will find that later on
-   **_Shutsuke_**, or  **discipline**  (_self_-discipline) : This means having the discipline to follow the practices and to frequently reflect on one’s work and be willing to change.

<a name="chapter1">
<h1>Chapter 1 - Clean Code</h1>
</a>

### what does Bjarne Stroustrup says about clean code ?
I like my code to be elegant and efficient. The logic should be straightforward to make it hard for bugs to hide, the dependencies minimal to ease maintenance, error handling complete according to an articulated strategy, and per- formance close to optimal so as not to tempt people to make the code messy with unprinci- pled optimizations. Clean code does one thing well.
### How To Defend Your Clean Code Responsability Against Your Managers
what if you were a doctor and had a patient who demanded that you stop all the silly hand-washing in preparation for surgery because it was taking too much time?2 Clearly the patient is the boss; and yet the doctor should absolutely refuse to comply. Why? Because the doctor knows more than the patient about the risks of dis- ease and infection. It would be unprofessional (never mind criminal) for the doctor to comply with the patient.  
So too it is unprofessional for programmers to bend to the will of managers who don’t understand the risks of making messes.
	
<a name="chapter2">
<h1>Chapter 2 - Meaningful Names</h1>
</a>

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
**insertUser** -> Problem Domain <br/>
**pubbleSortUsers** -> Soluation Domain

## 13 - **Add Meaningful Context**
Imagine that you have variables named `firstName`, `lastName`, `street`, `houseNumber`, `city`, `state`, and `zipcode`. Taken together it’s pretty clear that they form an address.<br/>
create a class named `Address`. Then, even the compiler knows that the variables belong to a bigger concept.

## 14 - **Don’t Add Gratuitous Context**
In an imaginary application called “Gas Station Deluxe,” it is a bad idea to prefix every class or function with `GSD`

<a name="chapter3">
<h1>Chapter 3 - Functions</h1>
</a>

# 1 - **Small**
The first rule of functions is that they should be small. The second rule of functions is that *they should be smaller than that.*

### **Blocks and Indenting**
This implies that the blocks within if statements, else statements, while statements, and so on should be one line long. Probably that line should be a function call. Not only does this keep the enclosing function small, but it also adds documentary value because the function called within the block can have a nicely descriptive name.

# 2 - **Do One Thing**
FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY.

### **Sections within Functions**
if a function is divided into sections such as `declarations`, `initializations`, and `sieve`. This is an obvious symptom of doing more than one thing. Functions that do one thing cannot be reasonably divided into sections.

# 3 - **One Level of Abstraction per Function**
Mixing levels of abstraction within a function is always confusing. Readers may not be able to tell whether a particular expression is an essential concept or a detail. for example:

- `getHtml()` -> High level abstraction
-  `String pagePathName = PathParser.render(pagePath);` -> intermediate level abstraction
- `.append("\n")` -> low level abstraction

###  **Reading Code from Top to Bottom: The Stepdown Rule**
We want the code to read like a top-down narrative. We want every function to be fol- lowed by those at the next level of abstraction so that we can read the program, descending one level of abstraction at a time as we read down the list of functions.


# 4 - **Switch Statements**
`switch` statements always do N things. Unfortunately we can’t always avoid `switch` statements, but we can make sure that each switch statement is buried in a `low-level` class and is never repeated. We do this, of course, with `polymorphism`.

# 5 - **Use Descriptive Names**
- The smaller and more focused a function is, the easier it is to choose a descriptive name.
- Don’t be afraid to make a name long. A long descriptive name is better than a short enigmatic name.
- A long descriptive name is better than a long descriptive comment.

# 6 - **Function Arguments**
The ideal number of arguments for a function is zero (niladic). Next comes one (monadic), followed closely by two (dyadic). Three arguments (triadic) should be avoided where possible. More than three (polyadic) requires very special justification—and then shouldn’t be used anyway.

###   **Flag Arguments**
Flag arguments`|True,False|` are ugly. Passing a boolean into a function is a truly terrible practice. It immediately complicates the signature of the method, loudly proclaiming that this function does more than one thing. It does one thing if the flag is true and another if the flag is false!

### **Dyadic Functions**
A function with two arguments is harder to understand than a monadic function. For exammple, `writeField(name)` is easier to understand than `writeField(output-Stream, name)`.
There are times, of course, where two arguments are appropriate. For example, `Point p = new Point(0,0);` is perfectly reasonabl.

### **Triads**
Functions that take three arguments are significantly harder to understand than dyads. The issues of ordering, pausing, and ignoring are more than doubled. I suggest you think very carefully before creating a triad.
For example, consider the common overload of `assertEquals` that takes three arguments: `assertEquals(message, expected, actual)`. How many times have you read the `message` and thought it was the `expected`?

### **Argument Objects**
When a function seems to need more than two or three arguments, it is likely that some of those arguments ought to be wrapped into a class of their own. Consider, for example, the difference between the two following declarations:

    Circle makeCircle(double x, double y, double radius);
    Circle makeCircle(Point center, double radius);

### **Argument Lists**
Function that takes argument lists can be monads, dyads or even triads: 

    void monad(String... args);
    void dyad(String name, String... args); 
    void triad(String name, int count, String... args)

### **Verbs and Keywords**
Choosing good names for a function can go a long way toward explaining the intent of the function and the order and intent of the arguments. In the case of a monad, the function and argument should form a very nice verb/noun pair.
`writeField(name)` is better than `write(name)`

# 7 - **Have No Side Effects**
Your function promises to do one thing, but it also does other hidden things. Sometimes it will make unexpected changes to the variables of its own class or even more.
Consider, for example, This function uses a standard algorithm to match a `userName` to a `password`. It returns `true` if they match and `false` if anything goes wrong. But it also has a side effect. Can you spot it?
```java
public class UserValidator {  
	private Cryptographer cryptographer;

	public boolean checkPassword(String userName, String password) { 
		User user = UserGateway.findByName(userName);  
		if (user != User.NULL) {
			String codedPhrase = user.getPhraseEncodedByPassword(); 
			String phrase = cryptographer.decrypt(codedPhrase, password);
			if ("Valid Password".equals(phrase)) {
				Session.initialize();
				return true; 
			}
		}
		return false; 
	}
}
```
The side effect is the call to `Session.initialize()`, of course. The `checkPassword` function, by its name, says that it checks the password. If it is called out of order, session data may be inadvertently lost. Temporal couplings are con-fusing, especially when hidden as a side effect. 
If you must have a temporal coupling, you should make it clear in the name of the function. In this case we might rename the function `checkPasswordAndInitializeSession`, though that certainly violates `“Do one thing.”`

### **Output Arguments**
output arguments should be avoided. If your function must change the state of something, have it change the state of its owning object.
when you see this functions `appendFooter(report);` you will be asking Does this function append `report` as the footer to something? Or does it append some footer to `report`? Is s an input or an output? 
better approch is to add the append   `report.appendFooter();` as a functiuon to a report object to make it clear.

# 8 - **Command Query Separation**
Functions should either do something or answer something, but not both as it will be confusing.
for example `public boolean set(String attribute, String value);` This function sets the value of a named attribute and returns `true` if it is successful and `false` if no such attribute exists.
 This leads to odd statements like this: `if (set("username", "unclebob"))`
 so a better version will be :
 ```java
 if (attributeExists("username")) { 
	 setAttribute("username", "unclebob");
	 ....
}
```

# 9 - **Prefer Exceptions to Returning Error Code**
```java
public void delete(Page page) { 
	try {
		deletePageAndAllReferences(page); 
	}catch (Exception e) { 
		logError(e);
	} 
}

private void deletePageAndAllReferences(Page page) throws Exception { 
	deletePage(page);  
	registry.deleteReference(page.name); 
	configKeys.deleteKey(page.name.makeKey());
}

private void logError(Exception e) {
	logger.log(e.getMessage());
}
```
In the above, the `delete` function is all about error processing. It is easy to understand and then ignore. The `deletePageAndAllReferences` function is all about the processes of fully deleting a page. Error handling can be ignored. This provides a nice separation that makes the code easier to understand and modify.

### **Error Handling Is One Thing**
Functions should do one thing. Error handing is one thing. Thus, a function that handles errors should do nothing else.

### **The Error.java Dependency Magnet**
Use Exceptions instead of Error codes.

# 10 - **Don’t Repeat Yourself**
Duplication may be the root of all evil in software. Many principles and practices have been created for the purpose of controlling or eliminating it.

# 11 - **Structured Programming**
every function, and every block within a function, should have one entry and one exit. Following these rules means that there should only be one `return` statement in a function, no `break` or `continue` statements in a loop, and never, ever, any `goto` statements.
So if you keep your functions `small`, then the occasional multiple `return`, `break`, or continue statement does no harm and can sometimes even be more expressive than the single-entry, single-exit rule. On the other hand, goto only makes sense in large functions, so it should be avoided.
