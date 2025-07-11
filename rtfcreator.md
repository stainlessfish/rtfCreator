﻿# Documentation for the `rtfcreator` package.
  
----------------------------------------------------------------
 
 *RTF Creator* 
  
----------------------------------------------------------------
 
### Version information:
  
- Package: rtfcreator
- Version: 0.0.1
- Generated: 2025-07-09T14:44:10
- Author(s): Hiroki Yamanobe
- Maintainer(s): Hiroki Yamanobe
- License: MIT
- File SHA256: `F*465A7365A4ADB10DC21E7B401735D1C137DBA14797B781FDFF89581900C815AF` for this version
- Content SHA256: `C*C5035262CA613AD76A890417502ED371C99498B8FCE47D813DBCC621A7C3D328` for this version
  
---
 
# The `rtfcreator` package, version: `0.0.1`;
  
---
 
## rtfcreator ##
This is a package that allows you to easily create RTF files.
You only need to specify the -dataset name-, -number of columns-, -variable names-, -left or right justyfy-, and -width-.
If you have your own STYLE template, you can also specify it.
  
---
 
  
---
 
Required SAS Components: 
  - Base SAS Software
  
---
 
 
--------------------------------------------------------------------
 
*SAS package generated by SAS Package Framework, version `20241207`*
 
--------------------------------------------------------------------
 
# The `rtfcreator` package content
The `rtfcreator` package consists of the following content:
 
1. [`%rtfcreator()` macro ](#rtfcreator-macros-1 )
2. [`%rtfddefine()` macro ](#rtfddefine-macros-2 )
  
 
3. [License note](#license)
  
---
 
## `%rtfcreator()` macro <a name="rtfcreator-macros-1"></a> ######

This is a macro that allows you to easily create RTF files.

You only need to specify the “dataset name,” “number of columns,” “variable names,” “left or right justyfy,” and “width.”
If you have your own STYLE template, you can also specify it.

Parameter: 
(Required)DS: Name of the dataset
(Required)COLNUM: Number of columns
(Required)VARLST: List of variable names
(Required)JUSTLST: List of justifications (e.g., left, right, center)
(Required)WIDTHLST: List of column widths
(Optional)OUTFILE: Output file name
(Optional)PAGEVAR: Page break flag variable
(Optional)LINEVAR: Bottom border flag variable
(Optional)TBLHEAD: Text of table top
(Optional)TBLFOOT: Foot of table bottom

** Example A  -- Simply;
**********************;
%rtfcreator(DS=sashelp.class
,COLNUM  =2
,VARLST  =name sex 
,JUSTLST =Left Center
,WIDTHLST=300 150 
);
** Example B -- use your STYLE template.;
**********************;
%rtfcreator(DS=sashelp.class
,COLNUM  =2
,VARLST  =name sex 
,JUSTLST =Left Center
,WIDTHLST=300 150 
,STYLENAM=Journal
);
** Example C -- Add text outside the table, bottom or top;
**********************;
%rtfCreator(DS=sashelp.class
,COLNUM  =2
,VARLST  =name sex 
,JUSTLST =Left Center
,WIDTHLST=300 150 
,TBLHEAD=%str(Table Head)
,TBLFOOT=%str(Table Foot)
);
** Example D -- Page break (you need to create a page break flag variable in advance, e.g., XXX = 1).;
**********************;
data RTFDS1;
  set sashelp.class;
  if _n_ eq 7 then PAGEBRK=1;
run;
%rtfcreator(DS=RTFDS1
,COLNUM  =2
,VARLST  =name sex 
,JUSTLST =Left Center
,WIDTHLST=300 150 
,PAGEVAR=PAGEBRK
);
** Example E -- adding a bottom border (you need to create a bottom border flag variable in advance, e.g., XXX = 1).;
**********************;
data RTFDS2;
  set sashelp.class;
  if _n_ eq 7 then BLINE=1;
run;
%rtfcreator(DS=RTFDS2
,COLNUM  =2
,VARLST  =name sex 
,JUSTLST =Left Center
,WIDTHLST=300 150 
,PAGEVAR=PAGEBRK
,LINEVAR=BLINE
);

  
---
 
## `%rtfddefine()` macro <a name="rtfddefine-macros-2"></a> ######

This is a macro for creating RTF styles.

By simply specifying the font and font size, you can create a template style using PROC TEMPLATE.

Parameters:
(Optional: default=PORTRAIT)LAYOUT: Page orientation -- either "PORTRAIT" or "LANDSCAPE"
(Optional: default=STUDY_RTF)STYLENAM: Name of the style to be created
(Optional: default=MS Mincho)FONT: Font name
(Optional: default=8pt)FONT_SIZE: Font size

  
---
 
  
---
 
# License <a name="license"></a> ######
 
	Copyright (c) since 2025, Hiroki Yamanobe

  Permission is hereby granted, free of charge, to any person obtaining a copy  
  of this software and associated documentation files (the "Software"), to deal 
  in the Software without restriction, including without limitation the rights  
  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell     
  copies of the Software, and to permit persons to whom the Software is         
  furnished to do so, subject to the following conditions:                      
                                                                                
  The above copyright notice and this permission notice shall be included       
  in all copies or substantial portions of the Software.                        
                                                                                
  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR    
  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,      
  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE   
  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER        
  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, 
  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE 
  SOFTWARE.
  
---
 
