/*............................... format procdeure: ............................................*/

/* proc format; */
/* run; */

/* invalue: ituses informat technique */
/*  */
/* 1.char to char */
/* 2.num to num  */
/* 3.char to num */
/*  */
/*   */
/* value: it uses format techique  */
/*  */
/* 1.char to char */
/* 2.num to char */
/*  */
/* these have functions : */
/* input: it requires informat technique convert values cahr or numeric */
/* put: it requires formatr techniqur convert values num to cahr */




data patient_demo;
    input PatientID Gender Age Visit_Status Dose_Code;
    datalines;
101 1 34 1 10
102 2 29 2 20
103 1 45 3 10
104 2 38 1 30
105 1 50 2 20
;
run;

/* ................................data conservations ..................................................*/

/* Visit_Status              visit      gender        sex             Dose_Code                       does */
/*  1                        week1        1           male             10                             0.1 */
/*  2                        week2        2          female            20                             0.2 */
/*  3                        week3                                     30                             0.3 */



proc format;
value wk 1="week1" 2="week2"  3="week3";
value sex11_ 1="male" 2="femaile";
invalue dsc 10=0.1 20=0.2 30=0.3;
run;


proc print data=patient_demo;
format Visit_Status wk. Dose_Code dsc. gender sex11_. ;
run;

/* we can directly give in print procedure using format  */

/*                     (or) */


/* data demo1; */
/* set patient_demo; */
/* visit=put(Visit_Status,wk.); */
/* does=input(put(Dose_Code,8.),dsc.); */
/* sex=put(gender,sex11_.); */
/* run; */
/* proc print data=demo1; */
/* run; */


data raw_patient;
input subjid  gender $ age dose $;
datalines;
101 M 25 LOW
102 F . HIGH
103 M 45 MID
104 F 30 LOW
;
run;

proc print data=raw_patient;
run;


proc format;
value $gen "F"="female" "M"="male";
invalue $doess "Low"=10 "mid"=20 "high"=30;
run;


data dm2;
set raw_patient;
gender=put(gender,$gen.);
doses=input(dose,$doess.); 
/* here we are converting char to numeric so we use $ symbol */
run;


/* key tip we use $(dollar symbol) for both char to char conversion and  char to numeric convertion  */



