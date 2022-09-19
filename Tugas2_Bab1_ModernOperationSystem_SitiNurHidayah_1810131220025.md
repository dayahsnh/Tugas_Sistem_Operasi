<img width="279" alt="cover tugas 2" src="https://user-images.githubusercontent.com/74997946/189486878-d112b40b-29a4-4569-849e-7ebd62617689.png">

# 1
# INTRODUCTION

A modern computer consists of one or more processors, some main memory,
disks, printers, a keyboard, a mouse, a display, network interfaces, and various
other input/output devices. All in all, a complex system.oo If every application programmer
had to understand how all these things work in detail, no code would ever
get written. Furthermore, managing all these components and using them optimally
is an exceedingly challenging job. For this reason, computers are equipped with a
layer of software called the operating system, whose job is to provide user programs
with a better, simpler, cleaner, model of the computer and to handle managing
all the resources just mentioned. Operating systems are the subject of this
book.
Most readers will have had some experience with an operating system such as
Windows, Linux, FreeBSD, or OS X, but appearances can be deceiving. The program
that users interact with, usually called the shell when it is text based and the
GUI (Graphical User Interface)—which is pronounced ‘‘gooey’’—when it uses
icons, is actually not part of the operating system, although it uses the operating
system to get its work done.
A simple overview of the main components under discussion here is given in
Fig. 1-1. Here we see the hardware at the bottom. The hardware consists of chips,
boards, disks, a keyboard, a monitor, and similar physical objects. On top of the
hardware is the software. Most computers have two modes of operation: kernel
mode and user mode. The operating system, the most fundamental piece of software,
runs in kernel mode (also called supervisor mode). In this mode it has complete access to all the hardware and can execute any instruction the machine is
capable of executing. The rest of the software runs in user mode, in which only a
subset of the machine instructions is available. In particular, those instructions that
affect control of the machine or do I/O )Input/Output" are forbidden to user-mode
programs. We will come back to the difference between kernel mode and user
mode repeatedly throughout this book. It plays a crucial role in how operating systems
work.

<img width="408" alt="figure 1 1" src="https://user-images.githubusercontent.com/74997946/189487967-e4f6e685-40d4-4cbb-ba1e-b71c6bf6682d.png">


The user interface program, shell or GUI, is the lowest level of user-mode software,
and allows the user to start other programs, such as a Web browser, email
reader, or music player. These programs, too, make heavy use of the operating system.
The placement of the operating system is shown in Fig. 1-1. It runs on the
bare hardware and provides the base for all the other software.
An important distinction between the operating system and normal (usermode)
software is that if a user does not like a particular email reader, he† is free to
get a different one or write his own if he so chooses; he is not free to write his own
clock interrupt handler, which is part of the operating system and is protected by
hardware against attempts by users to modify it.
This distinction, however, is sometimes blurred in embedded systems (which
may not have kernel mode) or interpreted systems (such as Java-based systems that
use interpretation, not hardware, to separate the components).
Also, in many systems there are programs that run in user mode but help the
operating system or perform privileged functions. For example, there is often a
program that allows users to change their passwords. It is not part of the operating
system and does not run in kernel mode, but it clearly carries out a sensitive function
and has to be protected in a special way. In some systems, this idea is carried
to an extreme, and pieces of what is traditionally considered to be the operating
† ‘‘He’’ should be read as ‘‘he or she’’ throughout the booksystem (such as the file system) run in user space. In such systems, it is difficult to
draw a clear boundary. Everything running in kernel mode is clearly part of the
operating system, but some programs running outside it are arguably also part of it,
or at least closely associated with it.
Operating systems differ from user (i.e., application) programs in ways other
than where they reside. In particular, they are huge, complex, and long-lived. The
source code of the heart of an operating system like Linux or Windows is on the
order of fiv e million lines of code or more. To conceive of what this means, think
of printing out fiv e million lines in book form, with 50 lines per page and 1000
pages per volume (larger than this book). It would take 100 volumes to list an operating
system of this size—essentially an entire bookcase. Can you imagine getting
a job maintaining an operating system and on the first day having your boss
bring you to a bookcase with the code and say: ‘‘Go learn that.’’ And this is only
for the part that runs in the kernel. When essential shared libraries are included,
Windows is well over 70 million lines of code or 10 to 20 bookcases. And this
excludes basic application software (things like Windows Explorer, Windows
Media Player, and so on).
It should be clear now why operating systems live a long time—they are very
hard to write, and having written one, the owner is loath to throw it out and start
again. Instead, such systems evolve over long periods of time. Windows 95/98/Me
was basically one operating system and Windows NT/2000/XP/Vista/Windows 7 is
a different one. They look similar to the users because Microsoft made very sure
that the user interface of Windows 2000/XP/Vista/Windows 7 was quite similar to
that of the system it was replacing, mostly Windows 98. Nevertheless, there were
very good reasons why Microsoft got rid of Windows 98. We will come to these
when we study Windows in detail in Chap. 11.
Besides Windows, the other main example we will use throughout this book is
UNIX and its variants and clones. It, too, has evolved over the years, with versions
like System V, Solaris, and FreeBSD being derived from the original system,
whereas Linux is a fresh code base, although very closely modeled on UNIX and
highly compatible with it. We will use examples from UNIX throughout this book
and look at Linux in detail in Chap. 10.
In this chapter we will briefly touch on a number of key aspects of operating
systems, including what they are, their history, what kinds are around, some of the
basic concepts, and their structure. We will come back to many of these important
topics in later chapters in more detail.

