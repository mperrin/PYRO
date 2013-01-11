
File Formats
===============

Proper formatting of the target list files 
--------------------------------------------------------------

**(input with -t, --targetlist flags)**

The default format is the standard Magellan telescope operator format.  For convenience, however, it is possible to define your own custom-made format by doing the following::

Custom file formats are read directly from the file itself (assumed to be an ASCII text file), and are stored in lines that begin with \'###\'.  In these lines, the next column defines the attribute type, and the one after gives the relevant value (which is often the column number that contains the relevant information; column numbers start at 0).  Columns after that are ignored.  Below is full list of attribute types via example.  The example file is assumed both to be for Magnesium II quasar targets and to have the following format:\nname redshift ra dec Jmag zmag exposure-time weight code comments\nExample:\n

### RESET (No other argument necessary) Resets all the below marker values to their default values.  Necessary when more than one list type is included within one target file.
### RA_DEC_TYPE 0 Defines whether units are hh:mm:ss and deg:arcmin:arcsec (==0), decimal (==1), or the sources are SDSS sources and the location is to be read from the name (==2).  MANDATORY.
### RA_COL 2 Defines column that holds the Right Ascension.  MANDATORY if RA_DEC_TYPE is 0 or 1.
### DEC_COL 3 Defines column that holds the Declination.  MANDATORY if RA_DEC_TYPE is 0 or 1.
### NAME_COL 0 Defines column that holds the name of the object.  MANDATORY.

# All other source list keywords are optional.  If not provided, the code attempts to compensate for their absence in various ways.  

### LABEL MG_II Defines the object label.
### REDSHIFT_COL 1 Defines column that holds the redshift of the object.*
### MAG_COL 4 Defines column that holds the magnitude.*
### MAG_BAND Jmag Describes what band is represented by the data in MAG_COL.
### MAG_COL2 5 Defines column that holds a second value of the magnitude.*
### MAG_BAND2 zmag Describes what band is represented by the data in MAG_COL2.
### EXP_COL 6 Defines column that holds the exposure time.
### WEIGHT_COL 7 Defines the scheduling priority-weight column.
### COMMENT_COL 9 Defines the comment column.
### MAG_UNKNOWN ? Defines the symbol used when a source within the list's magnitude is unknown.
### FILTER_COL 8 Defines a column used to filter data (optional).
### FILTER_VAL a;b;c; Semi-colon separated list of acceptable values to by pass the filter.

if REDSHIFT_COL==COMMENT_COL, MAG_COL==COMMENT_COL, or MAG_COL2==COMMENT_COL,
then the redshift and/or magnitudes are expected to be separated from the other
comments by semi-colons and preceded by \'z=\' and/or \'MAG_COL(2)=\',
respectively where MAG_COL or MAG_COL2 are the strings defined by the above
markers of the same name (for example, \'blah;z=4.5;J=15.7;blah2\' is the
correct comment if \'### MAG_BAND J\' is given)


Since the comments in this example would be ignored by the code, feel free to
cut and paste this section into your target list.  These informational columns
need not be placed at the beginning of the file.  Therefore, one could change
types midway through a target list (but be careful to reset the defaults using
### RESET!).  Commented (#) and empty lines are ignored.


Proper formatting of the telluric files 
--------------------------------------------------------------

(input with --telluric flag)


Telluric files follow the same format as Target files, with the catalogue
format of the Magellan telescope operators being the default.  The one
exception is that telluric files have an extra marker:

### SPEC_COL 6 (or whatever number)
This column represents the spectral type of the telluric.  (Target files may use the marker as well, if desired, but it has no effect on the scheduler.)

Proper formatting of the priority source files 
--------------------------------------------------------------


(input with -P, --Priority flags)

Priority source files should be ASCII text files with one source name per line.
To determine matches, pyro searches input target names for the substrings
contained in these lines.  Thus, full source names are not required (but be
careful not to assign priority to less worthy sources by putting a small
substring in the priorities file, such as \'SDSS1\', which is likely to match
many sources). Commented (#) and empty lines are allowed, and are ignored.


