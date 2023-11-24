# Java survival guide 


## Debugging

So you’ve just finished your program and go to compile but an error shows up. You go back to your program, spam control+s several times, pray a little, and then recompile. 

Debugging can definitely be frustrating, hopefully after reading this, it will get easier. The process of debugging is really just trying to gain more information about what is actually happening in the program when you compile/run and why that causes an error/doesn't produce the output you want. 

Bugs are pretty much unavoidable and happen to everyone so debugging efficiently is probably one of the best skills you can learn in java (along with commenting and pseudocode — in fact, good pseudocode should prevent a lot of bugs from even happening in the first place).


### General steps in debugging:

As mentioned before, debugging is really about getting more information (in your head the idea should have worked but in reality something is wrong, so there must be a disconnect between what you had in mind and what has been coded). 

The first step is always to look at the console/terminal and read the error output that java gives you. This is kind of like the first clue in a puzzle hunt, it’s the start of the process. This will give you a line number and an error type. As you debug more, you will realize that many of these error messages are really helpful. In the “Common errors” section, you will find a list of errors, their explanations, and some example codes/error messages. 

You should always scroll to the top, address the first one and then recompile. Sometimes solving the first error will solve other ones too! 


#### Reading error messages

Let’s take a look at an error message:


``` Java
PS C:\Users\micha\Desktop\javaTutor> java Example.java
Exception in thread "main" java.lang.NullPointerException: Cannot invoke "java.lang.Integer.intValue()" because "<local0>" is null
        at Example.doSomething(Example.java:9)
        at Example.main(Example.java:3)
```


The first line “PS C:\Users\micha\Desktop\javaTutor> java Example.java” is me running my program. Then it gives a “NullPointerException.” After that, it lists the path the compiler took when running the program up to the point when it ran into this error. The most recent ones are at the top so the location of this exception is “at Example.doSomething(Example.java:9).” The next step would be to look in Example.java on line 9 to see if there is anything that fits the description of the error message. 


#### Non-syntax errors:

Sometimes there is a logical error in your program, these might not even throw errors (the output is just not what you expected) and the errors that are thrown are often not helpful. The first step is usually trying different inputs. Maybe you will find that your program works only for certain types of input (your Encrpyt.java only works for lower case letters and spews out crazy symbols when you use upper case). Finding out the conditions which cause this error would really help narrow down your search (in the Encrypt.java example, now you only need to look at how you handle upper case letters). 

The next step is to take a closer look at the program. What you typed does not match what you had in mind. What we really want to do is look inside the java compiler and run through the program, line by line, as the compiler would, and compare what the compiler does to what it should be doing. To do this, we can try printing out the values of different variables before and after operations to see if they match. The thought process is something like: “Okay my input is 100 so the value of x should also be 100. We will run this for loop and do some operations on x and afterward it should be 79.” If the value of x from the println after the for loop isn’t 79, we now know what’s wrong.

After locating the error, we could go even further and each time the loop runs, we could print out all the variables along with the iteration the loop is on to find exactly when the program messed up.


### Common errors:


#### Things to look out for

These are very common syntax errors that happen all the time. Some can be really annoying to find! 



* Forgetting {} () or ;
* Having too many {} () or ;
* Putting a ; after a for loop (everything would seem fine but the loop only runs once)
* Putting a ; after a if condition
* Spelling (Java is case sensitive)
* D&I of vars
* Method params (type and number of params)


#### Null pointer Exception:

Error is thrown whenever you reference a var that is pointing to null. This happens when the var is set to null (like below). This will show up more often as you start using more and more complicated data structures. 


##### Example code: 


```Java
public class Example 
{
  public static void main(String[] args)
  {
      doSomething();
  }

  public static void doSomething() 
  {
    Integer number = null;

    if (number > 0) 
    {
      System.out.println("Positive number");
    }
  }
}
```



##### Error message:


```Java
PS C:\Users\micha\Desktop\javaTutor> java Example.java
Exception in thread "main" java.lang.NullPointerException: Cannot invoke "java.lang.Integer.intValue()" because "<local0>" is null
        at Example.doSomething(Example.java:9)
        at Example.main(Example.java:3)
```



#### ArrayIndexOutOfBoundsException:

