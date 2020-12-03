1st of December 2020

I heard yesterday about [Advent Of Code](https://adventofcode.com/) So I'm all for it.

I still have to manage a lot in Unity but can be something to manage. I want to do this.

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

Now we have to analize each string and see if there is a miss or if there is a tree. Each time there is going to be in someplace around in the 31 character long (I added a space) String. So the first


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
       "........#..#.##.#.............. ","...#...............#.#......... ","...#..#...#..##....#........... ","...#.............#....#.....#.. ","..#......#..#...#.......#...... ","..............##............... ","#.......#.........#......#....# ",".#.....###.....#...#.#.#...#... ","#.....................#....#.#. ",".......#...................#... ","...#.#...................#....# ","....#....#.......#...#......... ","..##.#............#..#......... ",".....##.#..............##..###. ","...........#....#....#......... ","#.....#...#...#.#.#.#.##.#...#. ",".#...............#....##....... ",".....#..#......#....#.......##. ",".....#........#.......#........ ","...#...##...#..##...#.....##... ",".....#.........#.###...##...#.. ",".#.##...#........#.#.#.#....#.. ","....#......##.#...#.....#....#. ",".......###..........#..#..#.... ","......#...#.##................. ","....#...#...#.........#......#. ",".....#...........#...###....#.. ",".....#...#.#.#....##.#......#.# ","......#...#.....#..#..#........ ","#......#..#...##........###.... ","##.....#....##..#.#.###.#...#.. ","........#....#.......#.....#..# ","#.#.#.##.#.#................... ","..#...##....#......#.....##.... ",".......#.##..#........##..#.... ",".#.#....##......#.#..........#. ","#..............#............#.. ",".#.#.#.#.#.####.#.#...##....... ",".#..#.....##.#.......#.##...#.. ","..#.#........#.............#.#. ","..#.#..........#..#........#... ","..#..#...#.......##...#.#....## ","...#.....#.#.#.....#....#....#. ",".#...#......#.....#..##........ ","...#.......##.#.#.....#......#. ","...........#.....#.#.......#... ","#...........#...#..#.#........# ","....#......#..##........#..###. ",".#..#........................#. ","#.......#......#...#...#..#.... ","....#.#...#..#.#....#....##.#.. ",".....#......#..#..........##.#. ",".#.....#...........#.........#. ","...###.#...#.......#.#......... ",".......#....#..........#..#...# ","......##..#.......#...##....... ","..#..........#.......#......... ","..........#..#..#..#..#........ ",".#.................####...#.#.# ","..##.....#............#........ ","....#.....###...#......#....#.# ","...##.#...........#.##......#.. ","#..##..#..#....#...#..#........ ","......#....#........#.......#.. ","......#.....#......###......... ",".#.....#.#......#.......#...... ","..#.........#..#..#........##.# ","..#.#....#.....#....##....#.#.. ","...#.............##............ ","........#..#..#......#...#..... ",".....#.#...#...##.....#.....#.. ",".#..#.#..........##...##.....#. ","......##.#..........#...#.....# ","#.#.##......#....#..........#.. ","................#.......#.##... ","#.......#.....#.......#....#... ","#..#.....#.##..##...........#.. ",".....#....#.#.##..........#..## ","#.......#.....#.##...........#. ","........#.##........###..#.#... ","........#..................#... ","#.........................#...# ","....#.........#...#.#..#.....#. ",".#............#....#........... ","..#.#...#..##...#.#.......#.... ",".#.#....#...........#.........# ","...#.#..........#.....#...#.... ","......#....#.#...............## ","....##......###...##.##.....##. ","............#.#....#.#.....#..# ",".....#..#.....#.#...###....#... ",".......##....##..#...##..#...## ",".....#.......##..#...#...#....# ","#.........##....#........###.#. ","...#..##...#...#.........#.#.#. ","....#.#.....#.....#............ ","#........#....#..#........#.... ",".......#....#...#.............. ","#...#.........##.....###.#..... ",".#....##..#...#..##.........#.. ","....#.....#......##..#..#....#. ","#.#..#.........#........#...... ","..#.......#.........#.....###.. ","..#..........#...........#....# ","..#...............#......#..#.. ","....#..#...#....###.....#..#..# ","#...#...#..#...........#....#.. ",".#....#.#..#....#.#...........# ",".....#.....#..#....#..#....#... ","#.#..#...........#.#........... ","..................#.#.......#.. ","...#.........#.....#..##....#.. ",".........#.#...#.........##.... ","...#..#....#.....#...#..#...... ",".#.##.....#....#....#......##.. ","##..#.........#.#....#...#..... ","#......#.#...#....#.#..#....... ",".......#.....#.....###....#.#.. ",".#....##.#.....#...#.......#... ",".#.......#..#...#......#..#..## ","...............#...#........... ","#..............#....#.#.#....#. ","...........#..#.......#.##..#.. ","..#......#.#....#...#.#.....#.. ","#.............................. ","#..#....#..........#...#....... ","......#.............#####...... ",".#...###......#.#.#.##..#...... ","............#.##.....#......... ",".........#....##....#.......... ","###....#......#.......#........ ",".#.......##..........#..#....#. ","#..#.....................#....# ","........#...........#.......... ","..#..........#...#..#.........# ","..#..#......##................# ",".....##..#...#..#.............. ",".......#...##..#............... ",".......##..#.####....#....#.#.. ","#.#..#..........#........##.... ","....##....#.#..#....#.#...#.... ","......#.......#...#.....#...#.. ","..#..#...#.....#.......###..... ","...#.......#.#.#.......#.##.... ","...............#..#.#........#. ",".#....###.#......#............. ",".#..#...#....#.#..#.....#...... ",".......#.##....#.#.##.##...#.#. ","..#...#....#.#..##.#.....#...## ","..#...#......#...#......#...#.. ","....#..#...#.#..#......#....... ","#..#...............#......#.##. ",".#....#...#..........#.#.....#. ",".#..#.#.#................#..#.. ",".#....#.#...#..##.###..#...###. ","#.............#.....#.........# ","...#.........#...#.......#..#.. ","......#..#.........#..........# ","........##................#..#. ","......#...#.#.....#......##.... ","...............#...#....#...... ","...#.#..#..#.....##.###..##..#. ",".#....##......#...#..##..#..... ",".....#.........##.##....#...#.. ",".....#.#..................####. ","#.....#...#.............##....# ","#.#..........#...#..#..#....... ","#..#.#.........#............... ","....#...#.........#...##....... ","...........#.....#..##..#...... ","#.....#.......#.#........#..... ","..##..#.....#...##......#...... ","....#....#..................... ","............#......#.........## ",".....##.............#.....##..# ",".......#.............#..#.#.##. ",".###...#......#..#........##.#. ","..#.#...#.#....#.....#..#...... ","..#.#..#.##........#...#....... ","........#.#...............#..#. ","........##.......#...#.......#. ","...#........##.#..........#.#.# ","..#..###.#.#.......#.#......#.. ","....#..........#...#..#........ ","...#..#...#...#.#....#...#..#.. ","...#...#........#......##...#.# ","#...........#..........#..#.##. ","...#..##..................#.#.. ","...##.#...#....#.#...#.####.... ",".....#...#.#.#..#.............. ",".....#..#.#.#..#............... ","..#..#..##...#.#..#.....##....# ",".......#.#..#.....#....#....... ","...#..#....#.........#...#..... ","..............#.#...#...##..... ","...................#........... ",".#......#.#...................# ",".##.....#........#.........#..# ",".##..##...#...................# ","...#....#.#..#.#.#..#.....##... ",".......#..#....#......####.#... ",".##..#..##....#.......#........ ",".#...#...........##............ ",".....#.....#........#.......... ","....##..#....#.....#........... ",".#...#....................#.... ","....#.........#.......##.....#. ",".#....#..#.....#.##....#....... ","....#..#.........#.#....#.#.... ",".......#.........##....#....... ","..#......#....#....#...#....... ","........#..#.......#.##......#. ","..#.....#......#...#..#.......# ","#..#.....##...#...#............ ",".......##.......#........#...#. ","..#......................#...#. ","....##.#.............#......#.. ","#.#............................ ","...##.#.....#.#............#.## ","......#...#..#.........##...... ",".#.......#.....##.......#.#.... ","...........#.#.........#..##... ","...#..........#.##....#........ ","........#..#..#...#....#....#.. ","........##....#.#....#........# ","..#........##....###....#...... ","#................###...#...#... ","................#.#..###......# ","..#.....##.#................#.. ",".....#...............#..#...... ","..#.......####.....#..#.#....## ","..#.....#..#....#.............. ","#.#...........#.#.....#..##.... ","#.#..........#.......#...#.###. ","........#....#...#..#.#........ ",".#.....#......#..#..#..###..#.. ",".#.........#.##.#.#......##.... ","..#.........#...##..#........#. ",".#...................#......... ","...#.#........#................ ","............#.....#..##........ ","..#.....#.#......#.......#...#. ","........#....##..##...#.....##. ",".#........#.#....#.#....#.#..#. ","#.#.......#.................... ",".#..#...##.........#..#........ ",".........#...............#..... ","...#...#.....#......#.......#.. ","###......................#.#..# ","...#.....####........#..#.....# ","#.#...#.#...................##. ",".........#..................... ","#..........##..#.....#....#.... ",".......#...#.#.##.#..##........ ","..........#..#.#..#.#.......#.# ",".....................#.#...#... ","...........#.#........#.#.#.... ",".......#......#........#...#.#. ",".........#....................# ",".##.##....#...#.#.#.#.......... ","#....##..#.##....#....#.......# ",".##.#...#...............#....#. ",".......#...#.###....#.......... ",".....#....#...#..#............. ","#.........#.##....#.#.#........ ","..#...#.............##..#..#... ","#..##.......#..........#...#.#. ",".#..#.....#...........#......#. ","......#......#..............##. ",".#...#..#...#..####.....#.....# ","....##.......#..........##..... ",".#.....#.......#.....#.#...#... ","..#..#..#.#...#......#......... ","......#.#....#........#.......# ","........#.......#.............. ","..#...#.#....#........#.......# ","............#....#...##.#...... ",".........#.............#..#.... ","#.............#.#..##.......#.. ","#....#...........###....#...... ","...#.....................#..... ","....#.#..........#...#.......#. ","......#..#.......#...#...#....# ",".#.#..#.....##.#........#...... ","...........#...#.#............. ","...###............#...#..#..... ","..#.#.......#...#.#..#......... ",".#......##...........#.....#.## ",".....##.....#....##...##.#.#... ","..........#.#.#......#........# ","..#.#........#....##....#.#.... ",".#....#...##...........#....#.. ","##......#...#.......#.......... ",".##...###..#...#......#..##.#.# ","...........##.#..##...#.......# ","..#..............##............ ","........#..#........#...#..#.#. ","..#.............#......#...##.. ","#...##....#...#....#....#.#.... ",".#.#......#..##............#.#. ",".....###.#....##....#....#..... ","#.#.#..........#...#...#.#.#... ",".....#.#...........####........ ",".....#....##...#.##..#......#.. ","#....#.......#.##.......#..#... ",".....#.....#........#.......... ",".......#.......#...#.##......#. ","...#.........##...#.#.#......## ","#........#........#...#..#..... ",".#......#.#......#.#...#....#.. ","#..#....##.....##.............. ","...#.##............#..........# ",".....#.#....#..#.#............# ","..#......#...###.##.......###.. ","........#....#.#.#.#........... ","............#..#........#.....# ","....#...............#.......... ","......#....#....###..#.......## ","#...#...##....#.........#...#.. ","...........#.#.............#... ","...#..#.....#..##.#....#......# ","..#...#..#...#......#.......... ","....#..#....#.......#........#."}; 
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
     
     
     Important: when using char (individual characters) and the method Equals, it's better to use '' instead of "" or it won't work. 
     
     
     And this is the first test
     
     
                 Console.WriteLine(inputs[4].Length);
             Console.WriteLine(inputs[4][31]);
             int horizontalPosition = 35;
             int treeCounter = 0;
             int characterPositionToCheck = (horizontalPosition % 31)  -1;
             if (inputs[1][characterPositionToCheck].Equals('#')) {
       treeCounter++;
       }
       Console.WriteLine(treeCounter);
       
       I had some problems with horizontal position because sometimes it went -1 so I just put a longer formula to get the index through the verticalPosition 
       
       int characterPositionToCheck = ((verticalPosition * 3) % 31);
       
       Aaaaand it worked! here is the snippet
       
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
  
  Now to the second puzle. It seems that I have to vary the for parameters. 

