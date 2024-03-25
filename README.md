# excel-for-usearch

replace cf. beauvoisii to cf.beauvoisii 
change rows 21872 to 21964 to Grateloupia turuturu chloroplast rbcL gene for ribulose Grateloupia turuturu chloroplast rbcL gene for ribulose 15-bisphosphate carboxylase/oxygenase large subunit partial cds specimen voucher: KU-d12359 DEFINITION


````
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
