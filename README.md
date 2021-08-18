# Assignment 2 - CSpotify

```
version: 1. 4. 1 last updated: 2020 - 11 - 17 18  00  00
```

copy from "https://cgi.cse.unsw.edu.au/~cs1511/20T3/assignments/ass2/index.html"  

# Introduction

We consider music streaming to be a normal thing that we use regularly... but it wasn't always this way. In the late 1990 s, a new file
format called the MP 3 appeared. Its ability to compress audio coupled with the rise of the internet lead to a new era in the music industry.
Napster (and a new generation of music pirates) brought this into the spotlight when they launched in 1999.

Nowadays, with services like Spotify, we have access to a massive library of music (and other audio) content from nearly any device with
an internet connection.

In this assignment, you'll be looking at some of the coding work that goes into organisation of music with things like song information,
playlists and personal music libraries. CSpotify is our implementation of a song library using linked lists as the primary data structure.

## Your Goal

The assignment is divided into two parts:

```
Part A - Implementation ( 5 Stages)
Your task here is to write the functions that will manage your music Libraryof Playlists which contain Tracks. All of these
functions are contained inside the file cspotify.c.
```
```
Part B - Testing
Your task here is to write functions in test_cspotify.c to check that your code works.
```
Please note that you do not need to scan in any inputs from the user, this is already completed for you in the given starter code.

## The Overall Picture - Your Library

The Library is the overall struct which contains all the objects you will need for the assignment. The Library contains a list of
Playlists. In each of the Playlists, there is a list of Tracks. At the start of the program, the Library starts off as an empty Library
containing no Playlists and hence no Tracks.

As you progress through Stage 1 of the assignment to manage Playlists to your Library, your Library might start to look like this,
where there are Playlists in the Library but not Tracks in any of the Playlists:

```
Note: You should refer to cspotify.h for more technical and detailed instructions in regards to each functionʼs
implementation.
```

Stage 2 will then allow you to navigate around your LibraryPlaylistsand add Tracks to each Library, resulting in a Library that could
look like this:

Each Track will store information about the title, artist and the trackLength in addition to a next pointer.

Stage 3 will focus on removing certain objects from your Library.

Stage 4 and 5 will be more challenging manipulations of your Library.

The assignment breaks up the above further into smaller tasks to help you build and navigate around your Library. It is strongly
recommended that you begin from Stage 1 and progress in the given order.


# Getting Started

## Starter Code

The starter code consists of the following files:

main.ccontains the main function for the assignment. It will scan the program's input, then call the functions you will write.
**You must not change this file.**

cspotify.hcontains the definitions of all the functions you will be writing. It also contains useful constants and type definitions.
**You must not change this file.**

cspotify.ccontains empty functions which you will need to implement. It already contains some functions. It is _strongly recommended_
that you use these.
**This file is where you will write your own code.**

test_main.ccontains a main function and other functions that allow you to run the tests you create in test_cspotify.c.
**You must not change this file.**

test_cspotify.hcontains the prototypes of the testing functions in test_cspotify.c.
**You must not change this file.**

test_cspotify.ccontains an alternative main function as well as template code that you will modify to make your own tests.
**This file is where you will write your own test cases.**

capture.hcontains the definition of a function that allows you to capture the output of your own code, to use in testing. It can only be
used in test_cspotify.c, and will not be available in cspotify.c.
**You must not change this file.**

capture.ccontains the implementation of functions that allow you to capture the output of your own code, to use in testing.
**You must not change this file.**

To run your code interactively, you should use the command:

```
$ dcc -o cspotify cspotify.c main.c
$ ./cspotify
```
To run your tests (written in test_cspotify.c), you should use the command:

```
$ dcc -o test_cspotify cspotify.c test_cspotify.c capture.c test_main.c
$ ./test_cspotify
```
## Allowed C Features

In this assignment, there are two restrictions on C Features:

```
You must follow the rules explained in the Style Guide.
You may not use the function fnmatch, or import fnmatch.h.
```
It is recommended to only use features that have been taught in COMP 1511. Course work in Week 8 will have a particular focus on
assistance for this assignment and you will not need any of the subject material from Weeks 9 or 10.