This is probably something you run into all the time. This happens when you try to reference an index of the array that is larger than array.length - 1 or less than 0. This often happens when you are looping through an array and go out of bounds before the looping ends.


##### Example code:


```Java
public class Example 
{
  public static void main(String[] args)
  {
    processArray();
  }

  public static String processArray() 
  {
    String[] names = new String[4];
    return names[5];
  }
}
```



##### Error message: 


```Java
PS C:\Users\micha\Desktop\javaTutor> java Example.java
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 5 out of bounds for length 4
        at Example.processArray(Example.java:8)
        at Example.main(Example.java:3)
```



#### StringIndexOutOfBoundsException

This is very similar to an array index out of bounds exception.


##### Example code:


```Java
public class Example 
{
  public static void main(String[] args)
  {
    String temp = new String("hellow");
    System.out.println(temp.charAt(10));
  }
} 
```



##### Error message:


```Java
PS C:\Users\micha\Desktop\javaTutor> java .\Example.java
Exception in thread "main" java.lang.StringIndexOutOfBoundsException: String index out of range: 10
        at java.base/java.lang.StringLatin1.charAt(StringLatin1.java:48)
        at java.base/java.lang.String.charAt(String.java:1512)
        at Example.main(Example.java:4)
```



#### ArithmeticException

This error is thrown when you do something illegal in math. Most of the time, it is dividing by 0.


##### Example code:


```Java
public class Example 
{
  public static void main(String[] args)
  {
    int temp  = 10/0;
    System.out.println(temp);
  }
} 
```



##### Error message:


```Java
PS C:\Users\micha\Desktop\javaTutor> java Example.java
Exception in thread "main" java.lang.ArithmeticException: / by zero
        at Example.main(Example.java:3)
```



#### “argument mismatch”/“method cannot be applied to given types”

This is thrown when the arguments passed to a method on its call do not match. Most often the wrong type of param or wrong number of param.


##### Example code:


```Java
public class Example 
{
  public static void main(String[] args)
  {
    argumentTest(100);
  }

  public static void argumentTest(String strIn)
  {
    System.out.println(strIn + "hello world!");
  }
} 
```



##### Error message:


```Java
PS C:\Users\micha\Desktop\javaTutor> java Example.java
Example.java:3: error: method argumentTest in class Example cannot be applied to given types;
    argumentTest(100);
    ^
  required: String
  found:    int
  reason: argument mismatch; int cannot be converted to String
1 error
error: compilation failed
```



##### Example code 2:


```Java
public class Example 
{
  public static void main(String[] args)
  {
    argumentTest(100, "Hello");
  }

  public static void argumentTest(String strIn)
  {
    System.out.println(strIn + "hello world!");
  }
} 
```



##### Error message 2:


```Java
PS C:\Users\micha\Desktop\javaTutor> java Example.java
Example.java:3: error: method argumentTest in class Example cannot be applied to given types;
    argumentTest(100, "Hellow");
    ^
  required: String
  found:    int,String
  reason: actual and formal argument lists differ in length
1 error
error: compilation failed
```



#### “cannot find symbol”

This happens all the time and it is mostly because you misspelled the name of a var or method (java is case sensitive!). It could also be because the var was D&I’d improperly.  


##### Example code:


```Java
public class Example 
{
  public static void main(String[] args)
  {
    argumentTest("Hello");
  }

  public static void argumentTest(String strIn)
  {
    System.out.println(strin + "hello world!");
  }
} 
```



##### Error message:


```Java
PS C:\Users\micha\Desktop\javaTutor> java Example.java
Example.java:7: error: cannot find symbol
    System.out.println(strin + "hello world!");
                       ^
  symbol:   variable strin
  location: class Example
1 error
error: compilation failed
```



##### Example code 2: 


```Java
public class Example 
{
  public static void main(String[] args)
  {
    Int temp = 100;
    System.out.println(temp);
  }
} 
```



##### Error message 2:


```Java
PS C:\Users\micha\Desktop\javaTutor> java Example.java
Example.java:3: error: cannot find symbol
    Int temp = 100;
    ^
  symbol:   class Int
  location: class Example
1 error
error: compilation failed
```



## Pseudocode

