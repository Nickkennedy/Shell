# Shell
#!/bin/bash
# Prints out file creator
echo "Name: Nicholas Kennedy"
echo "StudentID: 3674937"
echo ""

if [ "$1" == '1' ]
then
	echo "11111111111111111111"
	exit
fi

if [ "$1" == '2' ]
then
	echo "22222222222222222222222"
	exit
fi

if [ "$1" == '3' ]
then
	echo "3333333333333333333"
	exit
fi


if [ $# -eq 0 ]
then
	echo "======================================================"
	echo "No Argument passed in please try from the list below:"
	echo "1: Print the amount of free/occupied memory on the system"
	echo "2: Print the amount of free/occupied on the system"
	echo "3: Print connection infomation of all connected devices"
	echo "4: Print the amount of time the system has been running"
	echo "======================================================"
	echo ""
	exit
fi

# Meminfo will print out data while using grip and a while card will search for memory items
# awk will convert kB to MB
awk '$3=="kB"{$2=$2/1024;$3="MB"} 1' /proc/meminfo | grep "Mem*" | column -t

# Print CPU Cored
echo ""
echo "CPU Cores"
lscpu | grep "^CPU(s)"

# Print current process prioirty
echo ""
echo "Current process priority (Nice Number)"
ps -e -o uid,pid,comm,nice

# Print the number of running process
echo ""
echo "print the total number of processes running"
ps -eo user=|sort|uniq -c |awk '{ print $2 " " $1}' | grep $USER

# number of open files descriptors owned by current user
echo ""
echo "the number of open files descriptors owned by the current user"
lsof | grep $USER | wc -l

echo "======================================="
echo "Max files open"
cat /proc/sys/fs/file-max
#while getopts 'CPU' option; do
#	echo CPU
#	echo Work!!!!
#done