If you choose to disregard this advice, you **must** still follow the Style Guide. You also may be unable to get help from course staff if you
use features not taught in COMP 1511.

## Reference Implementation

If you have questions about what behaviour your program should exhibit, we have provided a sample solution for you to use.

```
$ 1511 cspotify
```
```
Download the starter code (cspotify.zip) here or copy it to your CSE account using the following command:
$ 1511 setup_cspotify
```

# Stage One

When you execute your program, you can assume that the Library has already been created for you to perform the following operations.
Stage 1 involves managing the Playlists in your Library as well as printing out the state of the Library. You will need to implement or
modify the following functions:

```
create_library(This is already implemented for you, you may need to modify it)
add_playlist
print_library
rename_playlist
```
## Add a playlist

In cspotify.c you have been given the function stub (a stub is an unimplemented function):

```
// Add a new Playlist to the Library.
int add_playlist(Library library, char playlistName[MAX_LEN]) {
return SUCCESS;
}
```
This function will be given a Library and a Playlist name. You will need to insert a new Playlist node at the end of the linked list of
Playlists in the Library. If the Library has no Playlists, your new Playlist will become the first Playlist in the Library. If this is the
case, you will need to make this Playlist “selected”.

You can assume you will never receive a Playlist name which already exists in the Library

You may receive invalid inputs so the function will return either:

```
ERROR_INVALID_INPUTSif the given Playlist name is invalid (i.e. not alphanumeric).
SUCCESSif a new Playlist is successfully added.
```
You will need to create a Playlist node (using malloc) before it is inserted into the Library.

Please note that until you implement the next function in this stage for printing out the Library, you will not be able to see whether your
Playlist has been added successfully into the Library.

## Print Out the Library

In cspotify.c you have been given the function stub (a stub is an unimplemented function):

```
// Print out the Library.
void print_library(Library library) {
```
```
}
```
You will need to use the following helper functions already provided to you in the same file: print_playlist, print_selected_playlist
and print_track.

This function will be given a Library. The function should go through each Playlist in the Library and print out the information in the
order they are in inside the Library. You should use the above helper functions to print the Library out, instead of calling printf
yourself. Note that the word static on these functions will make that function only accessible in the current file. We often use static on
helper functions that are not part of the header file and aren't used by any other parts of the program. static will not significantly
change how you will use or define this function.

```
Command: A <playlistName>
Example: A RoadTrip
Description: Adds a new Playlist named "Roadtrip" at the end of the Library of Playlists.
```
```
The message which appears right after running any command simply acknowledges the function has been called and/or depends
on your return values. It does not necessarily indicate the success of your implementation of this function.
```
```
Command: P
Example: P
Description: Prints out the Library.
```

You may see that both print_playlist and print_selected_playlist above take in an int number, this is the position in which they are
in in the Library of Playlists assuming that the first Playlistis at position 0.

The function should not return anything.

At this stage, you will only need to use print_playlist and print_selected_playlist to help you print out information in the Library.
print_trackis not needed until Stage 2 has been implemented. After implementing stage 2 , you should come back and make sure that
the Tracks in each Playlist are also printed out.

## Rename a Playlist

In cspotify.c you have been given the function stub (a stub is an unimplemented function):

```
// Rename the name of an existing Playlist.
int rename_playlist(Library library, char playlistName[MAX_LEN],
char newPlaylistName[MAX_LEN]) {
return SUCCESS;
}
```
This function will be given a Library, a Playlist name and a new Playlistname. Your task is to find the playlistName in the Library of
Playlistsand change its name to the name given in newPlaylistName.

You may receive invalid inputs so the function will return either:

```
ERROR_NOT_FOUNDif the given Playlist name is not found otherwise,
ERROR_INVALID_INPUTSif the new Playlist name is invalid (i.e. not alphanumeric).
SUCCESSif a new Playlist is successfully added.
```
# Stage Two

Stage 2 involves navigating around a Library of Playlists and adding Tracks. You will need to implement the following functions:

