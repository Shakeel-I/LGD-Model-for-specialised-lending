# EAD-model-using-SAS
Finding the best fit distribution for LGD using mixture models

<img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/f927b835-e245-4ac7-8c75-ad76381bf7ec" />  <img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/40361632-f33e-4cd3-b3ae-75bb24fe1cc1" />

<img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/b2c4df7f-a490-4f27-b9e8-aa3c714cfa49" />  <img width="400" height="300" alt="image" src="https://github.com/user-attachments/assets/75286bf2-884f-4856-80f7-439b795d2d0a" />

![Choose](https://github.com/user-attachments/assets/69ae6cf8-d44b-4d00-9dbe-13ba30446e3b)

Huang & Xie 2012
A mixture distribution is formed by combining two or more distributions weighted by mixing probabilities. For example, a mixture of two or more beta distributions or a mixture of normal and gamma distributions
to better model complex data patterns like multimodality or heterogeneity.

data: the name of the input dataset

depvar: the name of the dependent variable

kmax: the maximum number of the components

outstat: the name of the output dataset

modlist: the name list of the distributions tested separated by space

return: 5 fitting criterions plus the number of effective components and effective parameters


# SAS CODE
```
%macro modselect(data=, depvar=, kmin=, kmax=, outstat=, modlist=);
	%let modcnt = %eval(%sysfunc(count(%cmpres(&modlist), %str( )))+1);

	%do i=1 %to &modcnt;
		%let modelnow = %scan(&modlist, &i);
		ods output fitstatistics=&modelnow(rename=(value=&modelnow));
		ods select densityplot fitstatistics;

		proc fmm data=&data;
			model &depvar= / krestart kmax=&kmax dist=&modelnow;
		run;

	%end;

	data &outstat;
		%do i=1 %to &modcnt;
			set %scan(&modlist, &i);
		%end;
	run;

%mend;

%modselect(data=mydata.lgd, depvar=lgd_time, kmax=5, outstat=result, 
	modlist=beta lognormal gamma normal);


title "Choosing the best distribution";

proc print data=result;
run;

title;
```
=====================
```
%macro modselect(data=, depvar=, kmin=, kmax=, outstat=, modlist=);
	%let modcnt = %eval(%sysfunc(count(%cmpres(&modlist), %str( )))+1);
  
  %do i=1 %to &modcnt;
		%let modelnow = %scan(&modlist, &i);
		ods output fitstatistics=&modelnow(rename=(value=&modelnow));
		ods select densityplot fitstatistics;

proc fmm data=&data;
			model &depvar= / krestart kmax=&kmax dist=&modelnow;
		run;

%end;

data &outstat;
		%do i=1 %to &modcnt;
			set %scan(&modlist, &i);
		%end;
	run;

%mend;

%modselect(data=mydata.lgd, depvar=lgd_time, kmax=5, outstat=result, 
	modlist=beta lognormal gamma normal);
title "Choosing the best distribution";

proc print data=result;
run;

title;

proc fmm data=mydata.lgd;
	model lgd_time=LTV purpose1 / k=3 dist=normal;
	ods output parameterestimates=parmstat;
run;

proc fmm data=mydata.lgd;
	model lgd_time=LTV purpose1 /dist=normal;
	model + LTV purpose1 /dist=t;
	output out=fmm_out pred resid(component) resid(overall);
run;
```
