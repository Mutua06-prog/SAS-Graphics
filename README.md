# SAS-Graphics
I will be sharing SAS codes I have written during my free time in SAS graphs

# To create a Side-by-Side bar graph with annotated numbers 


*Clear work library;
proc datasets lib=work nolist memtype=data kill;
run;
quit;

*Clear log;
dm 'log; clear; ';
run;
quit;

*To set ADAM library;
libname adam "F:\SAS LEARNING\TRAIN FOLDER\DATA\ADAM" access = readonly; 