```
select_next_playlist
select_previous_playlist
add_track
playlist_length
```
## Select the Next Playlist

In cspotify.c you have been given the function stub (a stub is an unimplemented function):

```
// Selects the next Playlist in the Library.
void select_next_playlist(Library library) {
```
```
}
```
```
Command: R <playlistName> <newPlaylistName>
Example: R Roadtrip SleepMusic
Description: Renames the existing Playlist "Roadtrip" to "SleepMusic".
```
```
Run the tests for this stage with:
$ 1511 autotest-stage 01 ass2_cspotify
Check the style of your code with:
$ 1511 style cspotify.c
Please note, the files you test must be named correctly, or this test will not work properly.
To pass all the tests for this stage, you will need to add tests in test_cspotify.c See Writing your own automated tests for
more info.
```
```
Command: S
Example: S
Description: Selects the next Playlist in the Library.
```

This function will be given a Library. In Stage 1 , by default the first Playlist added into the Library was selected. For this function, you
will need to change the selected Playlist in the Library to the Playlist after the currently selected Playlist.

If the currently selected Playlist is the last Playlist in the Library, make the first Playlist in the Library become the new selected
Playlist.

The function should not return anything.

## Select the Previous Playlist

In cspotify.c you have been given the function stub (a stub is an unimplemented function):

```
// Selects the previous Playlist in the Library.
void select_previous_playlist(Library library) {
```
```
}
```
This function is very similar to selecting the next Playlist. Given a Library, you will need to change the Playlist that is selected to the
Playlist before the currently selected Playlist.

If the currently selected Playlist is the first Playlist in the Library, make the last Playlist in the Library become the new selected
Playlist.

The function should not return anything.

## Add a Track

In cspotify.c you have been given the function stub (a stub is an unimplemented function):

```
// Add a new Track to the selected Playlist.
int add_track(Library library, char title[MAX_LEN], char artist[MAX_LEN],
int trackLengthInSec, int position) {
return SUCCESS;
}
```
This function will be given a Library, Track title, the artist of the Track, the Track length in seconds as well as a position number.

Your task is to go through the selected Playlist and add a new Track node at the position specified by position. If position is 0 , the
node should be inserted at the front of the Playlist. If the position has a value equal to the number of Tracks in the Playlist, the node
should be inserted at the end of the Playlist.

It is possible that the same Track can be added to the same Playlist multiple times. You may receive invalid inputs so the function will
return one of the following:

```
ERROR_NOT_FOUNDif there are no Playlists in the Library, otherwise,
ERROR_INVALID_INPUTSif the given title/artist/position/track length is invalid. (see cspotify.h for more details)
SUCCESSif a new Playlist is successfully added.
```
You will also need to make changes to your print_library function in Stage 1 so that it will now also print out the Tracks you add to a
Playlist.

## Calculate the Length of the Playlist

```
Command: W
Example: W
Description: Selects the previous Playlist in the Library.
```
```
Command: a <title> <artist> <trackLengthInSec> <position>
Example: a PrettySavage BLACKPINK 350 0
Description: Adds a new Track at the 0 th position in the selected Playlist. Specifically, this is a Track titled "PrettySavage" by
the artist "BLACKPINK" and has a Track length of 350 seconds.
```
```
Command: T
Example: T
Description: Calculates the total length of the selected Playlist in minutes and seconds.
```

In cspotify.c you have been given the function stub (a stub is an unimplemented function):

```
// Calculate the total length of the selected Playlist in minutes and seconds.
void playlist_length(Library library, int *playlistMinutes, int *playlistSeconds) {
```
```
}
```
For this function, you are given a Library and two uninitialised int variables passed into the function by reference (i.e. the two int
pointers you receive in this function are pointing to the memory location of two int variables).

Your task is to go through and calculate the length of the currently selected Playlist in your Library. The total number of minutes in the
Playlist should be stored inside the memory pointed to by the playlistMinutespointer. The total number of seconds in the Playlist
should be stored in the memory pointed to by the playlistSeconds pointer.