Before typing each program, you should have a clear outline completed in the form of pseudocode. You know your pseudocode is good (good enough) if when you go to start coding, you barely need to think. All the “problems” that need to be addressed in the program should all be solved in the pseudocode stage, coding should really just be implementing your ideas. 

Having good pseudocode like this will prevent you from running into logic errors while programing and save a lot of time.


### Here are some good examples of pseudocode:


#### Example 1


```Java
If student grade >= 60
    Print "passed"
Else
    Print "failed"
```



---


#### Example 2


```Java
Set gradecounter to 1
While gradecounter <= 10
    Input next grade
    Add grade into total

Set classaverage to total / 10
Print classaverage.
```



---


#### Example 3


```Java
initialize passes to 0
initialize failures to 0
initialize student to 1

while studentcounter <= 10
    input the next exam result
    if the student passed
        add 1 to passes
    else
        add 1 to failures
    add 1 to studentcounter

print the number of passes
print the number of failures
if eight or more students passed
   print "raise tuition"
```



### Testing

Writing test cases for your program in the pseudocode stage can help you better understand the program you are supposed to write and the outputs it is supposed to give. If you go into the typing phase with a wrong understanding of the program, your program is definitely not going to work. 

You might have also realized that in the non-syntax debugging section, one of the first steps is to try different inputs and see if they match the output you were expecting. That is pretty much exactly what testing is. 


#### Corner cases

Deciding what numbers are best to test needs a bit of intuition, but it has a lot to do with “corner cases.” Corner cases are pretty much exactly what they sound like, they are the extremes at which the program operates. When running a for loop for n times, chances are, if there is a bug, the bug is on the nth iteration of the loop. There are a variety of reasons that contribute to corner cases being harder, they often need to be handled in a unique way because they are different from the rest of the cases. A perfect example of this is Encrypt.java’s y and z. These two letters, when shifted 2 down the alphabet, need to be wrapped around. 

So corner cases are especially important to pay attention to in testing. This is why really small and really large numbers are usually good tests.


## Comments

Comments are something that seems useless and annoying but will get more and more important as you code more, especially when collaborating with others. Comments serve many purposes. One of them is to remind yourself of what a method/section of code does. This is especially useful when programs get long (your game projects are probably going to be thousands of lines long). 

Another useful thing about comments is that they can tell other people what your code is doing. When coding in a job, you write your code not just for yourself, but for everyone else on your team. When you are done with a program and leave, someone else might pick up where you left off to add more functionality but if the code is undecipherable, it would cost the company a lot of time. 


### How to comment


#### Single line comments

At the start of the line, put two slashes: 


```Java
//this is a one line comment
```


These are often used before a section of code (explain what the for loop does, why we have this if statement, etc). They can also be used in the same line right after some code:


```Java
int i = 0; //D&I i to be 0
```



#### Multi-line comments

These are good for program headers, comments explaining entire methods, etc. The syntax for these are as follows:


```Java
/*Comment starts
continues
continues
.
.
.
Commnent ends*/
```



#### Comment tags

There are also a bunch of comment tags that you could consider utilizing to make your comments more concise. They are also used to generate documentation but that’s for a different class. There are a lot of them, here are a few:


<table>
  <tr>
   <td><code>Tag</code>
   </td>
   <td><code>Description</code>
   </td>
  </tr>
  <tr>
   <td><code>@author</code>
   </td>
   <td><code>To add the author of the class.</code>
   </td>
  </tr>
  <tr>
   <td><code>@version</code>
   </td>
   <td><code>To specify "Version" subheading and version-text when -version option is used.</code>
   </td>
  </tr>
  <tr>
   <td><code>@since</code>
   </td>
   <td><code>To add "Since" heading with since text to generated documentation.</code>
   </td>
  </tr>
  <tr>
   <td><code>@param</code>
   </td>
   <td><code>To add a parameter with given name and description to 'Parameters' section.</code>
   </td>
  </tr>
  <tr>
   <td><code>@return</code>
   </td>
   <td><code>Explains what a method returns (except void)</code>
   </td>
  </tr>
</table>



### Types of comments


#### Headers 

