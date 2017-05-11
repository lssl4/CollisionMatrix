# CollisionMatrix

This project was done by Tzi Siong Leong and Jason Chao

The collision matrix project file is mainfileOMPAndMPI.cpp with finalNeighbors.cpp and type.h as the accompanying files.

To compile and run our code use the following commmand lines:

mpic++ -fopenmp -std=c++11 mainfileOMPAndMPI.cpp -o mainfileOMPAndMPI

Our runSch script used for qsub is:

#PBS -l nodes=20:ppn=5
source /etc/bash.bashrc
mpirun mainfileOMPAndMPI data.txt keys.txt 4400 500 0.000001

where mainfileOMPAndMPI is the name of our executable which requires the following command line arguments:
<executable> <data file> <keys file> <data file rows> <data file columns> <dia distance>



Our combined openMP and MPI column wise matrix collisions program was implemented with the master and slave program structure in mind. This means that the master process (set as the process with rank 0) distributes the data columns to the different processes to generate the blocks for those columns. After the processes are done generating the blocks, the blocks are sent as an array to the master process where it pushes each block to the collision hashmap called collisionTable. This design tries to distribute work uniformly by distributing equal number of columns to each process. If the number of processes generated are not divisible by the number of columns in the data, it will keep decreasing the number of processes used until it finds the greatest common factor of the number of processes to work with the data columns.