The function should not return anything.

# Stage Three

Stage 3 involves removing objects from your Library and the Libraryitself. You will be freeing memory which has been malloced. You
will need to implement the following functions:

```
delete_track
delete_playlist
delete_library
```
## Delete a Given Track

In cspotify.c you have been given the function stub (a stub is an unimplemented function):

```
// Delete the first instance of the given track in the selected Playlist
// of the Library.
void delete_track(Library library, char track[MAX_LEN]) {
```
```
}
```
Calling this function should delete the first instance which matches the given Track name within the selected Playlist.

The function should not return anything.

## Delete the Selected Playlist

In cspotify.c you have been given the function stub (a stub is an unimplemented function):

```
Run the tests for this stage with:
$ 1511 autotest-stage 02 ass2_cspotify
Check the style of your code with:
$ 1511 style cspotify.c
Please note, the files you test must be named correctly, or this test will not work properly.
To pass all the tests for this stage, you will need to add tests in test_cspotify.c See Writing your own automated tests for
more info.
```
```
Command: d <track>
Example: d LovesickGirls
Description: Deletes the first instance of the Track titled "LovesickGirls" in the selected Playlist of the Library.
```
```
Command: D
Example: D
Description: Deletes the selected Playlist and select the next Playlist in the Library.
```

```
// Delete the selected Playlist and select the next Playlist in the Library.
void delete_playlist(Library library) {
```
```
}
```
Calling this function should delete the entire selected Playlist as well as all the Tracks within this Playlist. You should ensure that the
next Playlist in the Library is selected once the currently selected Playlistis removed. If there is no next Playlist, select the first
Playlist in the Library.

The function should not return anything.

## Delete the Entire Library

In cspotify.c you have been given the function stub (a stub is an unimplemented function):

```
// Delete an entire Library and its associated Playlists and Tracks.
void delete_library(Library library) {
```
```
}
```
Calling this function should delete the entire given Library including its Playlists and Tracks within each Playlist.

The function should not return anything.

# Stage Four

Stage 4 consists of more involved manipulations of the Library. You will need to implement the following functions:

```
cut_and_paste_track
soundex_search
```
## Cut and Paste Track

In cspotify.c you have been given the function stub (a stub is an unimplemented function):

```
Command: X
Example: X
Description: Deletes an entire Library and its associated Playlists and Tracks.
```
```
Run the tests for this stage with:
$ 1511 autotest-stage 03 ass2_cspotify
Check the style of your code with:
$ 1511 style cspotify.c
Please note, the files you test must be named correctly, or this test will not work properly.
To pass all the tests for this stage, you will need to add tests in test_cspotify.c See Writing your own automated tests for
more info.
```
```
This stage has very few tests in the autotest! They do not necessarily cover every edge case. You should test it with other
inputs, and compare your solution against the reference solution.
```
```
Command: c <trackName> <destPlaylist>
Example: c WakaWaka Fun
Description: Moves the Track title "WakaWaka" from the currently selected Playlist to an existing destination Playlist named
"Fun".
```

```
// Cut the given track in selected Playlist and paste it into the given
// destination Playlist.
int cut_and_paste_track(Library library, char trackTitle[MAX_LEN],
char destPlaylist[MAX_LEN]) {
return SUCCESS;
}
```
This function will take in a Library, a Track title and a destination Playlist. It should remove the first Track instance which matches the
given trackName from the selected Playlist and add it into the end of the Playlist with the given destination Playlist name. The
function should return one of the error codes (see cspotify.h for more details) or SUCCESS.

## Soundex Search

## What is Soundex?

Soundex is a phonetic algorithm which allows strings to be encoded so that words which sound similar will have the same encoding
despite small differences in spelling.

This becomes very useful in searching for music. For example, when searching for artists, mispelling the artist names will still allow you to
search for the artist.

In cspotify.c you have been given the function stub (a stub is an unimplemented function):

