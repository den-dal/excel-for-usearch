# usearch
````
1. Transform the alignment of sequences into a fasta file (example: RED_ALGAE_USEARCH_SHORT_220324.fas)
2. Go to the directory (folder) where the fasta file is and make sure that the execuatble for USEARCH is also in the same directory.
3. Open the directory in terminal
4. Code:
.\usearch11.0.667_win32.exe -allpairs_global RED_ALGAE_USEARCH_SHORT_220324.fas -acceptall -userout OUTPUT.txt -userfields query+target+id+bits+qcov+tcov

By prefixing .\, you're indicating to PowerShell that the executable should be executed from the current directory. This was done because without .\ there was the error: "The term 'usearch11.0.667_win32.exe' is not recognized as the name of a cmdlet, function,
script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again."

5. The Output.txt file is saved in the directory.

The output you provided appears to be in a tabular format. Here's a breakdown of what each field in the output represents:

Query: The name or identifier of the query sequence (in this case, "Acrochaetium secundatum plastid complete genome").
Target: The name or identifier of the target sequence from the reference database (in this case, "Galaxaura pacifica chloroplast rbcL gene for ribulose-15-bisphosphate carboxylase/oxygenase large subunit note: SAP 095744").
Identity (%): The percentage identity between the query and target sequences. This indicates the level of similarity between the two sequences.
Bitscore: The bitscore value, which is a measure of the significance of the alignment between the query and target sequences. Higher bitscore values indicate a more significant alignment.
Query Coverage (%): The percentage of the query sequence that aligns with the target sequence. This indicates how much of the query sequence is covered by the alignment.
Target Coverage (%): The percentage of the target sequence that aligns with the query sequence. This indicates how much of the target sequence is covered by the alignment.

Example:
Acrochaetium secundatum plastid complete genome. DEFINITION  Acrochaetium secundatum plastid complete genome.	Galaxaura pacifica chloroplast rbcL gene for DEFINITION  Galaxaura pacifica chloroplast rbcL gene for ribulose-15-bisphosphate carboxylase/oxygenase large subunit note: SAP 095744.	84.8	0	100	100
SO, the query sequence "Acrochaetium secundatum plastid complete genome" has a high percentage identity (84.8%) with the target sequence "Galaxaura pacifica chloroplast rbcL gene for ribulose-15-bisphosphate carboxylase/oxygenase large subunit note: SAP 095744". The alignment covers 100% of both the query and target sequences.

This output provides information about the similarity between your query sequences and the reference sequences in your database, which can help you assess sequence variability and identify matches between sequences from different species.
````
# Editing and analysing results in excel:
````

Just obtain genera and species from the query column and from the target column by separate text into column. then compare if query and target are from the same genus and from the same species.


These other analyses were actually unnecessary, but here there are anyway: 

replace cf. beauvoisii to cf.beauvoisii 
change rows 21872 to 21964 to Grateloupia turuturu chloroplast rbcL gene for ribulose Grateloupia turuturu chloroplast rbcL gene for ribulose 15-bisphosphate carboxylase/oxygenase large subunit partial cds specimen voucher: KU-d12359 DEFINITION

FIRST STEP:

=IF(ISNUMBER(SEARCH("SAP",A2)),RIGHT(A2, LEN(A2)-SEARCH(" SAP",A2)),"")

Explanation:
in column SAP: (column B)
=IF
(ISNUMBER(SEARCH("SAP",A2)), value if true, value if false)
Si
la celda [A2] contains "SAP", value true, value false

value if true: RIGHT(A2, LEN(A2)-SEARCH(" SAP",A2))
extraer characteres a la derecha despues de " SAP"

SECOND STEP:
in column voucher: (column C)
=IF(ISNUMBER(FIND("voucher", A2)), MID(A2, FIND("voucher", A2), FIND("DEFINITION", A2) - FIND("voucher", A2)), "")

extraer caracteres despues de voucher y antes de DEFINITION
This formula finds the position of "voucher" using FIND, then finds the position of "DEFINITION". It then extracts the substring between the positions of "voucher" and "DEFINITION" using MID. If "voucher" is not found in the text, it returns an empty string ("").

THIRD:
in column isolate: (column D)
=IF(ISNUMBER(FIND("isolate", A2)), MID(A2, FIND("isolate", A2), FIND("DEFINITION", A2) - FIND("isolate", A2)), "")

FOURTH.
Select column A --> text to colums (column E)
column E genus
Column F species


=CONCATENATE(E2," ",F2," ",B2," ",C2," ",D2," ",G2)




Extraer texto antes de DEFINITION
=LEFT(A2, SEARCH(" DEFINITION",A2))
then copy this as value to another column (Column D) to get the text

then remove some useless text 
replace:
 ribulose-15-bisphosphate carboxylase/oxygenase large subunit (rbcL) gene partial cds chloroplast.
ribulose-15-bisphosphate carboxylase/oxygenase 
ribulose-15-bisphosphate carboxylase/oxygenase
ribulose-15-bisphosphate carboxylase 
ribulose 15-bisphosphate carboxylase large
 chloroplast rbcL gene for ribulose
 chloroplast rbcL gene for 
````
in the column next to SAP
=IF(ISNUMBER(SEARCH("_voucher",A21872)),RIGHT(A21872, LEN(A21872)-SEARCH("_voucher",A21872)),"")
