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
