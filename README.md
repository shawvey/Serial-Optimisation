[中文版项目介绍](https://shawvey.github.io/%E4%BA%94%E7%82%B9%E6%A8%A1%E5%85%B7%E4%BB%A3%E7%A0%81%E7%9A%84%E4%B8%B2%E8%A1%8C%E4%BC%98%E5%8C%96/)
## 5-point stencil code

This code implements a weighted 5-point stencil on a rectangular grid.  The
value in each cell of the grid is updated based on an average of the values in
the neighbouring North, South, East and West cells.

The grid is initialised into a checkerboard pattern, with each square of the
checkerboard being 64x64 pixels. The stencil operation reads from one grid and
writes to a temporary grid.  The stencil is run twice for every iteration, with
the final result being held in the original array.  The results are quantised to
integers in the range [0,255] and output as a binary image file that may be
viewed graphically.

The only output of each run is the runtime of the iteration loop of the program.
Initialisation and output are not timed.

## Building and running the code

1. you have to run the following command to configure environment.

   ```shell
   source env.sh
   ```

2. A simple `Makefile` is provided to build the code using the GCC compiler.  Just
   type `make` to build the code.  A binary named `stencil` is produced on a
   successful build.

3. There are *three* input problems tested, representing different grid sizes.  The
   inputs are all set as command line arguments to the executable in the following
   format:

   ```shell
   ./stencil nx ny niters
   ```

4. The inputs required are:

| nx   | ny   | niters | Command                   | Runtime         |
| ---- | ---- | ------ | ------------------------- | --------------- |
| 1024 | 1024 | 100    | `./stencil 1024 1024 100` | ~ 0.11 seconds  |
| 4096 | 4096 | 100    | `./stencil 4096 4096 100` | ~ 2.88 seconds  |
| 8000 | 8000 | 100    | `./stencil 8000 8000 100` | ~ 10.35 seconds |

## Checking the results

The program will have executed correctly if the output image matches the
provided reference output images with a small tolerance of +/- 1.  A Python
check script is provided to check the values. 

    python check.py --ref-stencil-file stencil_1024_1024_100.pgm --stencil-file stencil.pgm

If any errors are found, the script can be rerun with the addition of the
`--verbose` flag to provide information about where the errors occur in the
grid.

The reference input files for the different problems are named:

| nx   | ny   | niters | Reference file              |
| ---- | ---- | ------ | --------------------------- |
| 1024 | 1024 | 100    | `stencil_1024_1024_100.pgm` |
| 4096 | 4096 | 100    | `stencil_4096_4096_100.pgm` |
| 8000 | 8000 | 100    | `stencil_8000_8000_100.pgm` |