```
// Search the given Library for tracks where its artist
// match the given searchTerm
void soundex_search(Library library, char artist[MAX_LEN]) {
```
```
}
```
This function will take in a Library and a search term. Your task is to go through the given Library and print out all Tracks with artists
that have the same Soundex encoding as the given search term. You will again, need to use the given help function print_trackinstead
of calling printf yourself to print out the matching Tracks.

The specific version of the Soundex algorithm which will be used is specified in cspotify.h

The function should not return anything.

# Stage Five

Stage 5 consists of more involved manipulations of the Library. You will need to implement the following functions:

```
add_filtered_playlist
d l li t
```
```
Command: s <searchTerm>
Example: s Robert
Description: Prints out all Tracks with artists that have the same Soundex Encoding as the given search term.
```
```
New: If you're looking for a verbal explaination, this is a recording of Tom (COMP 1511 course admin) explaining Soundex to his class:
https://www.youtube.com/watch?v=GPd_W 0 z 2 - 1 w
```
```
Run the tests for this stage with:
$ 1511 autotest-stage 04 ass2_cspotify
Check the style of your code with:
$ 1511 style cspotify.c
Please note, the files you test must be named correctly, or this test will not work properly.
To pass all the tests for this stage, you will need to add tests in test_cspotify.c See Writing your own automated tests for
more info.
```
```
This stage has very few tests in the autotest! They do not necessarily cover every edge case. You should test it with other
inputs, and compare your solution against the reference solution.
```

```
reorder_playlist
```
## Add Filtered Playlist

In cspotify.c you have been given the function stub (a stub is an unimplemented function):

```
// Move all Tracks with artists that have the same Soundex Encoding as
// the given artist to a new Playlist.
int add_filtered_playlist(Library library, char artist[MAX_LEN]) {
return SUCCESS;
}
```
This function will take in a Library and an artist. It should go through the entire Library and move all Tracks with artists that have the
same Soundex Encoding as the given artist into a new Playlist named with the given artist. The function should return one of the error
codes (see cspotify.h for more details) or SUCCESS.

## Reorder Playlist

In cspotify.c you have been given the function stub (a stub is an unimplemented function):

```
// Reorder the selected Playlist in the given order specified by the order array.
void reorder_playlist(Library library, int order[MAX_LEN], int length) {
```
```
}
```
This function differs slightly in the way in which the command is executed. Once the above command is executed, the program will
prompt you to enter a series of integers.

This function will take in a Library, an order array and length. It should reorder the Tracks in the selected Playlist based on the order in
the given array. More details about this function has been given in cspotify.h.

# Testing

It is important to test your program thoroughly to make sure it can manage different situations.

## Writing your own Automated Tests

As you implement functions in cspotify.c, you will encounter autotests in that require you to implement the functions in
test_cspotify.c.

You are given a file test_main.c. This is not the same as the interactive program in main.c. Instead, it runs the series of automatic tests
on the functionality provided by cspotify.h and cspotify.c. You should not change this main function.

Your main function will call other functions that look like this:

```
Command: F <artist>
Example: F Taylor
Description: Move all Tracks with artists that have the same Soundex Encoding as "Taylor" to a new Playlist.
```
```
Command: r <length>
Example: r 5
Description: Reorders the selected Playlist of 5 Tracksin an order which will be specified in the input following this command.
```
```
Run the tests for this stage with:
$ 1511 autotest-stage 05 ass2_cspotify
Check the style of your code with:
$ 1511 style cspotify.c
Please note, the files you test must be named correctly, or this test will not work properly.
```

```
// Test function for 'add_playlist'
int test_add_playlist(void) {
```
```
// Test 1: Does add_playlist return SUCCESS and add
// when adding one Playlist with a valid name?
Library testLibrary = create_library();
```
```
int result = add_playlist(testLibrary, "Favourites");
if (result != SUCCESS) {
printf("DOES NOT MEET SPEC \n ");
return ;
}
```
```
char printText[ 10000 ];
CAPTURE(print_library(testLibrary), printText, 10000 );
if (!string_contains(printText, "Favourites")) {
printf("DOES NOT MEET SPEC \n ");
return ;
}
```
```
// Test 2: Does add_playlist return ERROR_INVALID_INPUTS
// and not add the playlist into the Library
// when trying to add a Playlist with an invalid name?
// TODO: Add your test for Test 2
```
```
// Test 3: ???
// TODO: Add your own test, and explain it.
```
```
printf("MEETS SPEC \n ");
}
```
Your job is to fill in the spaces where it says "TODO" with a series of C statements that check whether the functions in cspotify.c work.