## 1.1 WHAT IS AN OPERATING SYSTEM?
It is hard to pin down what an operating system is other than saying it is the
software that runs in kernel mode—and even that is not always true. Part of the
problem is that operating systems perform two essentially unrelated functions: providing application programmers (and application programs, naturally) a clean
abstract set of resources instead of the messy hardware ones and managing these
hardware resources. Depending on who is doing the talking, you might hear mostly
about one function or the other. Let us now look at both.
### 1.1.1 The Operating System as an Extended Machine
The architecture (instruction set, memory organization, I/O, and bus structure)
of most computers at the machine-language level is primitive and awkward to
program, especially for input/output. To make this point more concrete, consider
modern SATA (Serial ATA) hard disks used on most computers. A book (Anderson,
2007) describing an early version of the interface to the disk—what a programmer
would have to know to use the disk—ran over 450 pages. Since then, the
interface has been revised multiple times and is more complicated than it was in
2007. Clearly, no sane programmer would want to deal with this disk at the hardware
level. Instead, a piece of software, called a disk driver, deals with the hardware
and provides an interface to read and write disk blocks, without getting into
the details. Operating systems contain many drivers for controlling I/O devices.
But even this level is much too low for most applications. For this reason, all
operating systems provide yet another layer of abstraction for using disks: files.
Using this abstraction, programs can create, write, and read files, without having to
deal with the messy details of how the hardware actually works.
This abstraction is the key to managing all this complexity. Good abstractions
turn a nearly impossible task into two manageable ones. The first is defining and
implementing the abstractions. The second is using these abstractions to solve the
problem at hand. One abstraction that almost every computer user understands is
the file, as mentioned above. It is a useful piece of information, such as a digital
photo, saved email message, song, or Web page. It is much easier to deal with photos,
emails, songs, and Web pages than with the details of SATA (or other) disks.
The job of the operating system is to create good abstractions and then implement
and manage the abstract objects thus created. In this book, we will talk a lot about
abstractions. They are one of the keys to understanding operating systems.
This point is so important that it is worth repeating in different words. With all
due respect to the industrial engineers who so carefully designed the Macintosh,
hardware is ugly. Real processors, memories, disks, and other devices are very
complicated and present difficult, awkward, idiosyncratic, and inconsistent interfaces
to the people who have to write software to use them. Sometimes this is due
to the need for backward compatibility with older hardware. Other times it is an
attempt to save money. Often, however, the hardware designers do not realize (or
care) how much trouble they are causing for the software. One of the major tasks
of the operating system is to hide the hardware and present programs (and their
programmers) with nice, clean, elegant, consistent, abstractions to work with instead.
Operating systems turn the ugly into the beautiful, as shown in Fig. 1-2.

<img width="447" alt="figure 1 2" src="https://user-images.githubusercontent.com/74997946/189487974-dd1c34de-279e-4a5e-9c1e-85a63362ceef.png">