Headers are where you put your name, program title, and a description of what your program does. In Java class, you will also sometimes put your testing, pseudocode, and “working on” in here as well. Here’s an example of Encrypt.java:


```Java
/*
* [name]
* [Date]
* Encrypt.java
*
* Description:
* This program uses String methods and for loops to encrypt a String that 
* the user enters 13 times. Since the encryption is a shift by two letters 
* down the alphabet after 13 times, it should get back to the original. 
* Punctuation and numbers stay the same.
*
* Working On:
*   for loops
*   if & else
*   string methods
*   boolean expressions
*   logical operators
*/
```



#### Methods

In class, each of your methods should have comments before it, explaining what it does. Here is an example:


```Java
/**
* Returns an Image object that can then be painted on the screen. 
* The url argument must specify an absolute href. The name
* argument is a specifier that is relative to the url argument. 
* 
* This method always returns immediately, whether or not the 
* image exists. When this applet attempts to draw the image on
* the screen, the data will be loaded. The graphics primitives 
* that draw the image will incrementally paint on the screen. 
*
* @param  url  an absolute URL giving the base location of the image
* @param  name the location of the image, relative to the url argument
* @return      the image at the specified URL
* @see         Image
*/

public Image getImage(URL url, String name) 
{
    try 
    {
        return getImage(new URL(url, name));
    } 
    catch (MalformedURLException e) 
    {
        return null;
    }
}
```



#### Detail comments

Adding comments into an algorithm to explain what each line does is good practice, especially for more complicated algorithms where what the program is doing is not immediately clear. Here is a good example for Encrpyt.java:


```Java
public void encryptString()
{
    char newChar = '';
    //this for loop checks every character in line
    for (int num = 0; num < line.length(); num++)
    {
        //the shifted character        
        newChar = (char)((int)(line.charAt(num)) + SHIFT);
        //checks if the shifted character goes beyond 'Z' or 'z'
        if ((newChar > 90 && newChar < 97) || (newChar > 122))
        {
            //wraps the shifted character (that went beyond z) back around
            newChar = (char)((int)(line.charAt(num)) - 26 + SHIFT);
            //puts the new character into the line
            line = line.substring(0, num) + newChar 
                + line.substring(num + 1);
        }
        //checks whether the shifted character is between A-Z or a-z
        else if ((newChar <= 90 && newChar >= 65) 
            || (newChar <=122 && newChar >= 97))
        {
            //adds the new character into the line
            line = line.substring(0, num) + newChar 
            + line.substring(num + 1);
        }
        else //everything else shouldn't change
            line = line.substring(0, num) + line.charAt(num) 
                + line.substring(num + 1);
    }
}
```



## Formatting and naming conventions

Formatting and naming conventions will help you stay organized and consistent. In Java class, you will be using Allman formatting and camelCase naming. Consistency in formatting will make your code easier to understand. 

To illustrate this, here is an example of really bad code formatting: 


```Java
public void encryptString(){ char newChar=''; 
for(int num=0;num<line.length();num++){
newChar = (char)((int)(line.charAt(num)) + SHIFT);
if((newChar>90&&newChar<97)||(newChar>122)){
newChar=(char)((int)(line.charAt(num))-26+SHIFT);
line=line.substring(0,num)+newChar+line.substring(num + 1);
}else if((newChar<=90&&newChar>=65)||(newChar<=122&&newChar>= 97))        
line=line.substring(0,num)+newChar+line.substring(num+1);
else line=line.substring(0,num)+line.charAt(num)+line.substring(num+1);}}
```


It is hard to believe that these two are exactly the same code! Both would run the same way when compiled. 


```Java
public void encryptString()
{
  char newChar = '';
  for (int num = 0; num < line.length(); num++)
  {
    newChar = (char)((int)(line.charAt(num)) + SHIFT);
    if ((newChar > 90 && newChar < 97) || (newChar > 122))
    {
      newChar = (char)((int)(line.charAt(num)) - 26 + SHIFT);
      line = line.substring(0, num) + newChar + line.substring(num + 1);
    }
    else if ((newChar <= 90 && newChar >= 65)
      || (newChar <=122 && newChar >= 97))
    {
      line = line.substring(0, num) + newChar + line.substring(num + 1);
    }
    else
    {
      line = line.substring(0, num) + line.charAt(num) + line.substring(num + 1);
    }
  }
}
```


