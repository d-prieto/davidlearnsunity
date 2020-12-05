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