It should be noted that the operating system’s real customers are the application
programs (via the application programmers, of course). They are the ones
who deal directly with the operating system and its abstractions. In contrast, end
users deal with the abstractions provided by the user interface, either a command-
line shell or a graphical interface. While the abstractions at the user interface
may be similar to the ones provided by the operating system, this is not always the
case. To make this point clearer, consider the normal Windows desktop and the
line-oriented command prompt. Both are programs running on the Windows operating
system and use the abstractions Windows provides, but they offer very different
user interfaces. Similarly, a Linux user running Gnome or KDE sees a very
different interface than a Linux user working directly on top of the underlying X
Window System, but the underlying operating system abstractions are the same in
both cases.
In this book, we will study the abstractions provided to application programs in
great detail, but say rather little about user interfaces. That is a large and important
subject, but one only peripherally related to operating systems.

### 1.1.2 The Operation System as a Resource Manager

The concept of an operating system as primarily providing abstractions to application
programs is a top-down view. An alternative, bottom-up, view holds that
the operating system is there to manage all the pieces of a complex system. Modern
computers consist of processors, memories, timers, disks, mice, network interfaces,
printers, and a wide variety of other devices. In the bottom-up view, the job
of the operating system is to provide for an orderly and controlled allocation of the
processors, memories, and I/O devices among the various programs wanting them.
Modern operating systems allow multiple programs to be in memory and run
at the same time. Imagine what would happen if three programs running on some
computer all tried to print their output simultaneously on the same printer. The first few lines of printout might be from program 1, the next few from program 2, then
some from program 3, and so forth. The result would be utter chaos. The operating
system can bring order to the potential chaos by buffering all the output destined
for the printer on the disk. When one program is finished, the operating system can
then copy its output from the disk file where it has been stored for the printer,
while at the same time the other program can continue generating more output,
oblivious to the fact that the output is not really going to the printer (yet).
When a computer (or network) has more than one user, the need for managing
and protecting the memory, I/O devices, and other resources is even more since the
users might otherwise interfere with one another. In addition, users often need to
share not only hardware, but information (files, databases, etc.) as well. In short,
this view of the operating system holds that its primary task is to keep track of
which programs are using which resource, to grant resource requests, to account
for usage, and to mediate conflicting requests from different programs and users.
Resource management includes multiplexing (sharing) resources in two different
ways: in time and in space. When a resource is time multiplexed, different
programs or users take turns using it. First one of them gets to use the resource,
then another, and so on. For example, with only one CPU and multiple programs
that want to run on it, the operating system first allocates the CPU to one program,
then, after it has run long enough, another program gets to use the CPU, then another,
and then eventually the first one again. Determining how the resource is time
multiplexed—who goes next and for how long—is the task of the operating system.
Another example of time multiplexing is sharing the printer. When multiple
print jobs are queued up for printing on a single printer, a decision has to be made
about which one is to be printed next.
The other kind of multiplexing is space multiplexing. Instead of the customers
taking turns, each one gets part of the resource. For example, main memory is normally
divided up among several running programs, so each one can be resident at
the same time (for example, in order to take turns using the CPU). Assuming there
is enough memory to hold multiple programs, it is more efficient to hold several
programs in memory at once rather than give one of them all of it, especially if it
only needs a small fraction of the total. Of course, this raises issues of fairness,
protection, and so on, and it is up to the operating system to solve them. Another
resource that is space multiplexed is the disk. In many systems a single disk can
hold files from many users at the same time. Allocating disk space and keeping
track of who is using which disk blocks is a typical operating system task.

## 1.2 HISTORY OF OPERATING SYSTEMS

Operating systems have been evolving through the years. In the following sections
we will briefly look at a few of the highlights. Since operating systems have
historically been closely tied to the architecture of the computers on which they run, we will look at successive generations of computers to see what their operating
systems were like. This mapping of operating system generations to computer
generations is crude, but it does provide some structure where there would otherwise
be none.
The progression given below is largely chronological, but it has been a bumpy
ride. Each development did not wait until the previous one nicely finished before
getting started. There was a lot of overlap, not to mention many false starts and
dead ends. Take this as a guide, not as the last word.
The first true digital computer was designed by the English mathematician
Charles Babbage (1792–1871). Although Babbage spent most of his life and fortune
trying to build his ‘‘analytical engine,’’ he nev er got it working properly because
it was purely mechanical, and the technology of his day could not produce
the required wheels, gears, and cogs to the high precision that he needed. Needless
to say, the analytical engine did not have an operating system.
As an interesting historical aside, Babbage realized that he would need software
for his analytical engine, so he hired a young woman named Ada Lovelace,
who was the daughter of the famed British poet Lord Byron, as the world’s first
programmer. The programming language Ada® is named after her.

