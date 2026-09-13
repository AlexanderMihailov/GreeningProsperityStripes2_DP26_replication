readme_GPS2_DP_260913.pdf

This readme file provides guidance on the data and the code necessary to replicate “Greening Prosperity Stripes 2: Consumption-Based Refinement”, by Alexander Mihailov, Economics Discussion Paper 2026-09, University of Reading:
https://research.reading.ac.uk/economics/wp-content/uploads/sites/87/2026/09/emdp202609.pdf

The codes, collected in this replication zip archive on GitHub, were run on a MacBookPro (November 2024), chip Apple M4 max, memory 36 GB, macOS Tahoe 26.5.1 and on MATLAB R2025b. They complete in several minutes each.

The data are collected online, as described in detail in the Data subsection of the DP, and the respective Excel *.xls, *xlsx, and *.csv files named below are downloaded in their raw format from the online sources provided with URLs and mnemonics in the same subsection of the DP.

In this replication zip archive, there are 8 data files (listed next in alphabetical order), of which 2 resulting from running the code below (marked), and 6 original files downloaded from online data archives, as clarified in the DP and in the guidance that follows here below:

API_EN.ATM.CO2E.PC_DS2_en_excel_v2_5607813.xlsx
API_NE.CON.PRVT.PC.PP.KD_MATLAB.xlsx (resulting)
API_NE.CON.PRVT.PP.KD_DS2_en_excel_v2_5530.xls
API_NY.GDP.PCAP.PP.KD_DS2_en_excel_v2_5607670.xlsx
API_NY.GDP.PCAP.PP.KD_DS2_en_excel_v2_5607670.xls
API_NY.GDP.PCAP.PP.KD_DS2_en_excel_v2_5607670.xlsx
ConsCO2pc_ExcelTableConversion_ExactMatch_EmptyColumns_MATLABGemini_AM260316.xlsx (resulting)
consumption-co2-per-capita.csv

In this replication zip archive, there are also 6 MATLAB code files (listed next in alphabetical order):

CO2pcConsBased_ExcelTableConversion_ExactMatch_MATLABGemini_AM260316.m (run 1st)
GPS1ProdBased_All4FigsByC_WinsorDYNAMIC_GeminiAM260318v0811.m (run after the preliminary stage, in no order)
GPS1ProdBased_All4FigsByC_WinsorSTATIC2020_GeminiAM260318v0811.m (run after the preliminary stage, in no order)
GPS2ConsBased_All4FigsByC_WinsorDYNAMIC_GeminiAM260318v0812.m (run after the preliminary stage, in no order)
GPS2ConsBased_All4FigsByC_WinsorSTATIC2020_GeminiAM260318v0811.m (run after the preliminary stage, in no order)
GPS2pcConsBased_ExcelTable_GeminiAM260318.m (run 2nd)

The execution of the code follows in two stages: preliminary (preparing the data) and calculation and plotting (generating the stripe images). They need to be executed in that order, i.e., start with Preliminary Stage 1a, followed by Preliminary Stage 1b; for Stage 2, the 4 MATLAB codes can be executed in any order, and each of them is richly annotated, storing its output in a specified folder, as described below.

Preliminary Stage 1a
Start with the code:

ConsCO2pc_ExcelTableConversion_ExactMatch_EmptyColumns_MATLABGemini_AM260316.m

% Purpose: The code uses the World Bank data file API_NE.CON.PRVT.PP.KD_DS2_en_excel_v2_5530.xls
%          and converts another data file from Our World in Data, consumption-co2-per-capita.csv
%          into exactly the same format, including empty columns for years 1960-1989. The output
%          file is then further used in other code as denominator of the consumption-based GPR2.

