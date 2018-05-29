ZEC: Mining statistically-solid k-mers for accurate NGS error correction

ZEC is developed based on the BLESS, which is developed by ESCAD Group, Computational Comparative Genomics Lab, and IMPACT Group in Univsersity of Illinois at Urbana-Champaign

--------------------------------------------------
System Requirements
--------------------------------------------------
Compiling ZEC requires MPI libraries. The latest version of ZEC was tested
with GCC 4.9.2, MPICH 3.1.3 (or OpenMPI 1.8.2).

--------------------------------------------------
Dependency
--------------------------------------------------
MPI: tested using MPICH 3.1.3 and OpenMPI 1.8.4

(Included dependent libraries)
Boost library (http://www.boost.org)
Google sparsehash (https://code.google.com/p/sparsehash)
klib (https://github.com/attractivechaos/klib)
KMC (http://sun.aei.polsl.pl/REFRESH/index.php?page=projects&project=kmc&subpage=about)
murmurhash3 (https://code.google.com/p/smhasher)
zlib (http://zlib.net)
pigz (http://zlib.net/pigz)

--------------------------------------------------
How to Install ZEC 
--------------------------------------------------
Type make.

--------------------------------------------------
How to Run ZEC 
--------------------------------------------------
Single-end reads or merged paired-end reads
> ./zec -read <fastq> -prefix <output prefix> -kmerlength <k-mer length>
<fastq>        : fastq file name
<output prefix>: <output directory name>/<file prefix>
<k-mer length> : k-mer length (odd number)

Paired-end reads
> ./zec -read1 <forward fastq> -read2 <reverse fastq> -prefix <output prefix> -kmerlength <k-mer length>
<forward fastq>: first read file of a paired-end fastq file
<reverse fastq>: second read file of a paired-end fastq file
<output prefix>: <output directory name>/<file prefix>
<k-mer length> : k-mer length (odd number)

Run zec with no option to see the entire options.

Running ZEC on multiple nodes using MPI
Launch single process on a node and bind the processes to their nodes
Ex) MPICH 3.1.3 Hydra Version
> mpirun -ppn 1 -bind-to board ./zec <options>

--------------------------------------------------
Choosing k-mer length
--------------------------------------------------
Our empirical analysis shows that the k value that satisfies the following two conditions usually generates the results close to the best one:
1) Ns / 4^k <= 0.0001 where Ns represents the number of unique solid k-mers (ZEC reports Ns).
2) Number of corrected bases becomes the maximum at the chosen k value, which means you need to increase k as long as the number of corrected reads increases.

--------------------------------------------------
Bug Reports:
--------------------------------------------------
Dr. Zhao <s080011@e.ntu.edu.sg>
