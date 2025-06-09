# Cursed code
Basically a bunch of code snippets for ~~esoteric~~ programming languages I use like [><>](https://esolangs.org/wiki/Fish), [Befunge-93](https://esolangs.org/wiki/Befunge), [brainfuck](https://esolangs.org/wiki/brainfuck), [Python](https://en.wikipedia.org/wiki/Python_(programming_language)), [URCL](https://github.com/ModPunchtree/URCL/blob/main/Release/URCL%20V1.5.0/URCL%20V1.5.0.md), and more.

--------------------------------------------------------

## Language list
- [><>](#fish) - A better version of Befunge-93 that I actually use.
- [brainf***](#brainf) --- This one speaks for itself.
- [Befunge-93](#befunge-93) --- Not really used.
- [URCL](#urcl) --- Just started today 2024/06/28 lol.
- [Python](#python) --- Used to make generators and stuff.
- [+Output](-output) --- Added 2025/02/19, my own (and most practical) esolang. Also 2D

## Fish
*The title of this header is not correct because of technical limitations. The correct title is actually* **><>**.

### Snippet list
- [The Arse Game???](#the-arse-game) - This sucks, live input isn't even supported on [suppen.no](https://suppen.no/fishlanguage).
- [Input loop](#input-loop) - Takes all input until no more.
- [Output loop](#output-loop) - Outputs everything until a `0` is reached.
- [Input + output loop (combined example)](#input--output-loop-combined-example) - A "cat program".
- [Stack clearer](#stack-clearer) - Deletes everything until a `0` is reached.
- [Cat program](#cat-program) - A better version and not just an [Input and output loop](#input--output-loop-combined-example) combined.
- [Even or odd](#even-or-odd) - Checks if the input is even or odd.
- [Even or odd (pretty version)](#even-or-odd-pretty-version) - Checks if the input is even or odd, but actually outputs something.
- [Number guessing game](#number-guessing-game-1-3) - Guess 1, 2, or 3 and the program will tell you if you're right or not.
- [Calculator v1](#calculator-v1) - A 4 function calculator in Polish Notation for some reason (Reverse Polish Notation is better).
- [Calculator v2](#calculator-v2)
- [Calculator v2 2](#calculator-v2-2) - Basically the same as [Calculator v2](#calculator-v2)
- [Deadfish interpreter](#deadfish-interpreter) - Interprets [Deadfish](https://esolangs.org/wiki/Deadfish) code provided from input.
- [Lol](#lol) - I have no idea why I made this.
- [Text reverser](#text-reverser) - Reverses text. What did you expect?
- [Char value adder](#character-value-adder) - Takes a string and adds each character's Unicode values and outputs the sum as a number.

### The Arse Game???
Notes: This sucks because the interpreter I use (which is like the only good one and is the one at [suppen.no](https://suppen.no/fishlanguage)) doesn't have prompting for input, only predefined.

Description: The entire program is just outputting text and the occasional `i` and `?` command.

```
"The ><> Arse Game"v For all of these, use
vooooooooooooooooor< interpret as array
>ao"Episode 1: Attempting the Arrest"v
v oaoooooooooooooooooooooooooooooooor<
>"Start? (0: no; 1: yes)"v
v oooooooooooooooooooooor<
>i?v;
v  <
>aaaooo "F: Oh no! OE is robbing the bank!"v
v        ooooooooooooooooooooooooooooooooor<
>ao"F: What should I do? (0: do nothing; 1: get backup)"v
v   ooooooooooooooooooooooooooooooooooooooooooooooooooor<
>iao?v"OE: Ahh, that sweet sweet money."v
      voooooooooooooooooooooooooooooooor<
      >ao"OE: That was so easy."v
     voaoaooooooooooooooooooooor<
     > "FAIL!"a"Wow, you just let him steal ~200k? Damn."v
       ;ooooo o oooooooooooooooooooooooooooooooooooooooor<
```

### Input loop
Notes: Leaves stack with the input and a `0` on the bottom.

Explanation: Takes a character and duplicates it. Then it checks it to see if it's `-1`. If it is, that means it's the end of input. Checking pops the input, which is why it gets duplicated. The `1+` at the end replaces the ending `-1` with a `0` and reverses the stack so the input is on the stack the same way it was provided.


22 bytes (goes left at end)
```
>i:01-=?v00.
     r+1<
```

25 bytes (right)
```
>i:01-=?v00.
        >1+r
```

12 bytes (by itself, leaves `-1` on stack)
```
>i:01-=?v00.
```

-2 (10 bytes) (leaves `-1`)
```
>i:0(?v00.
```

-3 (7 bytes) if you don't need the `00.`
```
>i:0(?v
```

22 bytes (right)
```
>i:0(?v00.
      >1+r
```

18 bytes (left)
```
>i:0(?v00.
   r+1<
```

### Output loop
Notes: Ends loop once it hits a `0`. If there is no `0` on the stack, well get ready for a very descriptive error message.

Description: Outputs everything on the stack as Unicode characters until the loop hits a `0`.

Explanation: On every iteration, the top item is duplicated and outputted. It is then checked (which is why it's duplicated) to see if it is `0`. If it is, then the loop ends; otherwise it continues.

12 bytes
```
>:o?v;
^   <
```

9 bytes (-3 and uses one line)
```
>:o?!;00.
```

-3 (6 bytes) if you don't need the `00.`
```
>:o?!;
```

### Input + output loop (Combined example)
Description: Aka, a cat program.

Really bad version (49 bytes)
```
>i:01-=?v00.
        >1+r>:o?v;
            ^   <
```

Good version (28 bytes)
```
>i:0(?v00.
v  r+1<
>:o?!;02.
```

### Stack clearer
Notes: Deletes everything until a `0` is hit.

Explanation: Pops and checks if the top item is a `0`. That's it.

12 bytes
```
0r>?v;
  ^ <
```

Version 2 (9 bytes)
```
0r>?!;! <
```

### Cat program
Notes: This has the same functionality as the [Input + output loop](#input--output-loop-combined-example), but is written differently.

Explanation: Takes a character, duplicates it, checks if it's equal to `-1`, and ends if it is. If it's not, output the character and go again.

- New version: Instead of pushing `-1` with `01-=` and seeing if they're equal, the program checks if it's less than `0` with `0(`, saving 2 bytes.

Old input loop (9 bytes)
```
i:01-=?;o
```

New input loop (7 bytes)
```
i:0(?;o
```

### Even or odd
Notes: Remove the `i` command to use the top of the stack. Goes right if even, down if odd.

```
i:n2%?v
```

### Even or odd (pretty version)
Notes: Same thing, but outputs `[number] is even/odd`.

```
i:n2%?v" is even."rooooooooo;
      >" is odd."roooooooo;
```

### Number guessing game (1-3)
Notes: Use the set initial stack (or `-v` in the Python interpreter) to input your guess. Guess either 1, 2, or 3.

```
&"- ><> Number Guessing Game (1-3). Guess either 1, 2, or 3. -"v
v oooooooooooooooooooooooooooooooooooooooooooooooooooooooooooor<
&>1v
>x2>ao=?v":("roo;
 >3^    >"GG"oo;
```

### Calculator v1
Notes: Uses input command (three times) and self-modification. Outputs in the format `Result: <answer>`.

Usage: Enter the three inputs separately. The first one is either `+` (43), `-` (45), `*` (42) or `/` (47). For the second and third inputs click interpret as array.

```
"- ><> Calculator (Enter + - * / and then 2 numbers. No input = -1.) -"rv
v:iooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo<
>"+"=?v:"-"=?v:"*"=?v:"/"=?v aov
     +6+    -9-    *6*    /6/  >"No operation? Alright."v
      7      5      7      8   ;ooooooooooooooooooooooor<
      *      *      *  v-4*<
      >1+    >      >  >37p07.
 ii_&ao~"Result: "roooooooo&n; Do NOT delete the underscore (_)
```

### Calculator v2
Notes: Same thing, but outputs in the format `<num1> <operation> <num2> = <answer>`.

```
"- ><> Calculator (Enter + - * / and then 2 numbers. No input = -1.) -"rv
v:iooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo<
>"+"=?v:"-"=?v:"*"=?v:"/"=?v aov
     +~+    -~-    *~*    /~/  >"No operation? Alright."v
                                ;ooooooooooooooooooooooor<
                           > ii:r:@ aon " ÷ "ooo n " = "ooo r,n;
                    > ii:r:@ aon " • "ooo n " = "ooo r*n;
             > ii:r:@ aon " - "ooo n " = "ooo r-n;
      > ii:r:@ aon " + "ooo n " = "ooo r+n;
```

### Calculator v2 2
Notes: Legit the same thing lol

```
"><> Calculator"v
voooooooooooooor<
>ao"Operation? (+ - * /)"v
v   oooooooooooooooooooor<           ;ooooooor<
>i :"+"=?v :"-"=?v :"*"=?v :"/"=?v~ao"Ok then"^
                                 >ao i:n" / "oooi:n" = "ooo , n;
                         >ao i:n" × "oooi:n" = "ooo * n;
                 >ao i:n" - "oooi:n" = "ooo - n;
         >ao i:n" + "oooi:n" = "ooo + n;
```

### Deadfish interpreter
[Deadfish esolangs.org link](https://esolangs.org/wiki/Deadfish)
Notes: Any invalid command will be skipped. Uses funny teleport thingies (the `.` command)

Explanation (get ready): I’m gonna give you a step by step list cuz that will probably be easier.
1. Takes all the input (all the commands, so if the input is iiiiiiiisio, then it will push each character.)
2. Load 0 into the register
3. Checks for each command
    1. Duplicate the command for checking
    2. Push another of the same character (now you have 2 to compare)
    3. Check if they’re both equal
    4. If they are equal then do that operation, covered below
    5. If not then check for the next one
    6. If not `i`, `d`, `s` or `o` then the program will just skip it
4. Runs that command if it’s valid
    1. i: increment the accumulator by 1
    2. d: decrement the accumulator by 1
    3. s: square the accumulator
    4. o: output the accumulator (as a number, for some reason)
    5. As you can see here, deadfish is absolute dogshit. It doesn’t have input nor character output. (
        Although it's very easily modifiable to do character outputting. Just replace `n` with `o`.)
5. The important step that I may or may not have forgotten before:
    1. Check if the accumulator is either -1 OR 256. If it is, then set it back to zero.
6. **r e p e a t**

253 bytes
```
>i:01-=?v00.
v   &0 r<
> :"i"=?!v~ &1+&v
 v       <
 >:"d"=?!v~ &1-&v
 v       <
 >:"s"=?!v~ &:*&v
 v       <
 >:"o"=?!v~ &:n&v
         ~      > &: 01- =?v f1+:*$:@=?vv
         >l0=?;     v&0 ~  <           <&
                 .21<              .b*45<
```

217 bytes
```
>i:0(?v
v  &0r<
>:"i"=?!v~&1+&v
v       <
>:"d"=?!v~&1-&v
v       <
>:"s"=?!v~&:*&v
v       <
>:"o"=?!v~&:n&v
        ~     >&:01-=?vf1+:*$:@=?vv
        >l?!;   v&0 ~ <          <&
             .21<              .21<
```

185 bytes
```
>i:0(?v
v  &0r<
>:"i"=?!v~&1+&v
v       <
>:"d"=?!v~&1-&v
v       <
>:"s"=?!v~&:*&v
v       <
>:"o"=?!v~&:n&>&:01-=?vf1+:*$:@=?v&12.
        >~l?!;  v&0 ~ <          <
             .21<
```

### Lol
Notes: I have no idea why I made this.

```
"You are so bad you have to use xray to find coal"a01.
 "You are so bad you have to use xray to find stone"a02.
 "I bet you sell feet pics for a living"a03.
 "What do you use?"a04.
 "Pornhub?"a05.
 "Pimbus?"a06.
 "Feetfinder?"a07.
 "Or perhaps all of them?"a0r08.
>:o?!;08.
```

### Text reverser
Notes: Uses input and output, so it's not just the `r` command.

Explanation: Takes all input, DOESN'T reverse the stack and outputs it.

v1
```
0i:01-=?v00.
;v?o:< ~<
 >   ^
```

v2
```
0i:0(?v00.
v?o:<~<;
>31.
```

### [Character Value Adder](https://codegolf.stackexchange.com/questions/30210/calculator-that-adds-char-values)
On Code-golf.

v1 (17 bytes)
```
0i:0(?v+!
   ;n~<
```

## brainf***
### Snippet list
- [I found this in a Truttle1 video](#i-found-this-in-a-truttle1-video)
- [I found this in a Truttle1 video again](#i-found-this-in-a-truttle1-video-again)
- [Hi interpreter](#hi-interpreter)
- [Find a 255 to the left/right](#find-a-255-to-the-leftright)

### I found this in a Truttle1 video
Notes: The video was about [Beatnik](https://youtu.be/Wa1Dh7Ts_IY?si=qRPziMAHWTVP6QVr&t=580) (click for timestamp).

Output: `THANKS FOR WATCHING`

```
-[--->+<]>-.------------.-------.+++++++++++++.---.++++++++.+[--->+<]>++++.+++[->++<]>.+++++++++.+++.--[----->++<]>.---[->+++<]>.+[---->+++<]>-.>-[--->+<]>-.[----->+<]>-.+++++.+.+++++.-------.-[-->+<]>--.
```

### I found this in a Truttle1 video again
Notes: The video was [Burn!?](https://youtu.be/rXtNBj160g8?si=nzu2J3rRio7Go0iK&t=90) (click for timestamp).

Output: `Hello, World!`

```
-[------->+<]>-.-[->+++++<]>++.+++++++..+++.[->+++++<]>+.------------.---[->+++<]>.-[--->+<]>---.+++.------.--------.-[--->+<]>.
```

### Hi interpreter
[Hi esolangs.org link](https://esolangs.org/wiki/Hi)

Notes: Uses all input. End of input MUST be `0`.

Explanation: Calculates length of input (adds one to a counter until the end of input) and outputs "hi" that many times.

```
,[,>+<]++++++++[>>+++++++++++++<<-]>[>.+.-<-]
```

### Find a 255 to the left/right
Notes: Moves the memory pointer left or right until it reaches a cell with 255.

Explanation: Uses the fact that if a cell is `0` a loop will be skipped.

Left:
```
+[-<+]-
```

Right:
```
+[->+]-
```


## Befunge-93
to be added


## +Output
to be added



## URCL
Most of these will be full programs rather than snippets. Also as of tau day 2024 (2024/28/6) I started kinda doing URCL a bit. I made some basic stuff. Also screw you, I use lowercase.

### Program list
Programs on the top are the oldest and get newer as the list goes down. *(#b)* means the amount of bits it's running on (which is the `bits #` in the top).

These programs use the cringe way of outputting text (printing every character separately with `out 20 (char)`).
- [Cringe Hello, world! (8b)](#cringe-hello-world-8b) - Cringe cuz, well look at it.
- [Simple adder (16b)](#simple-adder-16b)
- [Slightly prettified adder (16b)] - takes 2 numbers and prints the sum
- (#slightly-prettified-adder-16b) - Same as the simple adder but shows you what to do (although it's obvious already)

### Cringe Hello, world! (8b)
It's cringe cuz I used a [generator I wrote in](#urcl-text-generator) [Python](#python) xd
```
run rom
bits 8

out 16 72
out 16 101
out 16 108
out 16 108
out 16 111
out 16 44
out 16 32
out 16 119
out 16 111
out 16 114
out 16 108
out 16 100
out 16 33
hlt
```

### Simple adder (16b)
Takes 2 numbers from input via `%numb` and prints the output via `out r3 %numb`
```
run rom
bits 16

in r1 %numb
in r2 %numb
add r3 r1 r2
out %numb r3
hlt
```

### Slightly prettified adder (16b)
Also takes 2 numbers, but actually outputs text asking for them. Prints `(num1) + (num2) = (sum)`.
```
run rom
bits 16

// "first number?\n" and ask for number
out 20 102
out 20 105
out 20 114
out 20 115
out 20 116
out 20 32
out 20 110
out 20 117
out 20 109
out 20 98
out 20 101
out 20 114
out 20 63
out 20 10
in r1 %numb

// out "second number?\n" and ask again
out 20 115
out 20 101
out 20 99
out 20 111
out 20 110
out 20 100
out 20 32
out 20 110
out 20 117
out 20 109
out 20 98
out 20 101
out 20 114
out 20 63
out 20 10
in r2 %numb

// add
add r3 r1 r2

// prettify addition
out %numb r1
out 20 32
out 20 43
out 20 32d
out %numb r2
out 20 32
out 20 61
out 20 32
out %numb r3
out 20 10

hlt
```

## Python
Ok I kinda had to add this at some point. I use it when I stop feeling impractical.

### Snippet list
- [URCL text generator](#urcl-text-generator)

### URCL text generator
A text generator for the URCL programming language.

```py
print(("\n".join([f"out 20 {ord(char)}" for char in input()])) + "\nout 20 10", end="")
```
Prints a newline at the end. Remove `+ "\nout 20 10"` to not do this.