As you can see in Test 1 , some of these functions have already been partially implemented to show you what you should do

Some functions will ask you to specifically test something (in this case, to make sure add_playlist returns the correct amount if you call
it many times).

Some functions will ask you to decide on your own test. You should describe what you are testing, and then write a test for that situation.

Note that you can **only** test functions by checking their outputs, and their output to the terminal. You cannot access the fields of a struct,
nor can you redefine the structs from cspotify.c in test_cspotify.c. Doing so may cause you to lose marks.

You can test your tests yourself, by compiling it against your cspotify.c.

This is what you will see when you compile the starter code/tests.

```
$ dcc -o test_cspotify test_cspotify.c cspotify.c capture.c test_main.c
$ ./test_cspotify
*~~~~~~~~~~~~~~~~~~~~~~~{ CSpotify Tests }~~~~~~~~~~~~~~~~~~~~~~~*
Stage 1 - Test add_playlist: DOES NOT MEET SPEC
Stage 1 - Test rename_playlist: DOES NOT MEET SPEC
Stage 2 - Test add_track: MEETS SPEC
Stage 2 - Test playlist_length: MEETS SPEC
Stage 3 - Test delete_playlist: MEETS SPEC
Stage 4 - Test soundex_search: MEETS SPEC
Your extra tests: MEETS SPEC
```
If you want to see exactly what program the autotests will run, you can use the commands:

```
$ 1511 build_test_cspotify test_cspotify.c -o test_cspotify
$ ./test_cspotify INVALID_INPUTS
$ ./test_cspotify RENAME_FAILS
$ ./test_cspotify NONE
$ ./test_cspotify MANY_TRACKS
$ ./test_cspotify NO_MINUTES
$ ./test_cspotify NO_DELETE_FIRST
```
The above commands will each run a different broken solution, so you can see if your program functions correctly.

### Capture

You may notice that we have given you two extra files - - capture.cand capture.h. These files define the CAPTURE macro. Macros are not
covered in this course and as a result, you do not need to understand these files.


You can use them to capture what a function prints and put it into a string. This is useful if you use it with for example, the print_library
function, since you can then test the output for the Library is as you expect.

The header of capture.h describes how to use it.

```
// This file contains the `CAPTURE()` macro. To use this macro,
// you should define a large, empty string. Lets say your string is:
// char str[MAX_LENGTH];
// Then you can do the following:
// CAPTURE(my_function(), str, MAX_LENGTH)
// Which will put the output of `my_function()` into str.
```
## Autotests

As usual autotest is available with some simple tests - but your own tests in test_cspotify.c may be more useful at pinpointing exactly
which functions are and aren't working.

```
$ 1511 autotest cspotify
```
If you wish to use autotest to view only a specific stage of the assignment, you can use autotest-stage. The following example shows how
to autotest stage 1 but you can replace the stage number with any stage you would like to test.

```
$ 1511 autotest-stage 01 cspotify
```
# Frequently Asked Questions

## How many tests do I need to complete to get full marks?

