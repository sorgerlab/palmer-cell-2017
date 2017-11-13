This Mathematica program takes as input two lists of 'event data' from clinical trial of individual therapies (lists of each patient's time of disease progression or time of censoring), and calculates the effect of a combination of the two therapies expected under independent drug action. Predictions are performed over a range of correlations in response, specifically rho = 0.3 +/- 0.2.

Important limitations are noted below:

1) This method predicts the effects of drug combinations if there is no drug interaction causing 'additive' or 'synergistic' effect, but also if there is no suppressive interaction (see supplementary note on 'Mathematical definitions of additive and synergistic interactions'). Drug combinations may in reality show pharmacodynamic interactions that cause their combined effect to be significantly stronger or weaker than this prediction.

2) This method, as presently configured, predicts effects of drug combinations over a range of correlations in response based on the correlations between chemotherapies and targeted therapies observed in a large panel of patient-derived tumor xenografts (the dataset of Gao et al, 2015, Nature Medicine v21:p1318). Different drug combinations, based on their mechanisms of action, may in reality have response correlations outside of this range. In particular, drug combinations whose components have higher correlation in response can be expected to have weaker effects than this program will currently predict. However, the degree of response correlation in this program is an adjustable parameter.

3) All uses of this method in the attached manuscript are based on probabilities of Progression Free Survival, not Overall Survival. There is no evidence that this method is successful when applied to Overall Survival data; indeed there is theoretical reason to believe that it would not work, on the basis that Overall Survival will be heavily influenced by patient-specific health factors that are extraneous to the interaction between tumor and drug.


To demonstrate the method to predict combination effects from clinical trial data, we have included sample data from phase 2 clinical trials of chemotherapy and olaparib for recurrent platinum-sensitive ovarian cancer.
Progression Free Survival times for chemotherapy (paclitaxel and carboplatin) are collected from
Oza et al. Lancet Oncol 2015; 16: 87–97 http://dx.doi.org/10.1016/S1470-2045(14)71135-0
Progression Free Survival times for olaparib monotherapy are collected from 
Liu et al. Lancet Oncol 2014; 15: 1207–14 http://dx.doi.org/10.1016/S1470-2045(14)70391-2
Because individual event data are not released in these publications, the times and numbers of individual progression or censoring events are manually annotated from inspection of the published PFS curves. Therefore the included sample data is an approximation and does not precisely recapitulate the original event data from these trials; nonetheless it is sufficient to demonstrate the method.


To execute this demonstration, first place all of the following files in a single folder: 

Olaparib_events.csv
Paclitaxel_Carboplatin_events.csv
Prediction from monotherapy trials code.nb

The code can then be executed by loading the notebook 'Prediction from monotherapy trials code.nb' in Wolfram Mathematica v11.0, and selecting 'Evaluate Notebook' from the 'Evaluation' menu.



To apply this method to other clinical data sets, replace the 'CSV' files (e.g, Olaparib_events.csv, Paclitaxel_Carboplatin_events.csv) with tables of event data in matching format, as demonstrated by inspecting the files or as described below:

Each row describes a single patient outcome.
Column 1 gives the time of an event since commencing the therapy (disease progression or death; or censoring)
Column 2 describes the type of event: '0' indicates disease progression or death, and '1' indicates censoring.

Each file should contain a single header row. The first column's header will be used as the label for the time axis in the automatically generated and exported plots; thus it should read, for example, "Time (months)" or edited as needed for time units other than 'months'. Events on different therapies must be entered in the same time units - this program does not have an in-built capacity to properly compare, for example, one set of events recorded in weeks with another recorded in months.
