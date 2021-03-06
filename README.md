# Ice-Programming-Language


## Honors and Awards

This was a project made at the MLH Hacathon hths.hacks() that won.
The link to the devpost is here: https://devpost.com/software/ice-programming-language

## Inspiration
I recently started programming in low-level languages like C and C++ recently which is completely what I am not used as I program in intermediate to high level languages like Java, JavaScript, and Python. This project required hours of research to understand for the day of the hackathon and during the hackathon. I recently became fed-up with C, although its really simple, it just took so many lines and characters to do simple programs. During the empty and cold streets due to COVID-19 this idea froze like ice in my head and so I started to create my own programming language that would be very basic and still have machine code like performance through a JIT (Just In Time Compiler). I wanted to take all the good from C and make it more modern.

## What it does
This is a minimal scripting language that can be changed without recompilation and still execute machine code. It supports in-built functions like random numbers, user input, and print statements. Not only that but it allows for loops like while loops, and conditional branch statements like if, else, and elif. These are the most important component that make up what and how your program runs and can create high performance machine code that runs the program without the overhead of an interpreter. 

## How I built it
I used the coding back-end library known as LLVM that is useful for JIT and AOT compilation properties. Using this library in C I was able to generate LLVM IR which is a bytecode format like Python bytecode but can be compiled in to executable (AOT) or run executable code on the spot (JIT). Even though I had a useful library  for the back-end, I had to make the front-end which consists of the Tokenizer, Parser, and AST (Abstract Syntax Tree) was needed to be made manually. In C, generic types are non-existent, so I needed to create my own version of dynamic arrays in C in order to complete the tasks that I needed to.
In order to create the Tokenizer which splits up strings like this "a := 2;" into tokens like a, :=, 2, ; which can be used by the parser to create AST nodes. Instead of using a recursive function approach, I decided to use conditional goto statements to avoid compiler function call overhead. Each label that was used represented a different set of grouped tokens or specific type of tokens to be tokenized. Each of these were used in order to generate tokens. To save memory in the program I created a C++ static library, which I have never made before until now, use C++ code in C by using the std::set in order to not create multiple copies of each string that was created by the Tokenizer manually known as String Interning. For the Parser, I split up the parsing method into different statements that would be able to be parsed, for example, parse_binaryexpr to parse stuff like 2 *3 + 4 / 2. Each parsing method returned an AST Node which contains useful information that can be used to generate LLVM IR. Each node was listed in an enum to be used in a switch statement for every type of node that was recursively resolved into LLVM IR. This LLVM IR was then written to bitcode which was then executed by the JIT Compiler lli to run the bytecode with machine code performance.

## Challenges I ran into
I ran into many challenges throughout this hackathon which were linked bugs. For example, I had multiple segmentation faults when I ran my program because I was recursively calling my method to resolve a Literal Type but the code looked right, until I realized after 2 hours that my recursive call on only that method created memory corruption and when separated into a function did not corrupt memory. Solving this issue only led to another, which was a pointer encoding side effect which did not allow me to encode a pointer under a specific type unless I allocated the pointer with malloc. I had a hard time freeing any memory at all in my program, although for a compiler, as long as the references to the memory is not lost it just hogs the memory until after execution. Some of the other bugs that I ran into during the later stages of hacking were implementing in pre-declared methods like printf and rand without knowing whether they would require an implementation or not. Keeping my code clean was hard too, I put comments and notes in my programs to remind myself not to make the same mistakes when doing a function or what to do when I want to execute a specific task.

## Accomplishments that I'm proud of
I am proud of the number of statements that I was able to parse and and compile during this hackathon. I am proud of my ability to apply functions and programs with looking at less documented items in code, for example, looking at a function without documentation and figuring out how to use that function was very helpful in later stages of programming. 

## What I learned
I ended up learning a lot during the programming and became more versed in C and C++, and I would like to learn more about lower level programming and challenge myself with complex memory allocation and pointers. I learned how to use a complex and large library set that I can use in the future for other projects and how test and infer functions and what they do in order use them effectively.

## What's next for Ice Programming Language
I plan on adding functions and recursive function calling, then I may proceed on to custom structure types. After doing these thing, I plan on editing my implementation to make it cleaner and more readable.