Chances are, the first one gave you a headache. Even though both segments of code will be treated the same by the compiler, the second one is much easier to understand (and debug!).


### Allman 

Allman is what you will be using in java class, it is a style of formatting. In Allman, curly braces take up their own line: 


```Java
while (x == y)
{
  something();
  somethingelse();

  if(boolVar)
  {
    doThat();
  } 
  else
  {
    doThis();
  } 
}

finalthing();
```



### CamelCase 

This is a variable naming convention. Single word variable names are lower case (unless it’s constant) and var names with multiple words are put together with the first letter of each word after the first being uppercase. Snake_case is also pretty popular, instead of using uppercase letters, we put underscores (_) between words:


```Java
//CamelCase
variableNumberOne, wasChanged, counter

//SnakeCase
variable_number_one, was_changed, counter
```



### Other stylistic conventions 


#### Variable naming

Giving your variables useful names is, well, useful. From the Encrpty.java examples above, if we had really bad variable names, it might look something like this:


```Java
public void encryptString()
{
  char a = '';
  for (int b = 0; b < c.length(); b++)
  {
    a = (char)((int)(c.charAt(b)) + D);
    if ((a > 90 && a < 97) || (a > 122))
    {
      a = (char)((int)(c.charAt(b)) - 26 + D);
      c = c.substring(0, b) + a + c.substring(b + 1);
    }
    else if ((a <= 90 && a >= 65) || (a <=122 && a >= 97))
    {
      c = c.substring(0, b) + a + c.substring(b + 1);
    }
    else
    {
      c = c.substring(0, b) + c.charAt(b) + c.substring(b + 1);
    }
  }
}
```


The program becomes so much harder to understand. This is also the case for class and method names. 


#### Spacing 

Java compilers ignore all white space so, kind of like before, you can space things out however you want. Spacing in java just like paragraph breaks when writing an essay, it helps organize your program into logical sections.

It can be useful to have blank lines in your program, consider the follow program:


```Java
import java.util.*;
class Main 
{
  public static void main(String[] args) 
  {
    HashMap<String, Integer> numbers = new HashMap<>();
    numbers.put("First", 1);
    numbers.put("Second", 2);
    numbers.put("Third", 3);
    System.out.println("HashMap: " + numbers);
    int value = numbers.get("Second");
    value = value * value;
    numbers.put("Second", value);
    System.out.println("HashMap with updated value: " + numbers);
    Iterator hmIterator = numbers.entrySet().iterator();
    while (hmIterator.hasNext()) 
    {
        Map.Entry mapElement = (Map.Entry)hmIterator.next();
        int marks = ((int)mapElement.getValue() + 10);
        System.out.println(mapElement.getKey() + " : " + marks);
    }
  }
}
```


It is fine as it is, but it can be better:


```Java
import java.util.*;

class Main 
{
  public static void main(String[] args) 
  {
    HashMap<String, Integer> numbers = new HashMap<>();
    numbers.put("First", 1);
    numbers.put("Second", 2);
    numbers.put("Third", 3);


    System.out.println("HashMap: " + numbers);


    int value = numbers.get("Second");
    value = value * value;
    numbers.put("Second", value);


    System.out.println("HashMap with updated value: " + numbers);


    Iterator hmIterator = numbers.entrySet().iterator();
    while (hmIterator.hasNext()) 
    {
        Map.Entry mapElement = (Map.Entry)hmIterator.next();
        int marks = ((int)mapElement.getValue() + 10);


        System.out.println(mapElement.getKey() + " : " + marks);
    }
  }
}
```


Just like that, the program becomes easier to read (it would be even easier to read if it had comments!). Oftentimes, you will find putting blank lines before/after loops, if-else statements, or chunks of similar operations helpful in grouping up your program. 

Aside from blank lines between chunks of code, spaces can also be used between symbols to make things easier to read: 


```Java
value = value * value;
//vs
value=value*value;
```



#### Line length 

Most text editors/IDEs have a vertical line to the right of the screen. This line is a good marker for roughly how long your lines should be. If your lines go past it, you might want to consider splitting it up or continuing it on the next line.
