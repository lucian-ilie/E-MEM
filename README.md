# E-MEM
Efficient Computation of Maximal Exact Matches

##-- DESCRIPTION --

E-MEM is an efficient MEM computation program for large genomes which can be used as a stand alone application or a drop in replacement for MUMmer3. The detailed comparison of E-MEM with other leading programs can be found in E-MEM paper (Nilesh Khiste and Lucian Ilie).

   USAGE:
   
    e-mem  [options]  < reference >  < query > ...

    [options]    type 'e-mem -h' for a list of options.
    <reference>  reference file with one or more FastA sequences
    <query>      query file with one or more FastA sequences

   OUTPUT:
   
   The E-MEM program prints maximal exact matches on standard output. The output format varies depending on the command line options used. In the default mode 3-column output is printed. The option -b allows printing of matches in both forward and reverse complement directions. Below is the description of the output format with respect to the example included with e-mem program. For each query sequence, the sequence name or ID is reported on the first line followed by a '>' character. The sequence name will be reported even if there are no MEMs found for this sequence. For example, the query sequence in 'Reverse' reports sequence name with no matching MEMs. Note that, for each query sequence, the reverse complemented MEMs immediately follow the forward MEMs. For each match, the 3-columns list the start position in the reference sequence, the start position in the query sequence, and the length of the match respectively. For reverse matches, the positions are reported relative to the reverse query sequence. The option -c is used to report reverse match positions with respect to forward query sequence.
   
             > gi|5524211|gb|AAD44166.1|
               4              1             51
               8              1             51
              12              1             51
              16              1             51
              20              1             51
              24              1             51
              28              1             51
               1              2             50
          > gi|5524211|gb|AAD44166.1| Reverse
                    
The 3-column output is sufficient for reporting matches between one reference sequence and one/more query sequences. For multiple reference sequences, 4-column output is desired. E-MEM provides an option -F to print 4-column output which also prints the reference sequence name/ID for each match. Below is a dummy example of 4-column output. The first column now indicates the name/ID of the reference sequence followed by the 3-column output format as described above.

          > gi|5524211|gb|AAD44166.1|
             ref1                      4              1              51
             ref1                      8              1              51
             ref2                      12             1              51
             ref2                      16             1              51
             ref3                      20             1              51
             ref3                      24             1              51
                          
             
##-- INSTALLATION --

After extracting the files into the desired installation directory,
change to the "e-mem" directory.  Once in this directory, type: "make"

This command will build the e-mem binary. If you see any error messages, please
contact authors.

For sanity test, please execute shell-script run_example. On success, the script
will print "Test passed" as output.


##-- RUNNING E-MEM STANDALONE --

The E-MEM program can be used with fastA files with one or more sequences. The program can be run in both serial and parallel mode. The parallel mode has an advantage in terms of time with respect to serial mode.

The valid set of options for e-mem program are:

Options:

-n	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;match only the characters a, c, g, or t, they can be in upper or in lower case
   
-l	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;set the minimum length of a match. The default length is 50

-b	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;compute forward and reverse complement matches

-r	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;only compute reverse complement matches

-c	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;report the query-position of a reverse complement match relative to the original query sequence

-F	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;force 4 column output format regardless of the number of reference sequence input

-L	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;show the length of the query sequences on the header line

-d	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;set the split size. The default value is 1

-t	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;number of threads. The default is 1 thread

-h &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;show possible options

Apart from the options used in Mummer, we provide two more options. The option -d is used for splitting the sequences into two or more parts.  By default this value is set to 1, which means no splitting. This option with value >1 will reduce the overall memory requirement of the program with some compromise on performance.

The option -t is used for running the program in parallel mode. The default value is set to 1, which means serial mode. This option with value > 1 will reduce overall running time of the program with some compromise on memory.

##-- RUNNING E-MEM WITHIN MUMMER3 --

Mummer3 has many different scripts where one of the key program is MEM computation. In all the scripts, the MEM computation program can be replaced with E-MEM with ease for better performance.

For example, in order to use NUCMER (all-vs-all comparison of nucleotide sequences contained in FastA files) with E-MEM, simply change all the references to mummer (MEM computation program) with e-mem program. In script NUCMER, search for "$BIN_DIR/mummer" and replace it with "< path >/e-mem" where < path > is installation idirectory for e-mem program.

The other important script in MUmmer3 is run-mummer3 (the alignment program). To use this script with E-MEM, simply replace "$bindir/mummer" with "< path >/e-mem" where < path > is e-mem installation directory.

## CITE
If you find E-MEM program useful, please cite the E-MEM paper:

N. Khiste, L. Ilie [E-MEM: efficient computation of maximal exact matches for very large genomes](http://bioinformatics.oxfordjournals.org/content/31/4/509.short) Bioinformatics, 2015

 
