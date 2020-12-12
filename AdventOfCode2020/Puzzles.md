## First day

[You can see the problem here](https://adventofcode.com/2020/day/1)

So the idea is to sum all the numbers we have as an input and check, which pair of them sum 2020.

First I want to try to write it in C# (since it's Unity script language so I get used to it's Syntax).

This is the code:

```
var rounds = new int();
       var inputs = new List<int>()
       {1962
,1577
...
,847};

for (var firstNumber = inputs.Count - 1; firstNumber >= 0; firstNumber--)
{
   for (var secondNumber = firstNumber - 1; secondNumber >= 0; secondNumber--)
       {
       rounds++;
       if (inputs[firstNumber]+inputs[secondNumber] == 2020 ){
           Console.WriteLine("First number "+inputs[firstNumber]);
           Console.WriteLine("Second number "+inputs[secondNumber]);
           int solution = inputs[firstNumber] * inputs[secondNumber];
           Console.WriteLine("Solution: "+solution);
       }
       }

}

Console.WriteLine("Rounds done: "+rounds);
   }
}

```

![screenshot](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/AdventOfCode2020/Captura001.JPG)

The counter "round" goes up to 19900, so that's a long for loop.

If I stop it when it finds the solution, the round goes 17755 (not a big difference).

The second turn is to go deeper and search for 3 numbers that sum 2020.

I don't like go too deep in the for but for now it can be helpful as a first iteration.

```
for (var firstNumber = inputs.Count - 1; firstNumber >= 0; firstNumber--)
{
   for (var secondNumber = firstNumber - 1; secondNumber >= 0; secondNumber--)
       {
           for(var thirdNumber = secondNumber -1; thirdNumber >=0; thirdNumber--)
           {
               rounds++;
               if (inputs[firstNumber]+inputs[secondNumber] +inputs[thirdNumber] == 2020 ){
                   Console.WriteLine("First number "+inputs[firstNumber]);
                   Console.WriteLine("Second number "+inputs[secondNumber]);
                   Console.WriteLine("Third number "+inputs[thirdNumber]);
                   int solution = inputs[firstNumber] * inputs[secondNumber] * inputs[thirdNumber];
                   Console.WriteLine("Solution: "+solution);
                   firstNumber = 0;
                   secondNumber =0;
                   thirdNumber =0;
               }
           }
       }

}

```

_the for loop goes deep_

In this case the looped worked much more. 360088 times. Let's try to cut it.

I'm going to try to make it down.

Let's try to divide the list of input into even and odd numbers. Because we know that 2020 is an even number so it can be the sum of 2 odds numbers or 2 even numbers.

And this is the code I used:

```
// For each value add it to others
var evenInputs = new List<int>();
var oddInputs = new List<int>();
int solution;
Console.WriteLine("Sorting...");
for (var index = inputs.Count - 1; index >= 0; index--)
{
rounds++;
if (inputs[index]%2 == 0) {
    evenInputs.Add(inputs[index]);
}
else
{
    oddInputs.Add(inputs[index]);
}
}
Console.WriteLine("Sorting done. Rounds: "+rounds);
Console.WriteLine("Checking odds+odd");
for (var firstNumber = oddInputs.Count - 1; firstNumber >= 0; firstNumber--)
{
  for (var secondNumber = firstNumber - 1; secondNumber >= 0; secondNumber--)
      {
      rounds++;
      if (oddInputs[firstNumber]+oddInputs[secondNumber] == 2020 ){
          Console.WriteLine("First number "+oddInputs[firstNumber]);
          Console.WriteLine("Second number "+oddInputs[secondNumber]);
          solution = oddInputs[firstNumber] * oddInputs[secondNumber];
          Console.WriteLine("Solution: "+solution);
          firstNumber=0;
          secondNumber=0;
      }
      }
}
Console.WriteLine("Odd+Odd done. Rounds: "+rounds);
Console.WriteLine("Checking even+even");
for (var firstNumber = evenInputs.Count - 1; firstNumber >= 0; firstNumber--)
{
  for (var secondNumber = firstNumber - 1; secondNumber >= 0; secondNumber--)
      {
      rounds++;
      if (evenInputs[firstNumber]+evenInputs[secondNumber] == 2020 ){
          Console.WriteLine("First number "+evenInputs[firstNumber]);
          Console.WriteLine("Second number "+evenInputs[secondNumber]);
          solution = evenInputs[firstNumber] * evenInputs[secondNumber];
          Console.WriteLine("Solution: "+solution);
          firstNumber=0;
          secondNumber=0;
      }
      }
}
Console.WriteLine("Rounds done: "+rounds);
   }
}

```

And it's good. It needs only half of the rounds to find the solution. 7488 in this case. 10109 if I it was just the last pair of numbers. Cool! Now let's try with the combination.

If you have an odd number it can be Even+Even+Even, Odd+Odd+Even. So that's the 2 combinations we're going to try.

```
var evenInputs = new List<int>();
var oddInputs = new List<int>();
int solution;
Console.WriteLine("Sorting...");
for (var index = inputs.Count - 1; index >= 0; index--)
{
rounds++;
if (inputs[index]%2 == 0) {
    evenInputs.Add(inputs[index]);
}
else
{
    oddInputs.Add(inputs[index]);
}
}
Console.WriteLine("Sorting done. Rounds: "+rounds);
Console.WriteLine("Checking odds+odd+even");
for (var firstNumber = oddInputs.Count - 1; firstNumber >= 0; firstNumber--)
{
  for (var secondNumber = firstNumber - 1; secondNumber >= 0; secondNumber--)
      {
          for(var evenNumber = evenInputs.Count - 1; evenNumber >=0; evenNumber--)
          {
                     rounds++;
      if (oddInputs[firstNumber]+oddInputs[secondNumber]+evenInputs[evenNumber] == 2020 ){
          Console.WriteLine("First number "+oddInputs[firstNumber]);
          Console.WriteLine("Second number "+oddInputs[secondNumber]);
          Console.WriteLine("Third number "+evenInputs[secondNumber]);
          solution = oddInputs[firstNumber] * oddInputs[secondNumber] * evenInputs[evenNumber];
          Console.WriteLine("Solution: "+solution);
          firstNumber=0;
          secondNumber=0;
          evenNumber=0;
          }
      }
      }
}
Console.WriteLine("Odd+Odd+Even done. Rounds: "+rounds);
Console.WriteLine("Checking even+even+even");
for (var firstNumber = evenInputs.Count - 1; firstNumber >= 0; firstNumber--)
{
  for (var secondNumber = firstNumber - 1; secondNumber >= 0; secondNumber--)
      {
          for(var thirdNumber = secondNumber -1; thirdNumber >=0; thirdNumber--)
          {
              rounds++;
              if (evenInputs[firstNumber]+evenInputs[secondNumber] +evenInputs[thirdNumber] == 2020 ){
                  Console.WriteLine("First number "+evenInputs[firstNumber]);
                  Console.WriteLine("Second number "+evenInputs[secondNumber]);
                  Console.WriteLine("Third number "+evenInputs[thirdNumber]);
                  solution = evenInputs[firstNumber] * evenInputs[secondNumber] * evenInputs[thirdNumber];
                  Console.WriteLine("Solution: "+solution);
                  firstNumber = 0;
                  secondNumber =0;
                  thirdNumber =0;
              }
          }
      }

}
Console.WriteLine("Rounds done: "+rounds);
   }
}


```


And I find it! It takes 459076 rounds to find it. But wait. That's less than the 360088 times that the other algorithm took. So maybe using different groups (Because you have to take 1 from the even before going to the odds) is too much. Let's see how takes to the brute force to find it if it's the last pair.

(just comment the break out of the for iterator for that)

1313400 times. Ok. That's better. I cut that in half because if I run the other solution without taking the exit... 656619 times so still around half. Still not a bad strategy. Yay.

## Second day

This puzzle has a more dificult input. It should be easy to create a rule about it, but first I want to know I can parse it!

This is a line of the input:

```
2-3 b: bkkb
```

To separate the strings for each input I put "," with notepad++. And also retrieve the jumplines and put spaces because it doesn't enter as a collection if I don't do that. Now I have 1000 Strings. Cool.

Now not to break the online compiler, I'm making first a run to chop the String in the parts I need. This is what I've used:

```
// inputs is a collection with all the strings, but I take only one for checking

var stringToChop = inputs[25];
int firstDelimitation = stringToChop.IndexOf("-");
int secondDelimitation = stringToChop.IndexOf(" ");
int thirdDelimitation = stringToChop.IndexOf(":");
int leastTimes = Int32.Parse(stringToChop.Substring(0, firstDelimitation));
int mostTimes = Int32.Parse(stringToChop.Substring(firstDelimitation+1,secondDelimitation-2));
char letterToCheck = stringToChop[thirdDelimitation-1];
string password = stringToChop.Substring(thirdDelimitation+2);
Console.WriteLine(leastTimes);
Console.WriteLine(mostTimes);
Console.WriteLine(letterToCheck);
Console.WriteLine(password);


```

Now that I have the variables as I want them, I can try to make the check and then iterate it.

This is that step:

```

int validPasswords = 0;


var stringToChop = inputs[2];
int firstDelimitation = stringToChop.IndexOf("-");
int secondDelimitation = stringToChop.IndexOf(" ");
int thirdDelimitation = stringToChop.IndexOf(":");
int leastTimes = Int32.Parse(stringToChop.Substring(0, firstDelimitation));
int mostTimes = Int32.Parse(stringToChop.Substring(firstDelimitation+1,secondDelimitation-2));
char letterToCheck = stringToChop[thirdDelimitation-1];
string password = stringToChop.Substring(thirdDelimitation+2);
int repetitionCount =0;
  foreach (var character in password){
      if (character.Equals(letterToCheck)){
          repetitionCount++;
      }
  }
  if ((repetitionCount <= mostTimes) && (repetitionCount >= leastTimes)) {
      validPasswords++;
  }

  Console.WriteLine(leastTimes);
Console.WriteLine(mostTimes);
Console.WriteLine(letterToCheck);
Console.WriteLine(password);
Console.WriteLine(repetitionCount);
Console.WriteLine(validPasswords);


```

I like the iterator of characters in a string. Now time to double check that those >= and <= are correct to the problem!

Yeah, it seems so. Now time to iterate!

And it works! here is the code:

```

var inputs = new List<String>()
{"2-6 w: wkwwwfwwpvw ","14-15 v:
...
 };

int validPasswords = 0;


foreach (string stringToChop in inputs)
{

    int firstDelimitation = stringToChop.IndexOf("-");
    int secondDelimitation = stringToChop.IndexOf(" ");
    int thirdDelimitation = stringToChop.IndexOf(":");
    int leastTimes = Int32.Parse(stringToChop.Substring(0, firstDelimitation));
    int mostTimes = Int32.Parse(stringToChop.Substring(firstDelimitation+1,secondDelimitation-2));
    char letterToCheck = stringToChop[thirdDelimitation-1];
    string password = stringToChop.Substring(thirdDelimitation+2);
    int repetitionCount =0;
      foreach (var character in password){
          if (character.Equals(letterToCheck)){
              repetitionCount++;
          }
      }
      if ((repetitionCount <= mostTimes) && (repetitionCount >= leastTimes)) {
          validPasswords++;
      }
}



Console.WriteLine(validPasswords);



}
}

```

Now for the second part!

Ok, now the rules are different. But it seems that can be solved by being careful with "indexOf" (C# is zero based, the problem is not)

Time to use the [IR operator](https://docs.microsoft.com/es-es/dotnet/csharp/language-reference/operators/boolean-logical-operators#logical-exclusive-or-operator-), one of those operators that are almost never used.


This is the code used.

```

int validPasswords = 0;


foreach (string stringToChop in inputs)
{

    int firstDelimitation = stringToChop.IndexOf("-");
    int secondDelimitation = stringToChop.IndexOf(" ");
    int thirdDelimitation = stringToChop.IndexOf(":");
    int firstLetter = Int32.Parse(stringToChop.Substring(0, firstDelimitation));
    int secondLetter = Int32.Parse(stringToChop.Substring(firstDelimitation+1,secondDelimitation-2));
    char letterToCheck = stringToChop[thirdDelimitation-1];
    string password = stringToChop.Substring(thirdDelimitation+2);

      if (password[firstLetter-1].Equals(letterToCheck) ^ password[secondLetter-1].Equals(letterToCheck)) {
          validPasswords++;
      }
}



Console.WriteLine(validPasswords);

```

The only thing was the syntax error while swapping the if (always a "{" or a "(" extra). Ah, and also the correction was to put a -1 instead of a +1 that I thought that it gave a outofbounds error.

Yay * it's late *

## Third day

This is a [day about a map, trees](https://adventofcode.com/2020/day/3) and I think it has to do with the modulus operator. And today I don't have a mouse so everything is going to bit a little slower.

First we parse the input. As we did with other we need a bit of notepad++, we delete the end of line (EOL) and we add at the beginning of each line "," so you get something like this

```

var inputs = new List<string>()
       {

       ,"..#...#..#...#......#.......... ","....#..#....#.......#........#."
       };


```

Now we have to analize each string and see if there is a miss or if there is a tree. Each time there is going to be in someplace around in the 31 character long (I added a space) String. So the first thing I try to make the program to work with only one input string. Then, if it works I can interpolate.

This is the first iteration.

```

using System;
using System.Collections.Generic;

namespace HelloWorld
{
  class Program
  {
    static void Main(string[] args)
    {
      Console.WriteLine("Hello World!");   

var inputs = new List<string>()
       {
       "........#..#.##.#..............
       ...
        ","....#..#....#.......#........#."};
             Console.WriteLine(inputs[4]);
             Console.WriteLine(inputs[4].Length);
             Console.WriteLine(inputs[4][31]);
             int horizontalPosition = 0;
             int treeCounter = 0;
             int characterPositionToCheck = (horizontalPosition % 31)  -1;
             if (inputs[0][characterPositon].Equals("#")) {
       treeCounter++
       }
       Console.WriteLine(treeCounter);

       ```


     Important: when using char (individual characters) and the method Equals, it's better to use '' instead of "" or it won't work.


     And this is the next test

```     
                 Console.WriteLine(inputs[4].Length);
             Console.WriteLine(inputs[4][31]);
             int horizontalPosition = 35;
             int treeCounter = 0;
             int characterPositionToCheck = (horizontalPosition % 31)  -1;
             if (inputs[1][characterPositionToCheck].Equals('#')) {
       treeCounter++;
       }
       Console.WriteLine(treeCounter);
  ```

       I had some problems with horizontal position because sometimes it went -1, so I just put a longer formula to get the index through the verticalPosition.

         ```
       int characterPositionToCheck = ((verticalPosition * 3) % 31);
         ```

       I guess that converting from zero based to one base has this kind of problems.

       Aaaaand it worked! here is the snippet

         ```

                    Console.WriteLine(inputs[1]);
             Console.WriteLine(inputs.Count);
             Console.WriteLine(inputs[4][31]);
             int horizontalPosition = 1;
             int treeCounter = 0;
             for (int verticalPosition = 0; verticalPosition < inputs.Count; verticalPosition ++) {


             	int characterPositionToCheck = ((verticalPosition * 3) % 31);
                            if (inputs[verticalPosition][characterPositionToCheck].Equals('#')) {
       treeCounter ++;
       }



             }


       Console.WriteLine(treeCounter);
    }
  }
    ```

  Now to the second puzzle. It seems that I have to vary the for parameters.

  I think I could make an abstraction of the function because it's used 5 times, but since I'm not sure about how to do the last part, I finally chose just to make 5 times the same code with the tweaks. And it was correct! Yay!

    ```

               Console.WriteLine("FirstSlope");
             int firstTreeCounter = 0;
             for (int verticalPosition = 0; verticalPosition < inputs.Count; verticalPosition ++) {
             	int characterPositionToCheck = (verticalPosition % 31);
                            if (inputs[verticalPosition][characterPositionToCheck].Equals('#')) {
       firstTreeCounter ++;
       }     
             }
       Console.WriteLine(firstTreeCounter);
       Console.WriteLine("SecondSlope");
             int secondTreeCounter = 0;
             for (int verticalPosition = 0; verticalPosition < inputs.Count; verticalPosition ++) {
             	int characterPositionToCheck = ((verticalPosition * 3) % 31);
                            if (inputs[verticalPosition][characterPositionToCheck].Equals('#')) {
       secondTreeCounter ++;
       }     
             }
       Console.WriteLine(secondTreeCounter);
             Console.WriteLine("ThirdSlope");
             int threeTreeCounter = 0;
             for (int verticalPosition = 0; verticalPosition < inputs.Count; verticalPosition ++) {
             	int characterPositionToCheck = ((verticalPosition * 5) % 31);
                            if (inputs[verticalPosition][characterPositionToCheck].Equals('#')) {
       threeTreeCounter ++;
       }     
             }
       Console.WriteLine(threeTreeCounter);
             Console.WriteLine("ForthSlope");
             int forthTreeCounter = 0;
             for (int verticalPosition = 0; verticalPosition < inputs.Count; verticalPosition ++) {
             	int characterPositionToCheck = ((verticalPosition * 7) % 31);
                            if (inputs[verticalPosition][characterPositionToCheck].Equals('#')) {
       forthTreeCounter ++;
       }     
             }
       Console.WriteLine(forthTreeCounter);
                    Console.WriteLine("FifthSlope");
             int fifthTreeCounter = 0;
             for (int verticalPosition = 0; verticalPosition < inputs.Count; verticalPosition +=2) {
             	int characterPositionToCheck = ((verticalPosition / 2) % 31);
                            if (inputs[verticalPosition][characterPositionToCheck].Equals('#')) {
       fifthTreeCounter ++;
       }     
             }
       Console.WriteLine(fifthTreeCounter);
       double total = fifthTreeCounter * forthTreeCounter *threeTreeCounter * secondTreeCounter * firstTreeCounter;
       Console.WriteLine(total);
    }
  }
```

##  Forth Day

Today I do have a mouse and set up the computer properly to clean up the documentation of yesterday (it was a mess with the whole input) and start the new problem.

It seems that we're about of chopping more inputs, and today is more complex. It's the full passport stuff.

In this case in notepad++ I set that I don't like the EOL and extra spaces and that give me a long line that differenciated each subject with two spaces. So I replaced that for a "," and now I have a list of strings I can chop easily.

I wonder which part of that should be programed or not. But it's still done so I think it counts.

![screenshot](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/AdventOfCode2020/Captura002.JPG)

_lots of inputs_

I'm making a function to check the passports static so it can be checked out. Also if I didn't make static it didn't work because, I guess I miss objects instances with this kind of strings?

```

Console.WriteLine("Hello, world!");
Console.WriteLine(inputs[0]);
string passportToCheck = inputs[0];
Console.WriteLine(isValidPassport(passportToCheck));
Console.WriteLine(true);
}
static bool isValidPassport(string passport)
{
if (passport.IndexOf("byr:")== -1)
{
return false;
}
return true;
}


```

Now let's try this

```
int validPasssports = 0;
string passportToCheck = inputs[0];
foreach (string passport in inputs)
{
    if (isValidPassport(passport))
    {
        validPasssports++;
    }
}
Console.WriteLine(validPasssports);
Console.WriteLine(peopleFromTheNorthPole);
}

 static int peopleFromTheNorthPole = 0;

static bool isValidPassport(string passport)
{
if (passport.IndexOf("byr:")== -1)
{
return false;
}
if (passport.IndexOf("iyr:")== -1)
{
return false;
}
if (passport.IndexOf("eyr:")== -1)
{
return false;
}
if (passport.IndexOf("hgt:")== -1)
{
return false;
}
if (passport.IndexOf("hcl:")== -1)
{
return false;
}
if (passport.IndexOf("ecl:")== -1)
{
return false;
}
if (passport.IndexOf("pid:")== -1)
{
return false;
}
if (passport.IndexOf("cid:")== -1)
{
Console.WriteLine("One from the North Pole");
peopleFromTheNorthPole ++;
return true;
}
return true;
}
```

It's not enough so there are some that I'm missing out somehow.I changed the input to use the input from the example. I saw that it was correct and I tried again with the big input. Aaaand it was correct! Maybe I didn't copied it well. Who knows.

So the next part of the problem is more complex and we have to check more things.  

I'll keep this function because it will make easier to filter the passport that miss any field.

I change the name of the function to passportHasAllFields(string passport) to be more clear.

And I think that I need also a static function to look for the substrings for each field and then, sigh, 7 functions for each field.

```

}using System;
using System.Collections.Generic;

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<string>()
       {
---
       };
        Console.WriteLine("Hello, world!");
        Console.WriteLine(inputs[0]);

        int validPasssports = 0;
        string passportToCheck = inputs[0];
        foreach (string passport in inputs)
        {
            if (passportHasAllFields(passport) == false)
            {
                continue;
            }
			if (passportHasBirthYearCorrect(passport) == false)
            {
                continue;
            }
			validPasssports ++;
        }
 Console.WriteLine(validPasssports);
  Console.WriteLine("People from the North Pole: " +peopleFromTheNorthPole);
    Console.WriteLine(getField(inputs[0],"byr:"));
    }

         static int peopleFromTheNorthPole = 0;

   static bool passportHasBirthYearCorrect(string passport)
   {
	   int year = Int32.Parse(getField(passport,"byr:"));
	   if ((year >= 1920) %% (year <= 2002)
	   {
		   return true;
	   }
	   return false;
   }

   static string getField(string passport, string field) {
	   int startOfDataField = passport.IndexOf(field)+4;
	   int endOfDataField = passport.IndexOf(" ",startOfDataField);
	   return passport.Substring(startOfDataField, endOfDataField-startOfDataField);
   }


   static bool passportHasAllFields(string passport)
    {
        if (passport.IndexOf("byr:")== -1)
        {
        return false;
        }
        if (passport.IndexOf("iyr:")== -1)
        {
        return false;
        }
        if (passport.IndexOf("eyr:")== -1)
        {
        return false;
        }
        if (passport.IndexOf("hgt:")== -1)
        {
        return false;
        }
        if (passport.IndexOf("hcl:")== -1)
        {
        return false;
        }
        if (passport.IndexOf("ecl:")== -1)
        {
        return false;
        }
        if (passport.IndexOf("pid:")== -1)
        {
        return false;
        }
        if (passport.IndexOf("cid:")== -1)
        {
      //  Console.WriteLine("One from the North Pole");
        peopleFromTheNorthPole ++;
        }
        return true;
    }

}

```


## Day 5

This puzzle seems more interesting!

I learn that C# doesn't allow something like 2 ^ 3 to make powers of 2. = (

I can try to use Math.Pow and pray. And you need to cast int into double. Siiiigh. I don't like doubles.

This is what I'm trying to do and it doesn't work

```
row =  2^(6-something);

```

if you try

```

row +=  Math.Pow(2,(6-boardingcharacter));

```

It says that 2 is not a double. Sigh. I think is faster to make a for loop for this.

So this is the program for the rows

```

using System;
using System.Collections.Generic;

class Program {
    static void Main(string[] args) {
        var inputs = new List<String>();
        string boardingpass="BBFFBBFRLL";
		int row=0;
        for (int letterToCheck=0; letterToCheck<=6; letterToCheck++)
        {
             Console.WriteLine(boardingpass[letterToCheck]);
            if(boardingpass[letterToCheck].Equals('B'))
			{
				int addingNumber = 1;
				for (int index=0; index<=(5-letterToCheck); index++)
				{
				addingNumber = addingNumber * 2;
				}
				row += addingNumber;
			}
        }
        Console.WriteLine(row);


    }
}
```

Now let's get to the columns and the seatID!

This seems to work:

```

int row=0;

    for (int letterToCheck=0; letterToCheck<=6; letterToCheck++)
    {
        if(boardingpass[letterToCheck].Equals('B'))
  {
    int addingNumber = 1;
    for (int index=0; index<=(5-letterToCheck); index++)
    {
    addingNumber = addingNumber * 2;
    }
    row += addingNumber;
  }
    }
   // Console.WriteLine(row);
    int collumn = 0;
    for (int letterToCheck=7; letterToCheck<=9; letterToCheck++)
    {
        if(boardingpass[letterToCheck].Equals('R'))
  {
    int addingNumber = 1;
    for (int index=0; index<=(8-letterToCheck); index++)
    {
    addingNumber = addingNumber * 2;
    }
    collumn += addingNumber;
  }
    }
//	Console.WriteLine(collumn);
int seatID = ( row * 8 ) + collumn;
//	Console.WriteLine(seatID);
if (seatID > maxSeatID) {
    maxSeatID = seatID;
}

```
And it worked!

Here is the full code (except the input)

```

using System;
using System.Collections.Generic;

class Program {
    static void Main(string[] args) {
        var inputs = new List<String>()
...
        int maxSeatID = 0;

		foreach (string boardingpass in inputs) {
			int row=0;

        for (int letterToCheck=0; letterToCheck<=6; letterToCheck++)
        {
            if(boardingpass[letterToCheck].Equals('B'))
			{
				int addingNumber = 1;
				for (int index=0; index<=(5-letterToCheck); index++)
				{
				addingNumber = addingNumber * 2;
				}
				row += addingNumber;
			}
        }
       // Console.WriteLine(row);
        int collumn = 0;
        for (int letterToCheck=7; letterToCheck<=9; letterToCheck++)
        {
            if(boardingpass[letterToCheck].Equals('R'))
			{
				int addingNumber = 1;
				for (int index=0; index<=(8-letterToCheck); index++)
				{
				addingNumber = addingNumber * 2;
				}
				collumn += addingNumber;
			}
        }
	//	Console.WriteLine(collumn);
		int seatID = ( row * 8 ) + collumn;
	//
		if (seatID > maxSeatID) {
		    maxSeatID = seatID;
		}

		}
		Console.WriteLine(maxSeatID);
    }
}

```

The second part I think of it as a map. I don't really get how is it. So I'm going to make a "map" and take down every seat that I find. Then print the rest.

This is the code:

```
using System;
using System.Collections.Generic;

class Program {
    static void Main(string[] args) {
        var inputs = new List<String>()

        int[,] planeMap = new int[128,8];


		foreach (string boardingpass in inputs) {
			int row=0;

        for (int letterToCheck=0; letterToCheck<=6; letterToCheck++)
        {
            if(boardingpass[letterToCheck].Equals('B'))
			{
				int addingNumber = 1;
				for (int index=0; index<=(5-letterToCheck); index++)
				{
				addingNumber = addingNumber * 2;
				}
				row += addingNumber;
			}
        }
       // Console.WriteLine(row);
        int collumn = 0;
        for (int letterToCheck=7; letterToCheck<=9; letterToCheck++)
        {
            if(boardingpass[letterToCheck].Equals('R'))
			{
				int addingNumber = 1;
				for (int index=0; index<=(8-letterToCheck); index++)
				{
				addingNumber = addingNumber * 2;
				}
				collumn += addingNumber;
			}
        }
	//	Console.WriteLine(collumn);
	//	int seatID = ( row * 8 ) + collumn;
		planeMap[row,collumn]=1;

		}
        for(int i=0; i<=127; i++) {
			for (int j=0; j<7; j++)
			{
				Console.Write(planetMap[i,j]);
			}
			Console.WriteLine(planetMap[i,7]);
		}
	}
}
```

And it gives me a visual impresion of the plane. As the puzzle says there is a 0 in between a lot of 1 and there are rows of 0 at the beginning and at the end. Cool. Now let's iterate diferently = )

![screenshot](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/AdventOfCode2020/Captura003.JPG)

And it works!

```

int[,] planeMap = new int[128,8];


foreach (string boardingpass in inputs) {
int row=0;

for (int letterToCheck=0; letterToCheck<=6; letterToCheck++)
{
    if(boardingpass[letterToCheck].Equals('B'))
{
int addingNumber = 1;
for (int index=0; index<=(5-letterToCheck); index++)
{
addingNumber = addingNumber * 2;
}
row += addingNumber;
}
}
// Console.WriteLine(row);
int collumn = 0;
for (int letterToCheck=7; letterToCheck<=9; letterToCheck++)
{
    if(boardingpass[letterToCheck].Equals('R'))
{
int addingNumber = 1;
for (int index=0; index<=(8-letterToCheck); index++)
{
addingNumber = addingNumber * 2;
}
collumn += addingNumber;
}
}
//	Console.WriteLine(collumn);
//	int seatID = ( row * 8 ) + collumn;
planeMap[row,collumn]=1;

}
for(int i=0; i<=127; i++) {
for (int j=1; j<6; j++)
{
if ((planeMap[i,j] == 0) && (planeMap[i,j-1] == 1) && (planeMap[i,j+1]==1))
{
  int seatID = ( i * 8 ) + j;
  Console.WriteLine(seatID);
}
}

}
}
}

```

## Sixth day

Today is about of getting a string and count how many different letters it has.

I was thinking of using a map, but I think I'm making a string of different letters and count it.


For the input as other days, since c# doesn't pair well with strings with different lines, I use notepad++ and substitute the end of the line (EOL) with spaces. Then spaces differenciates several inputs and double spaces different groups.

This is the code where I write every letter I receive and I exclude the spaces.

```
using System;
using System.Collections.Generic;

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<String>() {
"abc","a b c","ab ac","a a a a","b"};
int questionsAnsweredYes =0;
foreach (string input in inputs){
	for (int i=0; i< input.Length; i++)
	{
	if (input[i].Equals(' ')){
		continue;
	}
		Console.WriteLine(input[i]);
	}
}
    }
}

```


And this program seems to work!

```

using System;
using System.Collections.Generic;

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<String>() {
		"abc","a b c","ab ac","a a a a","b"};
		int questionsAnsweredYes =0;
		foreach (string input in inputs){
			string questionsAnswered = "";
				for (int i=0; i< input.Length; i++)
				{
					if (input[i].Equals(' ')){
						continue;
					}
					if (questionsAnswered.IndexOf(input[i]) == -1)
					{
						questionsAnswered = questionsAnswered +	input[i];
					}
				}
			questionsAnsweredYes += questionsAnswered.Length;
			}
		Console.WriteLine(questionsAnsweredYes);
	}
}

```

Let's try the full input! Works! Yay, now the next part. Ok, it seems that I have to make another approach for this.

This is what I'm going to try:

```

using System;
using System.Collections.Generic;

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<String>() {
		"abc","a b c","ab ac","a a a a","b"};
		int questionsAnsweredYes =0;
		foreach (string input in inputs){
			int start = 0;
			int count = 0;
			int at = 0;
			int end = input.Length;
			var answers = new List<String>();
			while((start <= end) && (at > -1))
			{
				string answer;
				// start+count must be a position within -str-.
				count = end - start;
				at = input.IndexOf(" ", start, count);
				if (at == -1) {
					answer=input.Substring(start);
					answers.Add(answer);

					break;
				}
				else {
					answer=input.Substring(start,at-start);
					answers.Add(answer);

					start = at+1;
				}
				answers.Add(answer);
			}
        string commonAnswer = answers[0];
        foreach (string answer in answers)
		{
		    for (int i =0; i< commonAnswer.Length; i++)
		    {
		        if (answer.IndexOf(commonAnswer[i])==-1)
				 {	     
					commonAnswer = commonAnswer.Remove(i,1);
				 }
		    }
		}
		questionsAnsweredYes += commonAnswer.Length;
	}
Console.WriteLine(questionsAnsweredYes);

}
}


```

And the second part doesn't work. It's too high and I think it's because when I remove characters the index varies. Let's try with a while instead.

```

using System;
using System.Collections.Generic;

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<String>()
		int questionsAnsweredYes =0;
		foreach (string input in inputs){
			int start = 0;
			int count = 0;
			int at = 0;
			int end = input.Length;
			var answers = new List<String>();
			while((start <= end) && (at > -1))
			{
				string answer;
				// start+count must be a position within -str-.
				count = end - start;
				at = input.IndexOf(" ", start, count);
				if (at == -1) {
					answer=input.Substring(start);
					answers.Add(answer);

					break;
				}
				else {
					answer=input.Substring(start,at-start);
					answers.Add(answer);

					start = at+1;
				}
				answers.Add(answer);
			}
        string commonAnswer = answers[0];
        foreach (string answer in answers)
		{
			int i = 0;
			while(i<= commonAnswer.Length)
		    {
		        if (answer.IndexOf(commonAnswer[i])==-1)
				 {	     
					commonAnswer = commonAnswer.Remove(i,1);
				 }
				else {
					i++;
				}
		    }
		}
		Console.WriteLine(commonAnswer);
		questionsAnsweredYes += commonAnswer.Length;
	}
Console.WriteLine(questionsAnsweredYes);

}
}


```

And this gives me a slightly lower number and it works! yay!

## Seventh day

Oh MY.

Ok, I think that this needs a dictionary or something more complex. My idea is this.

Create a dictionary where key: color values: colors inside and a flag boolean if this leads to a shiny gold bag.

First I'm going to build the dictionary. Then iterate it looking for any shiny gold. If I find it, I'll flag them as they lead to a shiny gold bag.

Then I will take all the items that don't have that flag and look in them of the bags that they are flagged as they lead to a shiny gold bag.

If they lead to a color that leads to a shiny gold bag, I'll flag them.

Then I'll compare if the number of colors that lead to a shiny gold bag increases. If it doesn't, that means that we're finished.

Now good luck to me xD

I'm using classes and dictionaries and I feel like this dog:

```
using System;
using System.Collections.Generic;

public class BagType
{
   public string name {get; set;}
   public bool leadsToShinyGoldBag {get; set;}
   public List<string> colorsInside {get; set;}


   public BagType (string code) : this()
   {
       name = code;
   }
   public BagType()
   {
      this.colorsInside = new List<string>();
   }
}

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<String>() {
		"light red bags contain 1 bright white bag, 2 muted yellow bags.","dark orange bags contain 3 bright white bags, 4 muted yellow bags.","bright white bags contain 1 shiny gold bag.","muted yellow bags contain 2 shiny gold bags, 9 faded blue bags.","shiny gold bags contain 1 dark olive bag, 2 vibrant plum bags.","dark olive bags contain 3 faded blue bags, 4 dotted black bags.","vibrant plum bags contain 5 faded blue bags, 6 dotted black bags.","faded blue bags contain no other bags.","dotted black bags contain no other bags."
		};
		Dictionary <string, BagType> bagTypes = new Dictionary<string, Element>();
		foreach (string input in inputs) {
			BagType newBag = new BagType(input.Substring(0,input.IndexOf(" bags"));
			bagTypes.Add(newBag.getName(),newBag);
		}

}


}



```
At least for now it seems to work. And now let's [iterate the dictionary](https://stackoverflow.com/questions/141088/what-is-the-best-way-to-iterate-over-a-dictionary)

and just to test this is the code to make the iteration:

```
foreach(KeyValuePair<string, BagType> entry in bagTypes)
{
Console.WriteLine(entry.Value.name);
}
```

Now let's try to add the contained colours!

This is the first try:

```
using System;
using System.Collections.Generic;

public class BagType
{
   public string name {get; set;}
   public bool leadsToShinyGoldBag {get; set;}
   public List<string> colorsInside {get; set;}


   public BagType (string code) : this()
   {
       name = code;
   }
   public BagType()
   {
      this.colorsInside = new List<string>();
   }
}

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<String>() {
		"light red bags contain 1 bright white bag, 2 muted yellow bags.","dark orange bags contain 3 bright white bags, 4 muted yellow bags.","bright white bags contain 1 shiny gold bag.","muted yellow bags contain 2 shiny gold bags, 9 faded blue bags.","shiny gold bags contain 1 dark olive bag, 2 vibrant plum bags.","dark olive bags contain 3 faded blue bags, 4 dotted black bags.","vibrant plum bags contain 5 faded blue bags, 6 dotted black bags.","faded blue bags contain no other bags.","dotted black bags contain no other bags."
		};
		Dictionary <string, BagType> bagTypes = new Dictionary<string, BagType>();
		foreach (string input in inputs) {

			BagType newBag = new BagType(input.Substring(0,input.IndexOf(" bags")));
			int startOfContainedColors = input.IndexOf(" contain ")+6;
			int count = 0;
			int at = 0;
			int end = input.Length;
			var containedColours = new List<String>();

			while((startOfContainedColors <= end) && (at > -1)){

				count = end - startOfContainedColors;
				at = input.IndexOf("bag", startOfContainedColors, count);
				if (at == -1) {
					break;
				}
			    string containedColour = input.Substring(startOfContainedColors, at-startOfContainedColors);
				containedColours.Add(containedColour);
				startOfContainedColors = at+1;


			}
			newBag.colorsInside = containedColours;
			bagTypes.Add(newBag.name,newBag);
		}
		foreach(KeyValuePair<string, BagType> entry in bagTypes)
{
    Console.WriteLine("Color "+entry.Value.name+". Contained colours:");
    foreach(string colorInside in entry.Value.colorsInside)
    {
        Console.WriteLine(colorInside);
    }
}
}
}
```

It doesn't colect the colors properly. But it collects _something_

![screenshot](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/AdventOfCode2020/Captura004.JPG)

So let's go little by little. If we have a string "no other bags." it means that there is nothing to add. So I change this here and it works.

```
while((startOfContainedColors <= end) && (at > -1)){
    if (input.IndexOf("no other bags.") != -1){
        break;
    }

  count = end - startOfContainedColors;
  at = input.IndexOf("bag", startOfContainedColors, count);
  if (at == -1) {
    break;
  }
    string containedColour = input.Substring(startOfContainedColors, at-startOfContainedColors);
  containedColours.Add(containedColour);
  startOfContainedColors = at+1;

```

This seems to save the colors properly (with a last space)

```
using System;
using System.Collections.Generic;

public class BagType
{
   public string name {get; set;}
   public bool leadsToShinyGoldBag {get; set;}
   public List<string> colorsInside {get; set;}


   public BagType (string code) : this()
   {
       name = code;
   }
   public BagType()
   {
      this.colorsInside = new List<string>();
   }
}

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<String>() {
		"light red bags contain 1 bright white bag, 2 muted yellow bags.","dark orange bags contain 3 bright white bags, 4 muted yellow bags.","bright white bags contain 1 shiny gold bag.","muted yellow bags contain 2 shiny gold bags, 9 faded blue bags.","shiny gold bags contain 1 dark olive bag, 2 vibrant plum bags.","dark olive bags contain 3 faded blue bags, 4 dotted black bags.","vibrant plum bags contain 5 faded blue bags, 6 dotted black bags.","faded blue bags contain no other bags.","dotted black bags contain no other bags."
		};
		Dictionary <string, BagType> bagTypes = new Dictionary<string, BagType>();
		foreach (string input in inputs) {

			BagType newBag = new BagType(input.Substring(0,input.IndexOf(" bags")));
			int startOfContainedColors = input.IndexOf(" contain ")+6;
			int count = 0;
			int at = 0;
			int end = input.Length;
			var containedColours = new List<String>();

			while((startOfContainedColors <= end) && (at > -1)){
			    if (input.IndexOf("no other bags.") != -1){
			        break;
			    }

				count = end - startOfContainedColors;
				at = input.IndexOf("bag", startOfContainedColors, count);
				if (at == -1) {
					break;
				}
				string colorToTrim = input.Substring(startOfContainedColors, at-startOfContainedColors);
			    string containedColour = colorToTrim.Substring(colorToTrim.IndexOf(" ",colorToTrim.IndexOf(" ")+1)+1
				);
				containedColours.Add(containedColour);
				startOfContainedColors = at+1;


			}
			newBag.colorsInside = containedColours;
			bagTypes.Add(newBag.name,newBag);
		}
		foreach(KeyValuePair<string, BagType> entry in bagTypes)
{
    Console.WriteLine("Color "+entry.Value.name+". Contained colours:");
    foreach(string colorInside in entry.Value.colorsInside)
    {
        Console.WriteLine(colorInside);
    }
}
}
}


```

I put it that way with colorToTrim because to do it in just oneliner seemed _TOO MUCH_

Now time to make lists.

In this exercise if a bag cannot contain other colours and is not the Shiny Gold. Then is a color that I don't want to count.  

So I'm making 3 lists.

List of colors that I'm not interested at all (with no other colors inside)
List of colors that I do know that lead to Shiny Gold (starting with shiny gold)
List of colors that I want to look for.

With this I verify that the list is filled properly (at least the second one)

```
foreach(KeyValuePair<string, BagType> entry in bagTypes)
{
if(entry.Key.Equals("shiny gold")){
shinyGoldBags.Add(entry.Value);
continue;
}
}
Console.WriteLine(shinyGoldBags.Count);
}
}

```


I think I don't need 3 list but I can make 2. For now this is how I fill them using the dictionary:

```

List <BagType> bagsToLookFor = new List<BagType>();
List <BagType> shinyGoldBags = new List<BagType>();

foreach(KeyValuePair<string, BagType> entry in bagTypes)
{
if(entry.Key.Equals("shiny gold")){
shinyGoldBags.Add(entry.Value);
continue;
}
if(entry.Value.colorsInside.Count != 0)
{
bagsToLookFor.Add(entry.Value);
}
}
int bagsToLookForCounter = bagsToLookFor.Count;
Console.WriteLine("Done first iteration. Number of Shiny Gold leading colors: "+shinyGoldBags.Count);
Console.WriteLine("Number of bags to look for: "+bagsToLookForCounter);

```

Now it seems that I have to use the .Find method that needs a complex predicate. [This kind of stuff](https://docs.microsoft.com/es-es/dotnet/api/system.collections.generic.list-1.find?view=net-5.0#System_Collections_Generic_List_1_Find_System_Predicate__0__)

![screenshot](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/AdventOfCode2020/Captura005.JPG)

Ok. This doesn't work. It seems that during an iteration you cannot add or remove things from a list you're iterating!

```

using System;
using System.Collections.Generic;

public class BagType
{
   public string name {get; set;}
   public bool leadsToShinyGoldBag {get; set;}
   public List<string> colorsInside {get; set;}


   public BagType (string code) : this()
   {
       name = code;
   }
   public BagType()
   {
      this.colorsInside = new List<string>();
   }
}

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<String>() {
		"light red bags contain 1 bright white bag, 2 muted yellow bags.","dark orange bags contain 3 bright white bags, 4 muted yellow bags.","bright white bags contain 1 shiny gold bag.","muted yellow bags contain 2 shiny gold bags, 9 faded blue bags.","shiny gold bags contain 1 dark olive bag, 2 vibrant plum bags.","dark olive bags contain 3 faded blue bags, 4 dotted black bags.","vibrant plum bags contain 5 faded blue bags, 6 dotted black bags.","faded blue bags contain no other bags.","dotted black bags contain no other bags."
		};
		Dictionary <string, BagType> bagTypes = new Dictionary<string, BagType>();
		List <BagType> bagsToLookFor = new List<BagType>();
		List <BagType> shinyGoldBags = new List<BagType>();
		foreach (string input in inputs) {

			BagType newBag = new BagType(input.Substring(0,input.IndexOf(" bags")));
			int startOfContainedColors = input.IndexOf(" contain ")+6;
			int count = 0;
			int at = 0;
			int end = input.Length;
			var containedColours = new List<String>();

			while((startOfContainedColors <= end) && (at > -1)){
			    if (input.IndexOf("no other bags.") != -1){
			        break;
			    }

				count = end - startOfContainedColors;
				at = input.IndexOf("bag", startOfContainedColors, count);
				if (at == -1) {
					break;
				}
				string colorToTrim = input.Substring(startOfContainedColors, at-startOfContainedColors);
			    string containedColour = colorToTrim.Substring(colorToTrim.IndexOf(" ",colorToTrim.IndexOf(" ")+1)+1
				).Trim();
				containedColours.Add(containedColour);
				startOfContainedColors = at+1;

			}
			newBag.colorsInside = containedColours;
			bagTypes.Add(newBag.name,newBag);
		}
		Console.WriteLine("Done formating the dictionary");
				foreach(KeyValuePair<string, BagType> entry in bagTypes)
{
    if(entry.Key.Equals("shiny gold")){
		shinyGoldBags.Add(entry.Value);
		continue;
	}
	if(entry.Value.colorsInside.Count != 0)
	{
	    bagsToLookFor.Add(entry.Value);
	}
	}
    int bagsToLookForCounter = bagsToLookFor.Count;
		Console.WriteLine("Done first iteration. Number of Shiny Gold leading colors: "+shinyGoldBags.Count);
		Console.WriteLine("Number of bags to look for: "+bagsToLookForCounter);
	bool stopLooking = false;
	while (stopLooking == false){
	    foreach (BagType bag in bagsToLookFor) {
			foreach (BagType goldenBag in shinyGoldBags){
				if(bag.colorsInside.Exists(x => x.Equals(goldenBag.name)))
				{
					Console.WriteLine("Found something"+bag.name+goldenBag.name);
					shinyGoldBags.Add(bag);
					bagsToLookFor.Remove(bag);
				}
			}
		}
		Console.WriteLine("While loop done. We came from "+bagsToLookForCounter+"to "+bagsToLookFor.Count);
		if (bagsToLookFor.Count == bagsToLookForCounter){
		stopLooking = true;
	    }
		bagsToLookForCounter = bagsToLookFor.Count;
	}
    Console.WriteLine("Done iteration. Number of Shiny Gold leading colors: "+shinyGoldBags.Count);
}
}


```

So let's try something different. Maybe using other objects (like the dictionary that I'm not using too much)

Now I realize that the shinyGold does not lead to a shiny gold in the example so I'm counting it down. At the end. xD

```

using System;
using System.Collections.Generic;

public class BagType
{
   public string name {get; set;}
   public bool leadsToShinyGoldBag {get; set;}
   public List<string> colorsInside {get; set;}


   public BagType (string code) : this()
   {
       name = code;
   }
   public BagType()
   {
      this.colorsInside = new List<string>();
   }
}

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<String>() {
		"light red bags contain 1 bright white bag, 2 muted yellow bags.","dark orange bags contain 3 bright white bags, 4 muted yellow bags.","bright white bags contain 1 shiny gold bag.","muted yellow bags contain 2 shiny gold bags, 9 faded blue bags.","shiny gold bags contain 1 dark olive bag, 2 vibrant plum bags.","dark olive bags contain 3 faded blue bags, 4 dotted black bags.","vibrant plum bags contain 5 faded blue bags, 6 dotted black bags.","faded blue bags contain no other bags.","dotted black bags contain no other bags."
		};
		Dictionary <string, BagType> bagTypes = new Dictionary<string, BagType>();
		List <BagType> bagsToLookFor = new List<BagType>();
		List <BagType> shinyGoldBags = new List<BagType>();
		foreach (string input in inputs) {

			BagType newBag = new BagType(input.Substring(0,input.IndexOf(" bags")));
			int startOfContainedColors = input.IndexOf(" contain ")+6;
			int count = 0;
			int at = 0;
			int end = input.Length;
			var containedColours = new List<String>();

			while((startOfContainedColors <= end) && (at > -1)){
			    if (input.IndexOf("no other bags.") != -1){
			        break;
			    }

				count = end - startOfContainedColors;
				at = input.IndexOf("bag", startOfContainedColors, count);
				if (at == -1) {
					break;
				}
				string colorToTrim = input.Substring(startOfContainedColors, at-startOfContainedColors);
			    string containedColour = colorToTrim.Substring(colorToTrim.IndexOf(" ",colorToTrim.IndexOf(" ")+1)+1
				).Trim();
				containedColours.Add(containedColour);
				startOfContainedColors = at+1;

			}
			newBag.colorsInside = containedColours;
			bagTypes.Add(newBag.name,newBag);
		}
		Console.WriteLine("Done formating the dictionary");
				foreach(KeyValuePair<string, BagType> entry in bagTypes)
{
    if(entry.Key.Equals("shiny gold")){
		shinyGoldBags.Add(entry.Value);
		continue;
	}
	if(entry.Value.colorsInside.Count != 0)
	{
	    bagsToLookFor.Add(entry.Value);
	}
	}
    int bagsToLookForCounter = bagsToLookFor.Count;
		Console.WriteLine("Done first iteration. Number of Shiny Gold leading colors: "+shinyGoldBags.Count);
		Console.WriteLine("Number of bags to look for: "+bagsToLookForCounter);
	bool stopLooking = false;
	while (stopLooking == false){
		List <BagType> bagsToChange = new List<BagType>();
	    foreach (BagType bag in bagsToLookFor) {
			foreach (BagType goldenBag in shinyGoldBags){
				if(bag.colorsInside.Exists(x => x.Equals(goldenBag.name)))
				{
					Console.WriteLine("Found something: "+bag.name+" leads to "+goldenBag.name);
					bagsToChange.Add(bag);
					break;
				}
			}
		}
		foreach (BagType bag in bagsToChange) {
				shinyGoldBags.Add(bag);
				bagsToLookFor.Remove(bag);
		}
		Console.WriteLine("While loop done. We came from "+bagsToLookForCounter+"to "+bagsToLookFor.Count);
		if (bagsToLookFor.Count == bagsToLookForCounter){
		stopLooking = true;
	    }
		bagsToLookForCounter = bagsToLookFor.Count;
	}
    Console.WriteLine("Done iteration. Number of Shiny Gold leading colors: "+(shinyGoldBags.Count-1));
}
}


```

Now let's try the big output.

Nah, does not work. Too high. Ah. I didn't count down the gold bag. DUH.

This is the correct code:

```

using System;
using System.Collections.Generic;

public class BagType
{
   public string name {get; set;}
   public bool leadsToShinyGoldBag {get; set;}
   public List<string> colorsInside {get; set;}


   public BagType (string code) : this()
   {
       name = code;
   }
   public BagType()
   {
      this.colorsInside = new List<string>();
   }
}

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<String>() {

		};
		Dictionary <string, BagType> bagTypes = new Dictionary<string, BagType>();
		List <BagType> bagsToLookFor = new List<BagType>();
		List <BagType> shinyGoldBags = new List<BagType>();
		foreach (string input in inputs) {

			BagType newBag = new BagType(input.Substring(0,input.IndexOf(" bags")));
			int startOfContainedColors = input.IndexOf(" contain ")+6;
			int count = 0;
			int at = 0;
			int end = input.Length;
			var containedColours = new List<String>();

			while((startOfContainedColors <= end) && (at > -1)){
			    if (input.IndexOf("no other bags.") != -1){
			        break;
			    }

				count = end - startOfContainedColors;
				at = input.IndexOf("bag", startOfContainedColors, count);
				if (at == -1) {
					break;
				}
				string colorToTrim = input.Substring(startOfContainedColors, at-startOfContainedColors);
			    string containedColour = colorToTrim.Substring(colorToTrim.IndexOf(" ",colorToTrim.IndexOf(" ")+1)+1
				).Trim();
				containedColours.Add(containedColour);
				startOfContainedColors = at+1;

			}
			newBag.colorsInside = containedColours;
			bagTypes.Add(newBag.name,newBag);
		}
		Console.WriteLine("Done formating the dictionary");
				foreach(KeyValuePair<string, BagType> entry in bagTypes)
{
    if(entry.Key.Equals("shiny gold")){
		shinyGoldBags.Add(entry.Value);
		continue;
	}
	if(entry.Value.colorsInside.Count != 0)
	{
	    bagsToLookFor.Add(entry.Value);
	}
	}
    int bagsToLookForCounter = bagsToLookFor.Count;
		Console.WriteLine("Done first iteration. Number of Shiny Gold leading colors: "+shinyGoldBags.Count);
		Console.WriteLine("Number of bags to look for: "+bagsToLookForCounter);
	bool stopLooking = false;
	while (stopLooking == false){
		List <BagType> bagsToChange = new List<BagType>();
	    foreach (BagType bag in bagsToLookFor) {
			foreach (BagType goldenBag in shinyGoldBags){
				if(bag.colorsInside.Exists(x => x.Equals(goldenBag.name)))
				{
					Console.WriteLine("Found something: "+bag.name+" leads to "+goldenBag.name);
					bagsToChange.Add(bag);
					break;
				}
			}
		}
		foreach (BagType bag in bagsToChange) {
				shinyGoldBags.Add(bag);
				bagsToLookFor.Remove(bag);
		}
		Console.WriteLine("While loop done. We came from "+bagsToLookForCounter+"to "+bagsToLookFor.Count);
		if (bagsToLookFor.Count == bagsToLookForCounter){
		stopLooking = true;
	    }
		bagsToLookForCounter = bagsToLookFor.Count;
	}
    Console.WriteLine("Done iteration. Number of Shiny Gold leading colors: "+(shinyGoldBags.Count-1));
}
}


```

### Part 2

Now go the other way arouuuund

So first let's change the bagTypeClass to fit this problem:

```
public class BagType
{
   public string name {get; set;}
   public Dictionary<string, int>() colorsInside {get; set;}
   public BagType (string code) : this()
   {
       name = code;
   }
   public BagType()
   {
      this.colorsInside = new Dictionary<string, int>();
   }
}
```

Then how we fill the dictionary.

The parsing is hell. Did you know that?

```

using System;
using System.Collections.Generic;

public class BagType
{
   public string name {get; set;}
   public Dictionary<string, int> colorsInside {get; set;}
   public BagType (string code) : this()
   {
       name = code;
   }
   public BagType()
   {
      this.colorsInside = new Dictionary<string, int>();
   }
}

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<String>() {
		"light red bags contain 1 bright white bag, 2 muted yellow bags.","dark orange bags contain 3 bright white bags, 4 muted yellow bags.","bright white bags contain 1 shiny gold bag.","muted yellow bags contain 2 shiny gold bags, 9 faded blue bags.","shiny gold bags contain 1 dark olive bag, 2 vibrant plum bags.","dark olive bags contain 3 faded blue bags, 4 dotted black bags.","vibrant plum bags contain 5 faded blue bags, 6 dotted black bags.","faded blue bags contain no other bags.","dotted black bags contain no other bags."
		};
		Dictionary <string, BagType> bagTypes = new Dictionary<string, BagType>();
		foreach (string input in inputs) {

			BagType newBag = new BagType(input.Substring(0,input.IndexOf(" bags")));
			int startOfContainedColors = input.IndexOf(" contain ")+6;
			int count = 0;
			int at = 0;
			int end = input.Length;
			var containedColours = new Dictionary<string, int>();

			while((startOfContainedColors <= end) && (at > -1)){
			    if (input.IndexOf("no other bags.") != -1){
			        break;
			    }

				count = end - startOfContainedColors;
				at = input.IndexOf("bag", startOfContainedColors, count);
				if (at == -1) {
					break;
				}
				string colorToTrim = input.Substring(startOfContainedColors, at-startOfContainedColors);
				int firstSpace = colorToTrim.IndexOf(" ");
			    string containedColour = colorToTrim.Substring(colorToTrim.IndexOf(" ",firstSpace+1)+1
				).Trim();
				int numberOfBags = Int32.Parse(colorToTrim.Substring(firstSpace+1,1).Trim());
				containedColours.Add(containedColour,numberOfBags);
				startOfContainedColors = at+1;

			}
			newBag.colorsInside = containedColours;
			bagTypes.Add(newBag.name,newBag);
		}
		Console.WriteLine("Done formating the dictionary");
}
}


```

It's too late, I cannot do it u.u


Here is what I've done:

```

using System;
using System.Collections.Generic;

public class BagType
{
   public string name {get; set;}
   public Dictionary<string, int> colorsInside {get; set;}
   public BagType (string code) : this()
   {
       name = code;
   }
   public BagType()
   {
      this.colorsInside = new Dictionary<string, int>();
   }
}

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<String>() {
		"light red bags contain 1 bright white bag, 2 muted yellow bags.","dark orange bags contain 3 bright white bags, 4 muted yellow bags.","bright white bags contain 1 shiny gold bag.","muted yellow bags contain 2 shiny gold bags, 9 faded blue bags.","shiny gold bags contain 1 dark olive bag, 2 vibrant plum bags.","dark olive bags contain 3 faded blue bags, 4 dotted black bags.","vibrant plum bags contain 5 faded blue bags, 6 dotted black bags.","faded blue bags contain no other bags.","dotted black bags contain no other bags."
		};
		Dictionary <string, BagType> bagTypes = new Dictionary<string, BagType>();
		foreach (string input in inputs) {

			BagType newBag = new BagType(input.Substring(0,input.IndexOf(" bags")));
			int startOfContainedColors = input.IndexOf(" contain ")+6;
			int count = 0;
			int at = 0;
			int end = input.Length;
			var containedColours = new Dictionary<string, int>();

			while((startOfContainedColors <= end) && (at > -1)){
			    if (input.IndexOf("no other bags.") != -1){
			        break;
			    }

				count = end - startOfContainedColors;
				at = input.IndexOf("bag", startOfContainedColors, count);
				if (at == -1) {
					break;
				}
				string colorToTrim = input.Substring(startOfContainedColors, at-startOfContainedColors);
				int firstSpace = colorToTrim.IndexOf(" ");
			    string containedColour = colorToTrim.Substring(colorToTrim.IndexOf(" ",firstSpace+1)+1
				).Trim();
				int numberOfBags = Int32.Parse(colorToTrim.Substring(firstSpace+1,1).Trim());
				containedColours.Add(containedColour,numberOfBags);
				startOfContainedColors = at+1;

			}
			newBag.colorsInside = containedColours;
			bagTypes.Add(newBag.name,newBag);
		}
		Console.WriteLine("Done formating the dictionary");
		BagType shinyBag = bagTypes["shiny gold"];
		bool stopLooking == false;
		while (stopLooking == false){
			stopLooking=true;
		}

}
}


```

## Eighth Day


Today it seems that can be easier. So let's try to parse. The idea is to make a list including indexes. And when the index is repeated. BLAM.

So first let's parse the input (also easier today. )

This is the first try:

```

using System;
using System.Collections.Generic;

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<String>()
		{
		    "nop +0 ","acc +1 ","jmp +4 ","acc +3 ","jmp -3 ","acc -99 ","acc +1 ","jmp -4 ","acc +6"
		};
	    var indexesVisited = new List<int>();
	    bool stopRunning = false;
		int accessingLine = 0;
		int accumulator = 0;
	    while (stopRunning == false) {
			if (indexesVisited.IndexOf(accessingLine) != -1)
			{
				stopRunning = true;
				break;
			}
			indexesVisited.Add(accessingLine);
			if (inputs[accessingLine].IndexOf("nop") != -1)
			{
				accessingLine++;
				continue;
			}
			int accessingNumber = Int32.Parse(inputs[accessingLine].Substring(inputs[accessingLine].IndexOf(" ")));
			if (inputs[accessingLine].IndexOf("jmp") != -1)
			{
				accessingLine = accessingLine + accessingNumber;
				continue;
			}
			if (inputs[accessingLine].IndexOf("acc") != -1)
			{
				accumulator = accumulator + accessingNumber;
        accessingLine++;
				continue;
			}

	    }
		Console.WriteLine("Accumulator variable: "+accumulator);
    }
}

```

It doesn't work with the example. But at least I can work with it and it doesn't explode!

Time to add lots of Console.WriteLine

And I missed when the index is "acc" that I have to move the accessing line (now corrected in the code so I don't repeat it because it's one line). Will it work?

It does! Yay, only one hour of coding. Yay.

### Second Puzzle

Ooookey. So this is the thing that we have to iterate until we find the changes that makes the loop go over.

So for each instruction we evaluate if its a nop or a jump

If it's exactly a nop +0 we skip (because Jump+0 infinite loop). If it's an acc we skip. Else we test a new list with only that change. (I learned that you cannot change a list while iterating it)

I'm struggling because I think that I don't modify something as I would like to. This is the test code:

```

using System;
using System.Collections.Generic;

class Program {

    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<string>()
		{
		    "nop +0 ","acc +1 ","jmp +4 ","acc +3 ","jmp -3 ","acc -99 ","acc +1 ","jmp -4 ","acc +6"
		};
		var modifiedInputs = new List<string>(inputs);
	    var indexesVisited = new List<int>();
	    bool foundGoodInput = false;
		bool stopRunning;
		int accumulator = 0;
		int changingLine = 0;
		int accessingLine =0;
		while (foundGoodInput == false) {
			if (changingLine == inputs.Count) {
				break;
			}
			if (inputs[changingLine].IndexOf("acc") != -1)
			{
				changingLine++;
				continue;
			}
			int changingNumber = Int32.Parse(inputs[changingLine].Substring(inputs[changingLine].IndexOf(" ")));
			Console.WriteLine("Changing number: "+changingNumber);
			if (changingNumber == 0) {
				changingLine++;
				continue;				
			}
			if (inputs[changingLine].IndexOf("nop") != -1) {
				string changedInput = "jmp " + inputs[changingLine].Substring(inputs[changingLine].IndexOf(" "));
				modifiedInputs[changingLine] = changedInput;
				changingLine++;
			}
			if (inputs[changingLine].IndexOf("jmp") != -1) {
				string changedInput = "nop " + inputs[changingLine].Substring(inputs[changingLine].IndexOf(" "));
				modifiedInputs[changingLine] = changedInput;
				changingLine++;
			}

			stopRunning = false;
	    while (stopRunning == false) {
			Console.WriteLine("accessingLine variable: "+accessingLine);
			if (accessingLine == modifiedInputs.Count) {
				stopRunning = true;
				foundGoodInput = true;
				break;
			}
			if (indexesVisited.IndexOf(accessingLine) != -1)
			{
				stopRunning = true;
				break;
			}
			indexesVisited.Add(accessingLine);
			if (modifiedInputs[accessingLine].IndexOf("nop") != -1)
			{
				accessingLine++;
				continue;
			}

			int accessingNumber = Int32.Parse(modifiedInputs[accessingLine].Substring(modifiedInputs[accessingLine].IndexOf(" ")));

			if (modifiedInputs[accessingLine].IndexOf("jmp") != -1)
			{
				accessingLine = accessingLine + accessingNumber;
				continue;
			}
			if (modifiedInputs[accessingLine].IndexOf("acc") != -1)
			{
				Console.WriteLine("Accumulator variable: "+accumulator);
				accumulator = accumulator + accessingNumber;
				accessingLine++;
				continue;
			}

	    }
		if (foundGoodInput == true){
			break;
		}
		//reseting variables
		accessingLine = 0;
		accumulator = 0;
		modifiedInputs = new List<string>(inputs);

		}
		Console.WriteLine("Accumulator variable: "+accumulator);
    }
}

```

I was forgetting to add the reset of the visitedIndex variable so each time the inner loop was shorter and shorter

This is the code without the debugging:

```

var modifiedInputs = new List<string>(inputs);
    var indexesVisited = new List<int>();
    bool foundGoodInput = false;
  bool stopRunning;
  int accumulator = 0;
  int changingLine = 0;
  int accessingLine =0;
  while (foundGoodInput == false) {
    if (changingLine == inputs.Count) {
      break;
    }
    if (inputs[changingLine].IndexOf("acc") != -1)
    {
      changingLine++;
      continue;
    }
    int changingNumber = Int32.Parse(inputs[changingLine].Substring(inputs[changingLine].IndexOf(" ")));
    if (changingNumber == 0) {
      changingLine++;
      continue;				
    }
    if (inputs[changingLine].IndexOf("nop") != -1) {
      string changedInput = "jmp " + inputs[changingLine].Substring(inputs[changingLine].IndexOf(" "));
      modifiedInputs[changingLine] = changedInput;
      changingLine++;
    }
    if (inputs[changingLine].IndexOf("jmp") != -1) {
      string changedInput = "nop " + inputs[changingLine].Substring(inputs[changingLine].IndexOf(" "));
      modifiedInputs[changingLine] = changedInput;
      changingLine++;
    }

    stopRunning = false;
    while (stopRunning == false) {
    if (accessingLine == modifiedInputs.Count) {
      stopRunning = true;
      foundGoodInput = true;
      break;
    }
    if (indexesVisited.IndexOf(accessingLine) != -1)
    {
      stopRunning = true;
      break;
    }
    indexesVisited.Add(accessingLine);
    if (modifiedInputs[accessingLine].IndexOf("nop") != -1)
    {
      accessingLine++;
      continue;
    }

    int accessingNumber = Int32.Parse(modifiedInputs[accessingLine].Substring(modifiedInputs[accessingLine].IndexOf(" ")));

    if (modifiedInputs[accessingLine].IndexOf("jmp") != -1)
    {
      accessingLine = accessingLine + accessingNumber;
      continue;
    }
    if (modifiedInputs[accessingLine].IndexOf("acc") != -1)
    {
      accumulator = accumulator + accessingNumber;
      accessingLine++;
      continue;
    }

    }
  if (foundGoodInput == true){
    break;
  }
  //reseting variables
  accessingLine = 0;
  accumulator = 0;
  modifiedInputs = new List<string>(inputs);
  indexesVisited = new List<int>();
  }
  Console.WriteLine("Accumulator variable: "+accumulator);

```

Will it work?

It does! Yay!

## Day 9

Today it seems also simple. Just check 1 by one lot's of more/less simple inputs.

Here I have a code where I just store the preamble.

```
using System;
using System.Collections.Generic;

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
		var inputs = new List<String>() {
		"1 ","2 ","3 ","4 ","5 ","6 ","7 ","8 ","9 ","10 ","11 ","12 ","13 ","14 ","15 ","16 ","17 ","18 ","19 ","20 ","21 ","22 ","23 ","24 ","25 ","26 ","70"
		};
		int inputTotal = inputs.Count;
		int checkedInput = 0;
		bool foundIncorrectNumber = false;
		var preamble = new List<int>();
		while ((checkedInput <= inputTotal ) || (foundIncorrectNumber == false)){
			int numberChecked = Int32.Parse(inputs[checkedInput]);
			if (preamble.Count<25){
				preamble.Add(numberChecked);
				checkedInput++;
				continue;
			}
			break;
		}
		Console.WriteLine("IncorrectNumber: "+inputs[checkedInput]);
    }
}

```

And now I realize that I can use some code from the first day with those sums of numbers!

This code seems to work:

```

using System;
using System.Collections.Generic;

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
		var inputs = new List<String>() {
		"1 ","2 ","3 ","4 ","5 ","6 ","7 ","8 ","9 ","10 ","11 ","12 ","13 ","14 ","15 ","16 ","17 ","18 ","19 ","20 ","21 ","22 ","23 ","24 ","25 ","26 ","70"
		};
		int inputTotal = inputs.Count;
		int checkedInput = 0;
		bool foundIncorrectNumber = false;
		var preamble = new List<int>();
		while ((checkedInput <= inputTotal ) && (foundIncorrectNumber == false)){
			int numberChecked = Int32.Parse(inputs[checkedInput]);
			if (preamble.Count<25){
				preamble.Add(numberChecked);
				checkedInput++;
				continue;
			}
			for (var firstNumber = 24; firstNumber >= 0; firstNumber--)
			{
			   for (var secondNumber = firstNumber - 1; secondNumber >= 0; secondNumber--)
				   {
				   if (preamble[firstNumber]+preamble[secondNumber] == checkedInput ){
					preamble.Remove(preamble[0]);
					preamble.Add(numberChecked);
					checkedInput++;
					continue;
				   }
				   }

			}
			foundIncorrectNumber = true;
		}
		Console.WriteLine("IncorrectNumber: "+inputs[checkedInput]);
    }
}

```

So I'm testing with the second example as a test...

Nah, it doesn't work. But this does. Even if it has too much debug

```

using System;
using System.Collections.Generic;

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
		var inputs = new List<String>() {
		};
		int inputTotal = inputs.Count;
		int checkedInput = 0;
		int preambleSize = 25;
		bool foundIncorrectNumber = false;
		var preamble = new List<int>();
		while ((checkedInput <= inputTotal ) && (foundIncorrectNumber == false)){
		    foundIncorrectNumber = true;
			int numberChecked = Int32.Parse(inputs[checkedInput]);
			if (preamble.Count< preambleSize){
				Console.WriteLine("checked input just adding: "+inputs[checkedInput]);
				preamble.Add(numberChecked);
				checkedInput++;
				foundIncorrectNumber = false;
				continue;
			}
			Console.WriteLine("checked input: "+inputs[checkedInput]);
			for (var firstNumber = preambleSize-1; firstNumber >= 0; firstNumber--)
			{

			   for (var secondNumber = firstNumber - 1; secondNumber >= 0; secondNumber--)
				   {
				       Console.WriteLine("first number checking sum: "+preamble[firstNumber]+" second number checking sum: "+preamble[secondNumber]);
				   if (preamble[firstNumber]+preamble[secondNumber] == numberChecked ){
				    preamble = new List<int>();
					for (int i = 0; i<=preambleSize; i++) {
					    preamble.Add(Int32.Parse(inputs[checkedInput-i]));
					}
					checkedInput++;
					foundIncorrectNumber = false;
					break;
				   }
				   }

			}

		}
		Console.WriteLine("IncorrectNumber: "+inputs[checkedInput]);
    }
}

```

### Second part

For this I'm going to consider the solution of the first problem directly. I don't want to process it again.

This is the firs part (with no solution of the part 1 put)

```
int inputTotal = inputs.Count;
int solutionPart1 = NUMBER;
int checkingPosition = inputs.IndexOf(solutionPart1+" ");
var consecutiveSum = new List<int>();
bool foundConsecutiveSum = false;
while (foundConsecutiveSum == false) {
  break;
}


```

And this seems to work, but I noticed that the list is not ordered by size so I have to order it to have the solution

```

using System;
using System.Collections.Generic;

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
		var inputs = new List<String>() {
		};
		int inputTotal = inputs.Count;
		int solutionPart1 = x;
		int checkingPosition = (inputs.IndexOf(solutionPart1+" "))-1;
		var consecutiveNumbers = new List<int>();
		int consecutiveSum = 0;
		bool foundConsecutiveSum = false;
		while (foundConsecutiveSum == false) {

			for(var i= checkingPosition; i>=0; i--)
			{
				int checkingNumber = Int32.Parse(inputs[i]);
				consecutiveSum += checkingNumber;
				if (consecutiveSum < solutionPart1) {
					consecutiveNumbers.Add(checkingNumber);
					continue;
				}
				if (consecutiveSum == solutionPart1) {
					consecutiveNumbers.Add(checkingNumber);
					foundConsecutiveSum = true;
					break;
				}
				if (consecutiveSum > solutionPart1) {
					consecutiveNumbers = new List<int>();
					consecutiveSum = 0;
					checkingPosition--;
					break;
				}
			}
		}
		foreach (int item in consecutiveNumbers){
		    Console.WriteLine(item);
		}
    }
}

```

I could find the max and the min with C# but, in this case I will leave it to excel to do that.


![screenshot](https://raw.githubusercontent.com/d-prieto/davidlearnsunity/main/AdventOfCode2020/Captura006.JPG)


So done!

## Tenth day

When I read this I had a big trouble understanding it. But now it's something like this:

You have an unordered list of numbers. You have to order it and count how many gaps are there of 1 and how many of 3. And multiply both numbers.

So I'm going to order it. Luckily we have list.Sort when the value is comparable. Int are! Yay.

So this is the code. I had to add the value 0 and one 3 to the counter in the end (Because the last gap is between the biggest number and biggest number + 3)

```
using System;
using System.Collections.Generic;

class Program {
    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
		var inputs = new List<int>()
		{};
		inputs.Add(0);
		inputs.Sort();
		int numberOf1gaps = 0;
		int numberOf3gaps = 0;
		for (var index = 0; index < inputs.Count-1; index++)
		{
			if(inputs[index+1]-inputs[index] == 1)
			{
				numberOf1gaps++;
			}
			if(inputs[index+1]-inputs[index] == 3)
			{
				numberOf3gaps++;
			}
		}
		numberOf3gaps++;
		Console.WriteLine("number of 1 gap: "+numberOf1gaps);
		Console.WriteLine("number of 3 gap: "+numberOf3gaps);
		int solution1 = numberOf1gaps * numberOf3gaps;
		Console.WriteLine(solution1);
}}

```

### Second part

Wow, this one I have no idea how to optimize that counting. I'll give it a thought but if I cannot do it I'll leave it be.

## Eleventh Day


I started this but I didn't finished so let's get back on track!

I have problems with the for to make the matrix to keep on working. Here is the code I have by now:

```

using System;
using System.Collections.Generic;

class Program {

	static int howManySeatsAreFullAround (List<string> inputs, int row, int collumn, int gridWidth, int gridHeight)
	{
		Console.WriteLine("Row: "+row+" Column"+collumn);
		int seatsFull =0;
		for (int y = row -1; y <= row +1;y++)
		{
			if (y == -1 || y > gridWidth)
			{
				Console.WriteLine("Y skipped");
				continue;
			}
			for (int x = collumn -1; x <= collumn +1 ; x++ )
			{
				if (x == -1 || x > gridHeight)
				{
					continue;
				}
				if (inputs[y][x].Equals('#')){
					seatsFull++;
				}
			}
		}

		return seatsFull;
	}

    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");    

		var inputs = new List<string>()
		{
		"L.LL.LL.LL ","LLLLLLL.LL ","L.L.L..L.. ","LLLL.LL.LL ","L.LL.LL.LL ","L.LLLLL.LL ","..L.L..... ","LLLLLLLLLL ","L.LLLLLL.L ","L.LLLLL.LL"
		};
		List<string> lastInputs = new List<string>();
		List<string> newInputs = new List<string>(inputs);
		string newRow = "";
		int occupiedSeatCounter = -1;
		int newOccupiedSeatCounter =0;
		int gridWidth = inputs[0].Length-1;
		int gridHeight = inputs.Count;
		Console.WriteLine ("GridWidth" + gridWidth + " GridHeight: "+ gridWidth);
		while (occupiedSeatCounter!=newOccupiedSeatCounter){
			occupiedSeatCounter = newOccupiedSeatCounter;
			newOccupiedSeatCounter =0;
			lastInputs = newInputs;
			newInputs = new List<string>();
			for (int row = 0; row < gridHeight; row ++)
			{
				for (int column = 0; column < gridWidth; column ++)
				{
					switch (lastInputs[row][column])
					{
						case 'L':
							if (howManySeatsAreFullAround(lastInputs, row, column, gridWidth, gridHeight) ==0)
							{
							newRow = newRow + "#";
							newOccupiedSeatCounter ++;
							break;
							}
							newRow = newRow + "L";
							break;
						case '#':
							if (howManySeatsAreFullAround(lastInputs, row, column, gridWidth, gridHeight) >4)
							{
							newRow = newRow + "L";
							break;
							}
							newRow = newRow + "#";
							newOccupiedSeatCounter ++;
							break;
						default:
							newRow = newRow + inputs[row][column];
							break;
					}
				}
				newInputs.Add(newRow);
			}
			Console.WriteLine("Round done, seats occupied: " +newOccupiedSeatCounter);
		}
		Console.WriteLine(newOccupiedSeatCounter);

	}
}

```


## Twelfth Day

I like that twelfth has an f.

So today we have directions. Let's do then a for that checks the letter and the number and does things.

This a short version of that (just with the North command)

```

using System;
using System.Collections.Generic;

class Program {

    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<string>()
		{
		 "N50 ", "E30 "
		};
		int eastDistance = 0;
		int northDistance = 0;
		char directionFacing = 'E';
		foreach (string input in inputs){
			char order = input[0];
			int orderNumber = Int32.Parse(input.Substring(1));
			switch (order)
			{
				case 'N':
					northDistance += orderNumber;
					Console.WriteLine("N"+northDistance);
					break;
				default:
				    Console.WriteLine("not understood");
					break;
			}
		}

		Console.WriteLine("northDistance: "+northDistance);
		Console.WriteLine("eastDistance: "+eastDistance);
		int manhattanDistance = northDistance + eastDistance;
    }
}

```

And working a bit this is the code.

- I had to use Math.Abs to make the last sum.

- I guess that there is kind of enum that made the turning easier. But I didn't get it how to make it circular or fit in the program.

```

using System;
using System.Collections.Generic;

class Program {

    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<string>()
		{

		};
		int eastDistance = 0;
		int northDistance = 0;
		char directionFacing = 'E';
		foreach (string input in inputs){
			char order = input[0];
			int orderNumber = Int32.Parse(input.Substring(1));
			int numberofTurns = 0;
			switch (order)
			{
				case 'N':
					northDistance += orderNumber;
				//	Console.WriteLine("N"+northDistance);
					break;
				case 'S':
					northDistance -= orderNumber;
				//	Console.WriteLine("S"+northDistance);
					break;
				case 'E':
					eastDistance += orderNumber;
				//	Console.WriteLine("E"+eastDistance);
					break;
				case 'W':
					eastDistance -= orderNumber;
				//	Console.WriteLine("W"+eastDistance);
					break;
				case 'F':
					switch (directionFacing)
					{
						case 'N':
							northDistance += orderNumber;
						//	Console.WriteLine("N"+northDistance);
							break;
						case 'S':
							northDistance -= orderNumber;
						//	Console.WriteLine("S"+northDistance);
							break;
						case 'E':
							eastDistance += orderNumber;
						//	Console.WriteLine("E"+eastDistance);
							break;
						case 'W':
							eastDistance -= orderNumber;
						//	Console.WriteLine("W"+eastDistance);
							break;
						default:
						Console.WriteLine("Direction facing not understood");
						break;
					}
					break;
				case 'R':
					numberofTurns = orderNumber / 90;
					for (int i =0; i< numberofTurns; i++)
					{
						switch (directionFacing)
						{
							case 'N':
								directionFacing = 'E';
								break;
							case 'S':
								directionFacing = 'W';
								break;
							case 'E':
								directionFacing = 'S';
								break;
							case 'W':
								directionFacing = 'N';
								break;
							default:
							Console.WriteLine("Direction facing not understood");
							break;
						}
					}
				//	Console.WriteLine("New direction Facing: "+directionFacing);
					break;
				case 'L':
					numberofTurns = orderNumber / 90;
					for (int i =0; i< numberofTurns; i++)
					{
						switch (directionFacing)
						{
							case 'N':
								directionFacing = 'W';
								break;
							case 'S':
								directionFacing = 'E';
								break;
							case 'E':
								directionFacing = 'N';
								break;
							case 'W':
								directionFacing = 'S';
								break;
							default:
							Console.WriteLine("Direction facing not understood");
							break;
						}
					}
					break;
				default:
				    Console.WriteLine("Input not understood");
					break;
			}
		}

		Console.WriteLine("northDistance: "+northDistance);
		Console.WriteLine("eastDistance: "+eastDistance);
		int manhattanDistance = Math.Abs(northDistance) + Math.Abs(eastDistance);
		Console.WriteLine("Manhattan Distance: "+manhattanDistance);
    }
}

```

### Second puzzle

Now things are harder using a waypoint so we have to measure distance and such. Ok.

Oh, no, we don't have to do that kind of HARD math because the waypoint is always relative to the ship. Yay.

This is the code that worked:

```
using System;
using System.Collections.Generic;

class Program {



    static void Main(string[] args) {
        Console.WriteLine("Hello, world!");
        var inputs = new List<string>()
		{
		};
		int eastPosition = 0;
		int northPosition = 0;
		int wayPointEastPosition = 10;
		int wayPointNorthPosition = 1;
		foreach (string input in inputs){
			char order = input[0];
			int orderNumber = Int32.Parse(input.Substring(1));
			int numberofTurns = 0;
			switch (order)
			{
				case 'N':
					wayPointNorthPosition += orderNumber;
				//	Console.WriteLine("N"+wayPointNorthPosition);
					break;
				case 'S':
					wayPointNorthPosition -= orderNumber;
				//	Console.WriteLine("S"+wayPointNorthPosition);
					break;
				case 'E':
					wayPointEastPosition += orderNumber;
				//	Console.WriteLine("E"+wayPointEastPosition);
					break;
				case 'W':
					wayPointEastPosition -= orderNumber;
				//	Console.WriteLine("W"+wayPointEastPosition);
					break;
				case 'F':
				//	Console.WriteLine("Movement vector: "+wayPointEastPosition +"E + N"+ wayPointNorthPosition);
					for (int i= 0; i<orderNumber; i++){
						eastPosition += wayPointEastPosition;
						northPosition += wayPointNorthPosition;
					}
					break;
				case 'R':
					numberofTurns = orderNumber / 90;
					for (int i =0; i< numberofTurns; i++)
					{
						int tempNorthWaypointPosition = wayPointNorthPosition;
						wayPointNorthPosition = -wayPointEastPosition;
						wayPointEastPosition = tempNorthWaypointPosition;
					}
					break;
				case 'L':
					numberofTurns = orderNumber / 90;
					for (int i =0; i< numberofTurns; i++)
					{
						int tempNorthWaypointPosition = wayPointNorthPosition;
						wayPointNorthPosition = wayPointEastPosition;
						wayPointEastPosition = -tempNorthWaypointPosition;

					}
					break;
				default:
				    Console.WriteLine("Input not understood");
					break;
			}
		}

		Console.WriteLine("northPosition: "+northPosition);
		Console.WriteLine("eastPosition: "+eastPosition);
		int manhattanDistance = Math.Abs(northPosition) + Math.Abs(eastPosition);
		Console.WriteLine("Manhattan Distance: "+manhattanDistance);
    }
}
```

For the turns I had to made the drawing to turn vectors properly and use a temporary variable. I don't know if there is a more clever way to do that.
