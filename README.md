ZEC: Mining statistically-solid k-mers for accurate NGS error correction

The paper has been published in BMC Genomic at https://rdcu.be/be2c5

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

(Included dependent libraries)<br>
Boost library (http://www.boost.org)<br>
Google sparsehash (https://code.google.com/p/sparsehash)<br>
klib (https://github.com/attractivechaos/klib)<br>
KMC (http://sun.aei.polsl.pl/REFRESH/index.php?page=projects&project=kmc&subpage=about)<br>
murmurhash3 (https://code.google.com/p/smhasher)<br>
zlib (http://zlib.net)<br>
pigz (http://zlib.net/pigz)<br>

--------------------------------------------------
How to Install ZEC 
--------------------------------------------------
Type make.

--------------------------------------------------
How to Run ZEC 
--------------------------------------------------
Single-end reads or merged paired-end reads
> ./zec -read &#60;fastq&#62; -prefix &#60;output prefix&#62; -kmerlength &#60;k-mer length&#62;<br>
&#60;fastq&#62;        : fastq file name<br>
&#60;output prefix&#62;: &#60;output directory name&#62;/&#60;file prefix&#62;<br>
&#60;k-mer length&#62; : k-mer length (odd number)<br>

Paired-end reads<br>
> ./zec -read1 &#60;forward fastq&#62; -read2 &#60;reverse fastq&#62; -prefix &#60;output prefix&#62; -kmerlength &#60;k-mer length&#62;<br>
&#60;forward fastq&#62;: first read file of a paired-end fastq file<br>
&#60;reverse fastq&#62;: second read file of a paired-end fastq file<br>
&#60;output prefix&#62;: &#60;output directory name&#62;/&#60;file prefix&#62;<br>
&#60;k-mer length&#62; : k-mer length (odd number)<br>

Run zec with no option to see the entire options.<br>

Running ZEC on multiple nodes using MPI<br>
Launch single process on a node and bind the processes to their nodes
Ex) MPICH 3.1.3 Hydra Version<br>
> mpirun -ppn 1 -bind-to board ./zec &#60;options&#62;

--------------------------------------------------
Choosing k-mer length
--------------------------------------------------
Our empirical analysis shows that the k value that satisfies the following two conditions usually generates the results close to the best one:
1) Ns / 4^k &#60;= 0.0001 where Ns represents the number of unique solid k-mers (ZEC reports Ns).
2) Number of corrected bases becomes the maximum at the chosen k value, which means you need to increase k as long as the number of corrected reads increases.

--------------------------------------------------
Bug Reports:
--------------------------------------------------
Dr. Zhao &#60;s080011 AT e.ntu.edu.sg&#62;