### 1.2.1 The First Generation (1945-55): Vacuum Tubes

After Babbage’s unsuccessful efforts, little progress was made in constructing
digital computers until the World War II period, which stimulated an explosion of
activity. Professor John Atanasoff and his graduate student Clifford Berry built
what is now reg arded as the first functioning digital computer at Iowa State University.
It used 300 vacuum tubes. At roughly the same time, Konrad Zuse in Berlin
built the Z3 computer out of electromechanical relays. In 1944, the Colossus was
built and programmed by a group of scientists (including Alan Turing) at Bletchley
Park, England, the Mark I was built by Howard Aiken at Harvard, and the ENIAC
was built by William Mauchley and his graduate student J. Presper Eckert at the
University of Pennsylvania. Some were binary, some used vacuum tubes, some
were programmable, but all were very primitive and took seconds to perform even
the simplest calculation.
In these early days, a single group of people (usually engineers) designed,
built, programmed, operated, and maintained each machine. All programming was
done in absolute machine language, or even worse yet, by wiring up electrical circuits
by connecting thousands of cables to plugboards to control the machine’s
basic functions. Programming languages were unknown (even assembly language
was unknown). Operating systems were unheard of. The usual mode of operation
was for the programmer to sign up for a block of time using the signup sheet on the
wall, then come down to the machine room, insert his or her plugboard into the
computer, and spend the next few hours hoping that none of the 20,000 or so vacuum
tubes would burn out during the run. Virtually all the problems were simple straightforward mathematical and numerical calculations, such as grinding out
tables of sines, cosines, and logarithms, or computing artillery trajectories.
By the early 1950s, the routine had improved somewhat with the introduction
of punched cards. It was now possible to write programs on cards and read them in
instead of using plugboards; otherwise, the procedure was the same.

### 1.2.2 The Second Generation (1955-65): Transistors and Batch System

The introduction of the transistor in the mid-1950s changed the picture radically.
Computers became reliable enough that they could be manufactured and sold
to paying customers with the expectation that they would continue to function long
enough to get some useful work done. For the first time, there was a clear separation
between designers, builders, operators, programmers, and maintenance personnel.
These machines, now called mainframes, were locked away in large, specially
air-conditioned computer rooms, with staffs of professional operators to run them.
Only large corporations or major government agencies or universities could afford
the multimillion-dollar price tag. To run a job (i.e., a program or set of programs),
a programmer would first write the program on paper (in FORTRAN or assembler),
then punch it on cards. He would then bring the card deck down to the input
room and hand it to one of the operators and go drink coffee until the output was
ready.
When the computer finished whatever job it was currently running, an operator
would go over to the printer and tear off the output and carry it over to the output
room, so that the programmer could collect it later. Then he would take one of the
card decks that had been brought from the input room and read it in. If the FORTRAN
compiler was needed, the operator would have to get it from a file cabinet
and read it in. Much computer time was wasted while operators were walking
around the machine room.
Given the high cost of the equipment, it is not surprising that people quickly
looked for ways to reduce the wasted time. The solution generally adopted was the
batch system. The idea behind it was to collect a tray full of jobs in the input
room and then read them onto a magnetic tape using a small (relatively) inexpensive
computer, such as the IBM 1401, which was quite good at reading cards,
copying tapes, and printing output, but not at all good at numerical calculations.
Other, much more expensive machines, such as the IBM 7094, were used for the
real computing. This situation is shown in Fig. 1-3.
After about an hour of collecting a batch of jobs, the cards were read onto a
magnetic tape, which was carried into the machine room, where it was mounted on
a tape drive. The operator then loaded a special program (the ancestor of today’s
operating system), which read the first job from tape and ran it. The output was
written onto a second tape, instead of being printed. After each job finished, the
operating system automatically read the next job from the tape and began running it. When the whole batch was done, the operator removed the input and output
tapes, replaced the input tape with the next batch, and brought the output tape to a
1401 for printing off line (i.e., not connected to the main computer).