You only need to complete the tests marked with "TODO"; except the extra_testswhich are optional. For each function, this means you
will need to write two tests (note that this desn't include tests we have provided you). You do not need to write tests for stage five,
though we encourage you to do so for your own learning and enjoyment!

## Why can't I access structs from cspotify.c inside of test_cspotify.c?

The way C works is if the struct definition is not present in the current .c file then the code there is not able to access the members of
that struct. You can create a pointer variable which points to that struct, but you will not be able to access it's members with ->. This is a
good thing, and is intended.

This design feature is because it allows us to implement Abstract Data-Types (ADTs). The objective of using ADTs is so that the code of
one file can not access the “inner workings” of a variable that it uses, but is restricted to calling functions from a .h file with that variable.
This may sound counter productive at first, why would you want to limit access to a variable? Actually there are several advantages:

```
. Access Control : This is a useful concept when you have multiple programmers working together. It allows you to police the things
that happens to your Library. If you are the creator of the data type (the Library) you can prevent other people (who may not
know what their doing) from changing pointers (perhaps accidentally) in your data structure and in general ruining things.
. Abstraction : It presents a simple interface (defined in the .h file) to use the code of your Library. If you are the user of the data
type someone else has created, it is really helpful to be presented with a simpler interface which hides the details of the underlying
data structures, so they don't have to learn as many things to be able to use your data type.
. Decoupling : All test_cspotify.c files will conform to a common interface. Perhaps the way the other students in this course
organised the members in their structs might be different to the way you're doing it. Tests which don't directly interact with the
Library's members are interchangeable in this sense, one student's tests could be paired up with another student's Library and
there wouldn't be any compatibility issues there.
```
So, to fix your error, try to design tests which don't stab -> into the Library, just call the functions in cspotify.h and check their outputs
are correct/they did the correct things.

(Answer adapted from a forum post by Dean Wunder)

## Can I define structs from cspotify.c in test_cspotify.c?

```
Tests have been added in the autotest which are dedicated to testing some of the tests you write in test_cspotify.c. The
autotests will run the tests you write in test_cspotify.cwith a deliberately incorrect cspotify.csolution. Your tests should be
able to detect the issue in the broken code and output "DOES NOT MEET SPEC" in particular scenarios.
```

Unfortunately no, See above.

## Why do I keep getting the Incomplete definition of type ... error?

See above.

Look out for this space! More may be added to clarify any questions throughout the assignment!

# Assessment

## Attribution of Work

This is an individual assignment. The work you submit must be your own work and only your work apart from exceptions below. Joint
work is not permitted.

You may use small amounts (< 10 lines) of general purpose code (not specific to the assignment) obtained from site such as Stack
Overflow or other publically available resources. You should attribute clearly the source of this code in a comment with it.

You are not permitted to request help with the assignment apart from in the course forum, help sessions or from course lecturers or
tutors.

Do not provide or show your assignment work to any other person (including by posting it on the forum) apart from the teaching staff of
COMP 1511.

The work you submit must otherwise be entirely your own work. Submission of work partially or completely derived from any other
person or jointly written with any other person is not permitted. The penalties for such an offence may include negative marks, automatic
failure of the course and possibly other academic discipline. Assignment submissions will be examined both automatically and manually
for such submissions.

Relevant scholarship authorities will be informed if students holding scholarships are involved in an incident of plagiarism or other
misconduct. If you knowingly provide or show your assignment work to another person for any reason, and work derived from it is
submitted you may be penalised, even if the work was submitted without your knowledge or consent. This may apply even if your work is
submitted by a third party unknown to you.

Note, you will not be penalised if your work is taken without your consent or knowledge.

## Submission of Work

**You are required to test and/or submit intermediate versions of your assignment.** Every time you work on the assignment and make
some progress you should copy your work to your CSE account and submit it using the give command, or autotest it using
1511 autotest

It is fine if intermediate versions do not compile or otherwise fail submission tests.

Only the final submitted version of your assignment will be marked. **You must give when you have completed your assignment.**

If you would like to retrieve your old work, you can go to: View Autotests/Submissions/Marking and click the yellow bubble next to
ass2_cspotify. This will show you a timeline of all the code you have submitted recently.

You submit your work like this:

```
$ give cs1511 ass2_cspotify cspotify.c test_cspotify.c
```
The only files you can modify are cspotify.c and test_cspotify.c. **It is not possible to add new files, or modify the other files we
have given you**. If you believe you need to modify those files, you have misunderstood the specification. You should not modify your
copies of those files in any way.

## Assessment Scheme

This assignment will contribute 25 % to your final mark.

70 % of the marks for this assignment will be based on the performance of the functions you write in _cspotify.c_.

10 % of the marks for this assignment will come from the test_cspotify.c file. We will examine your own test cases to assess how many
distinct cases they test, and whether they meet the descriptions in test_cspotify.h.

20 % of the marks for assignment 2 will come from hand marking of the readability of the C you have written. These marks will be
awarded on the basis of clarity, commenting, elegance and style. In other words, your tutor will assess how easy it is for a human to read
and understand your program.

Marksforyourperformancewillbeallocatedroughlyaccordingtothebelowscheme.


Marks for your performance will be allocated roughly according to the below scheme.

```
100 % for Performance Completely working implementation of Stages 1 - 5
```
```
85 % for Performance Completely working implementation of Stages 1 - 4
```
```
70 % for Performance Completely working implementation of Stages 1 - 3
```
```
60 % for Performance Completely working implementation of Stages 1 and 2
```
```
50 % for Performance Completely working implementation of Stages 1 and working selection.
```
```
40 % for Performance Completely working implementation of Stage 1
```
```
30 % for Performance Partially working implementation of Stage 1 - - Creating and printing out a playlist's name.
```
```
< 40 % for Performance Manually assessed based on closeness to a working program.
```
```
100 % for Style Perfect style
```
```
90 % for Style Great style, almost all style characteristics perfect.
```
```
80 % for Style Good style, one or two style characteristics not well done.
```
```
70 % for Style Good style, a few style characteristics not well done.
```
```
60 % for Style OK style, an attempt at most style characteristics.
```
```
<= 50 % for Style An attempt at style.
```
Note that the following penalties apply to your total mark for plagiarism:

```
0 for the assignment Knowingly providing your work to anyone and it is subsequently submitted (by anyone).
```
```
0 for the assignment Submitting any other person's work. This includes joint work.
```
```
0 FL for COMP 1511 Paying another person to complete work. Submitting another person's work without their consent.
```
The following is an indicative list of characteristics of your program that will be assessed, though your program will be assessed
wholistically so other charactersitics may be assessed too:

```
Header Commenting.
Consistent, sensible indenting.
Using Blank Lines & Whitespace.
Using constants.
Decomposing code into functions where relevent (especially after Stage 2 ).
Using comments effectively (at least at top of functions, and not containing irrelevant info).
```
The course staff may vary the assessment scheme after inspecting the assignment submissions but it will remain broadly similar to the
description above.

### Due Date

This assignment is due Sunday 22 November 2020 20  00  00

If your assignment is submitted after this date, each hour it is late reduces the maximum mark it can achieve by 2 %. For example if an
assignment worth 78 % was submitted 5 hours late, the late submission would have no effect. If the same assignment was submitted 15
hours late it would be awarded 70 %, the maximum mark it can achieve at that time.

### Change Log

**Version 1. 0**
( 2020 - 11 - 01 22  30  00 )

```
Assignment draft released.
```
**Version 1. 1** Testingtestsforassignmentreleased


```
COMP 1511 20 T 3 : Programming Fundamentals is brought to you by
the School of Computer Science and Engineering
at the University of New South Wales, Sydney.
For all enquiries, please email the class account at cs 1511 @cse.unsw.edu.au
CRICOS Provider 00098 G
```
### Credits

Created by Tammy Zhong.

Credits to Marc Chee, Tom Kunc, Dean Wunder, Ollie Xue and Tammy Zhong for this assignment.

**Version 1. 1**

( 2020 - 11 - 02 02  30  00 )

```
Testing tests for assignment released
Fix 30 % criteria being wrong
```
**Version 1. 2**
( 2020 - 11 - 07 01  50  00 )

```
Added explanation relating to autotests for tests
```
**Version 1. 3**
( 2020 - 11 - 10 18  50  00 )

```
Added autotest-stage and style instructions; and compile instructions for tests.
```
**Version 1. 4**
( 2020 - 11 - 11 02  00  00 )

```
Removed underscores from variable names in diagrams.
```
**Version 1. 4. 1**
( 2020 - 11 - 17 18  00  00 )

```
Added soundex explainer
```

