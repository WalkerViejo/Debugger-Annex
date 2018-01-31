# Debugger-Annex

This is a package of C++ header files that are to be #included in C++ code.


purposes:

#1. date arithmetic, i.e. Find the number of days between two dates -- or the date that is n days before of after date X.

#2. to convert a unit of measure to a compound string form, like "12 feet 5.21 inches" or 12' 5.21"

#3. to enforce arithmetic restrictions, in order to avoid erroneous operations with units of measure



There are plenty of softwares to do date arithmetic, including practically every spreadsheet. But on some program developer's blogs
there are calls for date arithmetic routines that can be #included in C++ code; I couldn't find any, so I made my own.

As for #2, the need is obvious. Close to my house on a highway overpass, there is a sign "CLEARANCE 17 feet 6 inches".

--  --- - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  

The interactive development environments (IDE's), complete with source-level interactive debuggers have surely made the development
of computer programs quicker and easier! But these interactive debuggers  will  NOT catch  erroneous operations  on   numbers  that
represent quantities, like 245 calories, 30 mph,  or 21 inches. Addition or subtraction of unlike quantities needs to be disallowed,
e.g. 21 inches + 245 calories. For addition or subtraction of quantities that are alike but  in  different  units,  an  appropriate
conversion factor has to be put in, e.g. 50 miles + 40 km. Obviously, this package should be used in  conjunction  with a debugger,
and hence the name "Debugger Annex".

Quantities can  be  multiplied  and  divided.  For  example,  volts  =  joules / coulumb. Watts = amperes * volts. Force = mass *
acceleration, energy = force * distance, ... etc. Would mph be considered a quantity or a rate?  That is  a  matter  of  semantics.
What's important is that unlike rates and quantities have to be disallowed, as explained above.

--  --- - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  

A date is a place in time == not a quantity. A pointer in C/C++ is a place in a computer's memory -- not a quantity. Two places     
can be subtracted but not added or multiplied or divided. A quantity can be added to or subtracted to  a  place,  for  example:

5/15/2017 - 5/13/2017 = 2 days (a quantity of time).  5/15/2017 + 10 days = 5/25/2017.  5/15/2017 - 10 days = 5/5/2017.


Actually, "algebraic freedom" is allowed.
6/15/2017 + 5/15/2017 - 5/13/2017 = 6/17/1017,  i.e. 6/15/2017 + (5/15/2017 - 5/13/2017).

But 6/15/2017 + 5/15/2017 is disallowed.  As  for  how  the  package  does  this  and  makes  the  "subtle"  distinction, see the 
file Debugger_Annex_implement.com .


Temperatures, in this package, are treated like places. And the same arithmetic rules and restrictions apply. For example:

15 deg_C - 13 deg_C = 2 Kelvin_dg.  15 deg_C + 10 Kelvin_dg = 25 deg_C.  15 deg_C - 10 Kelvin_dg = 5 deg_C.


This all is analogous to C++ pointers.

*P - *Q = mem_quan;   *P + mem_quan = *Q;  *P - mem_quan = *q;

Last time I checked, the C++ compilers don't allow the above-mentioned "algebraic freedom".
--  --- - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  - -- ---  

Once again, this package offers date arithmetic and compound string conversion, in addition to being the "Debugger Annex".

Now on to the coding examples.


munit_quantity  my_weight = 197.3 * lbs;
munit_quantity  airplane_speed = 675.0 * mph;
munit_quantity  Concorde_speed = mach * 2.04;
munit_quantity  package_net_weight = lb / 4.0;	// i.e. a quarter of a pound
munit_quantity  package_net_wt	   = 0.25.* lb; // same thing

munit_quantity  distance_driven = 50.47 * miles + 40.52 * km;

munit_quantity  vanilla_1_amount = 5.2 * grams;		 // weight measure
munit_quantity  vanilla_2_amount = 1.5 * tsp;			 // volume measure
munit_quantity Xu = vanilla_1_amount + vanilla_2_amount; // This statement gets flagged as an error.

It's an error, because it attempts to add unlike quantities. Should this package  have  a  table of
volume/weight densities  of  every  powder  and  liquid? That  is  a rhetorical	question, of course.


Angles are one type of quantity; and there is a special provision for trigonometric functions.

munit_quantity angle_45  = 45 * trig_degrees;			      // 45 degree angle
munit_quantity angle_33g = (100.0 / 3.0) * gradients;	  // 30 degree angle, 33.3333 gradients

double aorth_45_d_sin = sin(angle_45);					  // value: .5 * sqrt(2)
double aorth_45_d_cos = cos(angle_45);					  // value: .5 * sqrt(2)
double aorth_45_d_tan = tan(angle_45);					  // value:  1

double aorth_33_g_sin = sin(angle_33g);					  // value: .5
double aorth_33_g_cos = cos(angle_33g);					  // value: sqrt(3) / 2
double aorth_33_g_tan = tan(angle_33g);					  // value: sqrt(3) / 3


There is a provision for invrse trigonometric functions.

munit_quantity xxiz = Asin(sqrt(2) / 2);          // value: 45 trig_degrees, or 50 gradients
munit_quantity x2iz = Atan(sqrt(3));              // value: 60 trig_degrees, or 66.6666... gradients