%% Data source: https://ourworldindata.org/grapher/consumption-co2-per-capita
% Per capita consumption-based CO₂ emissions
% Global Carbon Project
% Annual consumption-based emissions of carbon dioxide (CO₂), measured in tonnes per person.
% Source: Global Carbon Budget (2025); Population based on various sources (2024) – with major processing by Our World in Data
% Last updated: November 13, 2025
% Next expected update: November 2026
% Date range: 1990–2024 (AM: but still incomplete for many countries after 2020)
% Unit: tonnes per person

Running it, creates xlsx output file for consumption-based CO2 emissions matching EXACTLY (including EMPTY columns) the structure of the above-mentioned input (raw data source) file downloaded first from the World Bank (to be used further):
'ConsCO2pc_ExcelTableConversion_ExactMatch_EmptyColumns_MATLABGemini_AM260316.xlsx'


Preliminary Stage 1b
Then run the code:
GPS2pcConsBased_ExcelTable_GeminiAM260318.m
which uses as input real consumption data in
'API_NE.CON.PRVT.PP.KD_DS2_en_excel_v2_5530.xls';

and population data in

'API_SP.POP.TOTL_DS2_en_excel_v2_11.xls';

to create as output real consumption per capita (to be used further):

API_NE.CON.PRVT.PC.PP.KD_MATLAB.xlsx';


Calculation Stage 2: Greening prosperity stripe calculation and plotting

The latter two ‘resulting’ xlsx output files, together with 6 other (as listed above and specified below), are then used to create the GPS visualizations, in 4 versions, as follows:

(1) Consumption-based GPRs with static winsorization anchored at the 2020 distributions (graphs in main text)
The code:
GPS2ConsBased_All4FigsByC_WinsorSTATIC2020_GeminiAM260318v0811.m
uses as unput data from:

consFile = 'API_NE.CON.PRVT.PC.PP.KD_MATLAB.xlsx';
co2consFile  = 'ConsCO2pc_ExcelTableConversion_ExactMatch_EmptyColumns_MATLABGemini_AM260316.xlsx';

to create all figures and to save them as output in:
outDir = 'Stripes2Cons_STATIC_2020_AllColorbars_1990_2020';


(2) Production-based GPRs with static winsorization anchored at the 2020 distributions (graphs in main text)
The code:
GPS1ProdBased_All4FigsByC_WinsorSTATIC2020_GeminiAM260318v0811.m
uses as input data from:

RGDPFile = 'API_NY.GDP.PCAP.PP.KD_DS2_en_excel_v2_5607670.xlsx';
co2prodFile  = 'API_EN.ATM.CO2E.PC_DS2_en_excel_v2_5607813.xlsx';

to create all figures and to save them as output in:
outDir = 'Stripes1Prod_STATIC_2020_AllColorbars_1990_2020';


(3) Consumption-based GPRs with dynamic winsorization of the global panel data distributions (graphs in appendix)
The code:
GPS2ConsBased_All4FigsByC_WinsorDYNAMIC_GeminiAM260318v0812.m
uses as unput data from:

consFile = 'API_NE.CON.PRVT.PC.PP.KD_MATLAB.xlsx';
co2consFile  = 'ConsCO2pc_ExcelTableConversion_ExactMatch_EmptyColumns_MATLABGemini_AM260316.xlsx';

to create all figures and save them as output in:
outDir = 'Stripes2Cons_DYNAMIC_2020_AllColorbars_1990_2020';


(4) Production-based GPRs with dynamic winsorization of the global panel data distributions (graphs in appendix)
The code:
GPS1ProdBased_All4FigsByC_WinsorDYNAMIC_GeminiAM260318v0811.m
uses as input data from:

RGDPFile = 'API_NY.GDP.PCAP.PP.KD_DS2_en_excel_v2_5607670.xlsx';
co2prodFile  = 'API_EN.ATM.CO2E.PC_DS2_en_excel_v2_5607813.xlsx';

to create all figures and save them as output in:
outDir = 'Stripes1Prod_DYNAMIC_2020_AllColorbars_1990_2020';


Alexander Mihailov (University of Reading)
Sunday, 13 September 2026
