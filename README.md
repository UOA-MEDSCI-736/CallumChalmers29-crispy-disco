#ePygenetics

This programme extracts data from .wig files based on user input. The output of the programme is a database called ePygenetics.csv which contains all data extracted by the user.

##Project Description

This programme was designed as part of Medsci 736, a course on Digital Research Skills at the University of Auckland, New Zealand. 

The project was designed by Dr Justin O'Sullivan from the Liggins Institute who wanted to add the epigenetic status of single nucleotide polymorphisms to his genetic data analysis. 

In simple terms, this programme allows scientists to get extra information about person to person genetic variation. This information can then be used to better understand how genetics is related to disease and to look for treatments for diseases with a genetic component.

The programme was designed using data from the [NIH Roadmap Epigenomics Repository](https://www.ncbi.nlm.nih.gov/geo/roadmap/epigenomics/?search=DNAse+hypersensitivity&display=50) which is open access. A subset of 5 modified files has been included in the ```test-data``` folder for testing the programme.

##Prerequisites:
1. **Python**
  - To run the software you will need Python 3.5.2 or a compatible version
  - Follow [this link](https://www.python.org/downloads/release/python-352/) to download Python 3.5.2 
  - Alternatively under the CC BY-SA 4.0 license you can update the code to be compatible with your own version of python 

2. **Operating System**
 - The programme was scripted for Ubuntu 16.04 LTS, it is yet to be tested for compatibility issues with other operating systems
 - If you are using the file on Windows, on line 13 of ePygenetics.py you will need to change the code to read os.system('cls')

3. **Data File Requirements**
 - The programme can only read Wiggle (.wig) files with a fixed step of 20, see [this link](https://genome.ucsc.edu/goldenpath/help/wiggle.html) for more information about this file type
 - **For the programme to read the files, both the script and the files need to be in the same directory**
 - **At least one .wig file is needed to run the programme**
 - For the output to be valid, all files must use the same genome build see [this link](https://genome.ucsc.edu/FAQ/FAQreleases.html) for more information about genome releases
 - Files must contain a "-" in their name to be read by the programme, whatever text is before the dash will be the column heading in the output database so bear this in mind when naming files

##Running the programme

###To run the programme:

1. Open the command line to folder containing the Python script called ePygenetics
2. Type the command ```python ePygenetics.py```

You will be greeted with a menu with 4 options: 

1. Add a cell line (loading a file)
2. Add a SNP
3. Help
4. Exit

You will then be asked to choose which of the 4 options you would like to do.

###Adding a cell line:
 - You will be asked to enter the name of a cell line to add to the database or 0 to return to the menu
 - If the output database ```ePygenetics.csv``` does not exist, it will be created as part of this process
 - This refers to loading a file into the database 
 - For this action to work the corresponding file must be in the same directory as the python script
 - The file must be named [cell line]-[any text] and it must be a .wig file
 - If you enter a cell line that does not have a corresponding file in the directory an error message will pop up thats asks you to move the file into the directory and then press enter
 - If you enter a cell line that is already in the database, an error message will pop up asking you how you would like to proceed (see below)
 - If you enter 0 you will returned to the menu
 - If you enter a valid cell line, the programme will add a column to the database and search the file for any SNPs that have been entered into the file
 - Once this is complete, the programme will notify you that your cell line was added and ask if you would like to add another cell line, return to the main menu or exit the programme
 - If you press 1, the cycle will repeat
 - If you press 2, the programme will return to the menu
 - If you press 3, the programme will exit

###Adding a SNP:
 - You will be asked to enter the chromosome the desired SNP is on or enter 0 to return to the main menu
 - If you enter a value that is not the number 0-23 or the letters M, X or Y, you will be notified your input is invalid and will be asked to press enter before entering a valid input
 - If you enter 0 you will returned to the main menu
 - Then you will be asked to enter the position of the SNP on that chromosome. The position is the location of that SNP in base pairs.
 - If you enter 0 you will be returned to main menu
 - If the output database ```ePygenetics.csv``` does not exist then it will be created at this point
 - If you enter a SNP that is already in the database, you will be asked how you would like to proceed (see below)
 - At this point the programme will add a row to the database for that SNP
 - The programme will then take the user parameters and use them to search for that SNP in all the files that have been loaded into the database
 - If no files have been loaded, it will simply notify you that your SNP has been added and ask how you want to proceed (see below)
 - The programme will then return the number of contigs that aligned to the section of the genome that covers that SNP for each file. If the region of the genome that contains your SNP is not in the file, the programme will return NaN.
 - The programme will then populate the row of the database using the values it extracted from each file
 - The programme will then notify you that your SNP was added
 - The programme will then ask if you want to add another SNP, want to return to the main menu or exit the programme
 - If you press 1, this cycle will repeat
 - If you press 2, the programme will return to the menu
 - If you press 3, the programme will exit

###Help:
 - You will be redirected to a brief manual that explains what each function does
 - You will then be asked to press enter to continue and you will be redirected to the main menu 

###Exit:
 - The programme will close

###Output:
 - Once you are finished, all the data you have added can be visualised in the output database ```ePygenetics.csv``` which can be found in the same directory as the script. This file can be opened in almost any text editor but is best visualised in Google Docs, Libre or Open Office Calc or Microsoft Excel. 

##Testing the programme
1. Download ```test-data``` and transfer the contents to the same directory as the main script
2. Download the ```test-ePygenetics``` folder and move the entire folder to the same directory as the main script
3. In the main script, delete the last line ```main()``` and save the file
4. To install pytest, open the command line in the directory containing the main script and run the command ```pip install -U pytest```
5. To check this worked correctly type the command ```python -m pytest --version``` and it should return a message similar to this ```This is pytest version 2.9.2, imported from /home/admin736/anaconda3/lib/python3.5/site-packages/pytest.py```
6. Once this is complete, type the command ```python -m pytest```
7. This will collect all the tests in the ```test-ePygenetics``` folder and run them
8. The output should be similar to this:
```============================= test session starts ==============================
platform linux -- Python 3.5.2, pytest-2.9.2, py-1.4.31, pluggy-0.3.1
rootdir: /home/admin736/Desktop/Assignments/CallumChalmers29-crispy-disco, inifile: 
collected 18 items 

test-ePygenetics/test_ePygenetics.py ..................

========================== 18 passed in 0.03 seconds ===========================```
9. This confirms the programme is working correctly, if you do not get this screen, delete and redownload the contents of the GitHub repo and try again
10. Once this is complete, in the main script add the last line ```main()``` back in and save the file




