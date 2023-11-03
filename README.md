
# PAV Phase 1

  

## Program Flow

  

We get the active body of the method from the boilerplate code already given, we extract all the `Stmt` using the `getUnits()` method. We then use `BriefUnitGraph`, to get the control  flow of the program, which we use to find the `successor` of each program statement. We store the statement and its successor in a `ProgramPoint` Object.

This gives a list of 	`ProgramPoint` objects, in order of Jimple statements. This list is passed to 
`Kildalls.run(points: points, d0: bot, bot: bot)`, which takes a list of points to run Kildalls on, `d0 `is initial state (initial `LatticeElement`), `bot` LatticeElement. 

The appropriate transfer functions are implemented in `PointsToLatticeElement` which implements `LatticeElements`, which are called from `Kildalls`.

`Kildalls.run` returns `ArrayList<ArrayList<LatticeElements>>` which is the output of each iteration of `Kildalls`.

Kildalls output is used to write the last iteration output to `targetDirectory/tClass.tMethod.output.txt`, all the iterations are printed to file  `targetDirectory/tClass.tMethod.fulloutput.txt`.

The CFG of the program with states at each program point  is printed to the file `targetDirectory/tClass.tMethod.dot`.

Which is then converted to `.png` file with `dot` command in `run-analysis-one.sh`

## Running

We have implemented around ~35 private tests, which reside in the MyTest file. `run-analysis.sh` file calls all of this tests.

### Note: You might get an error related to newline while running `make`.
There might be some newline issues, as we used the Windows Subsystem of Linux for development.

error-related newline might occur if you use our  `run-analysis.sh`  or `Makefile`. so, before running `make`,
please run `dos2unix */*`, it converts Windows newline `CLRF` to unix newline`RF`.

## Transfer functions

We will try to mathematically define all the transfer functions we used, 
Let,
![Screenshot 2023-11-03 212205](https://github.com/khushit-shah/PAVPhase1/assets/42430171/e4c71974-8722-4510-9b96-e38db0b3c14d)
here, newXX is set of all dummy variables that represents allocations sites.
