# Basics

## Reading Code

### Comments

Anything starting with two slashes or between `/*` and `*/` are **comments**, lines of code that are ignored by the computer and allow programmers to leave hints or old code without interfering with functioning code.

Ex:

    // Command *autonomousCommand;
    //static bool twistPID_Enabled;
    /*static Elevator* elevator;
    static Pneumatics* pneumatics;
    static Elevator2* elevator2;
    */

### Variables

**Variables** have three main parts: their **type**, **name**, and **value**. An example is below:

    float FLSetPoint = 0;
    type |   name    | value

A `type` refers to what kind of data the variable is; some universal types include `bool` (short for "boolean", which can be `true` or `false`), `number` (like the number `1`), or `string` (which are words, like `'1'`), but you can also use types that are declared from other files (like `OI` and `DriveTrain` in the code above).

The `name` of the variable is what it sounds like; variables must be referred to by their exact name in order to be used.

The `value` of a variable is optional, and this leads to two steps to using variables. A variable must be **declared**, which causes the computer to reserve memory space dedicated to that variable, before its value can be **set**, which causes the computer to "associate" that variable with something.

    float FLSetPoint = 0; // the variable is being declared AND set

    double FLOffset;; // the variable is being declared
    FLOffset = 0; // the variable is being set

### Functions

**Functions** are sections of code that "do a job" - they can receive inputs (aka arguments or parameters) and can give outputs. Functions need to have a `type`, `name`, and `parameters` when they are declared.

Ex:

    type |     function name      |            arguments (4 total)
    void DriveTrain::SetDriveSpeed(float FLSpeed, float FRSpeed, float RLSpeed, float RRSpeed) {
        // applies inversion variables defined in SetSteerSetPoint function
        frontLeftDrive->Set(ControlMode::PercentOutput, FLSpeed * FLInv);
        frontRightDrive->Set(ControlMode::PercentOutput, FRSpeed * FRInv);
        rearLeftDrive->Set(ControlMode::PercentOutput, RLSpeed * RLInv);
        rearRightDrive->Set(ControlMode::PercentOutput, RRSpeed * RRInv);
    }

Everything inside the curly braces (`{}`) is part of the function. Functions do not have accept inputs, such as this one:

    void DriveTrain::InitDefaultCommand() {
        // Set the default command for a subsystem here.
        // SetDefaultCommand(new MySpecialCommand());
    }

Functions are **called/executed** by using the function name followed by open + closed parenthesis (`()`). In the example function `DriveTrain::SetDriveSpeed`, the 4 functions `frontLeftDrive->Set`, `frontRightDrive->Set`, `rearLeftDrive->Set`, and `rearRightDrive->Set` are all being called/executed.

Being able to recognize when you are dealing with a function (something which ends with `()`) versus a variable (something which doesn't end with `()`) is probably the most important thing to keep in mind when attempting to read code - code is read up-to-down and left-to-right, but whenever a second function is called, the computer will "jump" over to that second function and only go "back" to the original function when the second function is resolved.

    float addTwoNumbers(float: number1, float: number2) {                       // line 1
        return number1 + number2;
    }

    float addThreeNumbers(float: number1, float: number2, float: number3) {     // line 5
        float number1and2 = addTwoNumbers(number1, number2);
        return addTwoNumbers(number1and2, number3);
    }

    addThreeNumbers(1, 2, 3);                                                   // line 9

In this example, two functions are declared (`addTwoNumbers` and `addThreeNumbers`), then `addThreeNumbers` is being called at the bottom. The computer will interpret this as the following:

1) It sees `addThreeNumbers` being called on line 9, so it needs to see what `addThreeNumbers` should do.
  
2) It jumps to line 5 for the definition of `addThreeNumbers` and reads that top-down.

3) On line 6, it sees that the variable `number1and2` is equal to the output of function `addTwoNumbers`, so it needs to see what `addTwoNumbers` should do.

4) It jumps to line 1 for the definition of `addTwoNumbers`, then `returns` the value of `number1 + number2` back to `number1and2` on line 6.

5) On line 7, it sees `addTwoNumbers` again, so it has to figure out what that function should do.

6) It jumps back to line 1 for `addTwoNumbers`, then `returns` the value of `number1 + number` back to line 7.

Learning how to jump back and forth between lines to follow along with the computer is one of the trickiest things about reading code. However, much like reading music and figuring out where to go when a song repeats, this skill comes with practice.

### Includes

**Include** statements allow you to take code from other files and use them in the current file. By convention, these are always at the top of the file.

Ex:

    #include "OI.h"
    #include "subsystems/DriveTrain.h"