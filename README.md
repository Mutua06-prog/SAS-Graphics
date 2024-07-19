# SAS-Graphics
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

*To get Bign from SAFFL population flag;
proc sort data = adam.adqs out = adqs_ nodupkey; 
  by usubjid;
  where SAFFL in ("Y"); 
run; 

proc freq data = adqs_(where= (SAFFL ="Y")) noprint; 
  tables trt01an*trt01a / out = Bign(drop=percent);
run;  

data _null_;   
  set bign;  
  call symputx("trt_"!!put(trt01an,1.),count);
run; 
%put &trt_1.;  
%put &trt_2.; 

*TO get the right records for the graph;
data adqs_sevtm(keep= usubjid trt01a trt01an aval avalc avisitn avisit paramcd param att symptom );
  set adam.adqs; 
  where SAFFL="Y" and parcat1="PRO-CTCAE" and paramcd in ("PT01003A") and anl02fl="Y" and avisit ne "After 18 weeks post PD-unscheduled";
  symptom_=substr(param,6); 
run; 

