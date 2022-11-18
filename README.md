# MTUOC-aligner
Scripts and programs to automatically align text files using Hunalign or SBERT.

This repository offers a series of Python scripts and programs to facilitate the process of automatic text text alignment using Hunalign or SBERT. To align the text files, they should be segmented. You can use [MTUOC-segmenter](https://github.com/aoliverg/MTUOC-segmenter), or any other program to segment the files prior aligning them. If you plan to use Hunalign, don't forget to add the paragraph mark (\<p\>) when segmenting the files.

Before starting the alignment procedure, organize the files in the following way.

* Put all the source language segmented files in one directory (por example text-eng). 
* Put all the tarfet language segmented files in one directory (por example text-spa).

The source and target files should have the same name for both languages (for example, the source files: fileA.txt, file-B.txt, file_C.txt and the corresponding target files with exactly the same name, fileA.txt, file-B.txt, file_C.txt) or alternativelly, with a language code attached to the name  fileA-eng.txt, file-B-eng.txt, file_C-eng.txt and fileA-spa.txt, file-B-spa.txt, file_C-spa.txt).

Once you have organized the files in such way, you can start the alignment procedure.

## 1. Alignment with Hunalign

The programs MTUOC-aligner-hunalig.py (for the use in command line) and MTUOC-aligner-hunalign_GUI.py (with a Graphical User Interface, that is also provided as a Windows executable, MTUOC-aligner-hunalign_GUI.exe)

### 1.1. Bilingual dictionaries for alignment with Hunalign

To help to align we can use a bilingual dictionary. The bilingual dictionaries to use should be in the Hunalign format, that is: target_language_word @ source_language_word. For example, the English-Catalan dictionary would include the followint entries:

```
sionisme @ Zionism
abacà @ abaca
àbac @ abacus
abampere @ abampere
abandó @ abandonment
abandonament @ abandonment
reducció @ abatement
abadia @ abbey
...
```

You can download some alignment dictionaries created from the transfer dictionaries of the Apertium machine translation system from: [https://github.com/aoliverg/hunapertium](https://github.com/aoliverg/hunapertium). 

The use of bilingual dictionaries is not compulsory, you can indicate an empty file (null.dic).


### 1.2. Alignment with Hunalign using the command line

To prepare the aligment script we use the program MTUOC-aligner-hunalign.py. To see the parameters use the -h option:

```python3 MTUOC-aligner-hunalign.py -h 

usage: MTUOC-aligner-hunalign.py [-h] --dirSL DIRSL --dirTL DIRTL --dirALI DIRALI --dictionary DICTIONARY --script
                                 SCRIPT [--r1 R1] [--r2 R2] [--windows]

A script to create the align script to be used with hunalign.

optional arguments:
  -h, --help            show this help message and exit
  --dirSL DIRSL         The input dir containing the segmented text files for the source language.
  --dirTL DIRTL         The input dir containing the segmented text files for the target language.
  --dirALI DIRALI       The output dir to save the aligned files.
  --dictionary DICTIONARY
                        The bilingual dictionary to use.
  --script SCRIPT       The name of the alignment script.
  --r1 R1               The first string for name replacement.
  --r2 R2               The second string for name replacement.
  --windows             Create a bat file for Windows.
```

Following the name of the directories in the examples above we can write:

```
python3 MTUOC-aligner-hunalign.py --dirSL text-eng --dirTL text-cat --dirALI alignments-eng-cat --dictionary hunapertium-en-ca.dic --script alignscript.sh --r1 eng.txt --r2 cat.txt
```

Further explanation of r1 and r2 paramenters should be given. These parameters indicates the endings of the file names that you should substract to make the source and target language file names equal. For example, if you have fileA-eng.txt and fileA-cat.txt you should indicate r1=-eng.txt and r2=-cat.txt to convert both names to fileA. **BUT** in this parameters you can not include hyphens (-), so you should indicate **--r1 eng.txt** and **--r2 cat.txt**.

And a script with the alignment instructions will be created, containing several lines as the following:

```
timeout 5m ./hunalign hunapertium-en-ca.dic -utf -realign -text "text-eng/fileA-eng.txt" "text-cat/fileA-cat.txt" > "alignments-eng-cat/ali-fileA-eng.txt"
```

To run the alignment process, give execution permisions to this script and to hunalign:

```
chmod +x alignscript.sh
chmod +x hunalig
```

Then run the script:

```
./alignscript.sh
```

And the alignment process will start. Once finished the alignment, select the alignments based on the confidence score as explained in section *3. Selecting the alignments*.

If you're working on Windows, dont forguet to use the option --windows and use a .bat extension for the script file. The created instructions will be slightly different:

```
hunalign.exe hunapertium-en-ca.dic -utf -realign -text t "text-eng/fileA-eng.txt" "text-cat/fileA-cat.txt" > "alignments-eng-cat/ali-fileA-eng.txt"
```

Then you can run the bat file (either in the terminal or double-clicking on it.

### 1.2. Alignment with Hunalign using GUI version

The GUI version offers an intuitive interface to perform the same process. Remember that this version is distributed both as Python script and as a Windows executable file. Once you run the program, the following interface will appear:

![](https://github.com/aoliverg/imageswiki/blob/main/MTUOC-aligner-hunalign_GUI.PNG)

Simply fill all the required information and press the button **Create script!**.

Further explanation of Source lang. ending and Target lang. ending fields should be given. These parameters indicates the endings of the file names that you should substract to make the source and target language file names equal. For example, if you have fileA-eng.txt and fileA-cat.txt you should indicate -eng.txt and -cat.txt to convert both names to fileA. **BUT** in this parameters you can not include hyphens (-), so you should indicate **eng.txt** and **cat.txt**.

## 2. Alignment with SBERT


## 3. Selecting the alignments
