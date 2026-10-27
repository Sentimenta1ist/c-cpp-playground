# University Training: C, C++ and Java Exercises

A collection of early programming exercises: SFML graphics, a console word game, pthreads synchronization, Makefile builds, a sorting benchmark and Codewars katas.

Year: 2019-2020 · Stack: C, C++ (SFML), Java, pthreads, Make, CMake · Context: university coursework (KPI), self-study exercises and a course project

## What's inside

- `WorkWithSortAlgorithm/` - course work "Data Structures and Algorithms": benchmarks selection sort, a 4-way selection sort variant and quicksort on a 3D array (`P=3` layers of `M=15` x `N=10`), sorting columns by their sums; `array_sort.c` vs `vector_sort.c`, timing in `measurement.c`, console menu in `menu.c`, CMake build.
- `MultithreadingOnC/` - six pthreads (producer, consumer and others) sharing a linked-list queue (`queue.h`), coordinated with a mutex, a semaphore, a condition variable and a barrier (`thread.h`, `base.h`).
- `WorkWithMakeFiles/с/` (the folder name is a Cyrillic letter) and `WorkWithMakeFiles/java/` - the same matrix task written in C and in Java, each with a hand-written `Makefile` and `test.sh`. The C version takes `-d` (debug trace) and the matrix size as arguments.
- `LetterOnSfml/` - a letter drawn from SFML rectangles and convex shapes, in 2D and a pseudo-3D version, movable with the keyboard, with console menus for background and letter color (Windows only: `windows.h`, `conio.h`).
- `MiniGraphOnSfml/` - plots the catenary family `y = -a*cosh(x/a)` for a = 1, 2, 4 ... 512 with hand-drawn axes and tick marks; Z/X zoom the view. It loads `HelveticaThinItalic.ttf`, which is not in the repo.
- `MiniGameInCons/` - a console "words" (hangman-style) game: 10 words, 15 points, a correct letter reveals its dashes, a wrong guess costs a point.
- `SomeTasksCodewars/` - about 700 lines of Codewars solutions in C++ (many commented out), e.g. a regex-based `numberFormat` for thousands separators.

## Interesting bits

- `MultithreadingOnC/thread.h`: the producer backs off with a growing `usleep` delay when the queue is full, and threads use `pthread_mutex_trylock` plus `sem_trywait` instead of blocking; atomics come from GCC `__sync_*` builtins.
- `WorkWithSortAlgorithm/array_sort.c`: columns are sorted using a precomputed vector of column sums as the key vector, and each swap exchanges whole columns.
- `WorkWithSortAlgorithm/measurement.h`: timing uses 28 runs, discards the first 2 and the 3 smallest and 3 largest, then averages the rest.
- `WorkWithMakeFiles/с/task.c`: finds the first maximum and the last minimum on the minor diagonal and swaps them; debug mode prints the diagonal and each search step.

## Run

Verified in this container (Linux, gcc/g++, JDK):

```
cd WorkWithMakeFiles/с && make && ./main -d 7
cd MultithreadingOnC && gcc -o threads main.c -lpthread && ./threads
cd WorkWithSortAlgorithm && gcc -o sort *.c -lm && ./sort     # starts, shows intro and menu
cd WorkWithMakeFiles/java && make && java -jar main.jar
```

The SFML programs (`LetterOnSfml`, `MiniGraphOnSfml`) were not re-tested: they need SFML, and the first one needs Windows.

## Note

Written in 2019-2020, before AI coding assistants. Kept as-is for history.
