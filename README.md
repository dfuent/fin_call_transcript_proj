# fin_call_transcript_proj
- NLP project analyzing financial-earnings transcripts 

Each section in the fin_aggregated.ipynb notebook can run standalone. 
It takes about an hour to run the entire notebook.
Each section flows into the next; e.g. Section A produces files, section B might reference them.

The notebook takes two mapping files as input:
-	LoughranMcDonald_MasterDictionary_2020.csv
-	sp_mapping.csv
The entire notebook can run with just these mapping files and the raw_data_files¬ folder within proj_data.

Section 1:
-	This section does not need run for the rest of the code to work
-	Contains the web scraper used to pull the transcript data. Each time I ran this section, a raw HTML file was produced. 

Input Files: None

Output Files: 

- Raw HTML output (contained in the raw_data_files folder)

Section 2:
-	Contains code to combine and clean the raw HTML

Input Files: 

- the set of files df_rawComp_v….csv produced in Section 1 (in raw_data_files folder).
- sp_mapping.csv mapping file.

Output Files: 

- F0 document, F0_rawAll.csv, which is the combination of all the files produced in Section 1. File contains URLs, transcripts, and raw file names.
- data_clean.csv, which contains transcripts and data for each call, like company and date.
- companies.csv, which is similar to F0 and contains transcript URL, call title (company, ticker, date, quarter), and file location.

Section 3:
-	Contains code to add financial data to dataset.
-	Pulling data from Yahoo Finance takes some time.

Input Files: 
- data_clean.csv

Output Files: 
- comps_prices.csv, which is a table containing date, ticker, market cap, and closing price for each company from the min call date through August 12, 2021.
- data_clean2.csv, which contains the data produced in Section 2, but with financial data appended to it along with some qualitative variables, like Q&A flagging. 
- price_map.csv, which also contains some financial information (this file is used as a mapping table later in the modeling section).*

Section 4: 
-	Section produces OHCO-indexed files for analysis

Input Files:

- data_clean2.csv

Output Files: 

- LIB.csv
- CALL.csv, which contained transcripts and price data grouped by ticker, quarter, and Q&A.
- speaker_call.csv, which contains the transcripts grouped by ticker, speaker, call quarter, and Q&A.
- COMPANY.csv, which contains all transcripts grouped by ticker
- transition_call.csv, which contains each transcript split by transition between speakers
- TOKENS.csv
- VOCAB.csv

Section 5:
-	Section produces much of the text analysis. Also contains some model prep (via sentiment analysis and PoS tagging).
-	FYI: The VADER section takes a while to run. THETA and PHI take time to run as well.

Input Files:

- TOKENS.csv
- VOCAB.csv
- LIB.csv
- transition_call.csv
- LoughranMcDonald_MasterDictionary_2020.csv
- CALL.csv
- price_map.csv

Output Files:
- reduced_TFIDF.csv
- model_vars.csv, contains info for modeling with Q&A split (NOT USED)
- model_vars_noQA.csv, model used for modeling

Section 6:
-	Section models on the data and produces performance metrics and visualizations. 
-	To test model performance, I run each potential model to predict all 90 close prices after every call. This takes some time.

Input Files: 
- LIB.csv
- model_vars_noQA.csv

Output Files:
- model_performance_ALL.csv
