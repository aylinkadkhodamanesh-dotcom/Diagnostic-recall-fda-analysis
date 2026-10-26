# Diagnostic-recall-fda-analysis
Why are diagnostic devices recalled?

An analysis of 7,004 real In Vitro Diagnostic (IVD) device recalls published by the U.S. Food and Drug Administration (FDA), looking at how many trace back to design and which design control step failed.

Motivation

Design controls exist to catch problems before a product reaches patients. I wanted to see, with real data, where design quality actually breaks down in diagnostics: how often recalls come from design rather than manufacturing, how much of that is software, and what real failures look like when you map them back to the design control process.

Data
Source: openFDA device recall database, downloaded in full through the openFDA download service
59,552 medical device recall records in total
7,004 diagnostic device recalls, selected by regulation number (Title 21 of the U.S. Code of Federal Regulations, parts 862, 864 and 866)
Largest specialties: clinical chemistry (3,430), microbiology (1,453), hematology (1,028)
Method
Downloaded every device recall with Python and kept only diagnostic devices
Reviewed all 41 official root cause categories and grouped them into design (original design and design changes), manufacturing, labeling error, regulatory, use and unknown
Calculated the design share of all recalls and of recalls with a known cause, and the software share of design failures
Looked at the trend by year
Read a random sample of design recalls and mapped each one to the design control step that failed: user needs, design input, verification, validation or design change control

The grouping rule: a recall counts as design when the problem was built into the product before it reached the factory. Changes to an approved design count as design too, because design change control is part of design controls.

Findings
	Recalls	Share
Design, original and changes	1,614	23% of all diagnostic recalls
Design, among recalls with a known cause		36%
Software within design failures	764	47%
Root cause unclear (other, under investigation, unknown, pending)	2,525	36% of all diagnostic recalls
More than one in three diagnostic recalls with a known cause traced back to design.
Software was almost half of those design failures, and software design (647) was a larger single category than device design (598).
A large share of recalls had no clear root cause, which shows how hard, and how important, good root cause analysis is.
Case studies

Horiba Medical, liver enzyme (AST) assay, 2012. Very high values (800 and 1,000 U/L) were reported as 280 and 199 with no alarm, so a doctor could underestimate serious liver damage. The missing piece was a design input: results above the measuring range must be flagged instead of reported as a number. It was caught during validation on a new analyser.

Tosoh Bioscience, several immunoassays, 2018. Asfotase alfa, a drug for the rare bone disease hypophosphatasia, interferes with the results. The drug is the enzyme alkaline phosphatase, which the assays also use to produce their signal, and it was approved after the assays were launched. The probability is low, but the error is serious and invisible to the lab, while the fix is simple: a warning in the instructions and a notice to labs. It shows that design is not finished at launch, and that post market information has to feed back into the risk file.

A recurring hazard. Two different manufacturers (Ortho Clinical Diagnostics in 2014, Abbott in 2021) had analyser software that did not reliably stop work with expired calibration or reagents.

Limitations
Each record is one recalled product; one recall event can cover several products
Root causes are assigned by the firm and the regulator, and more than a third are unclear
Recalls without a regulation number in openFDA are not in the diagnostic subset
Grouping causes involves judgement; the rules are written out in the notebook and can be changed and rerun

Next step

Train a simple text model on the free text recall reason to predict the root cause group, and check it with cross validation against the official labels.
