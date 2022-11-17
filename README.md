# MTUOC-aligner
Scripts and programs to automatically align text files using Hunalign or SBERT.

This repository offers a series of Python scripts and programs to facilitate the process of automatic text text alignment using Hunalign or SBERT. To align the text files, they should be segmented. You can use [MTUOC-segmenter](https://github.com/aoliverg/MTUOC-segmenter), or any other program to segment the files prior aligning them. If you plan to use Hunalign, don't forget to add the paragraph mark (\<p\>) when segmenting the files.

Before starting the alignment procedure, organize the files in the following way.

* Put all the source language segmented files in one directory (por example text-eng). 
* Put all the tarfet language segmented files in one directory (por example text-spa).

The source and target files should have the same name for both languages (for example, the source files: fileA.txt, file-B.txt, file_C.txt and the corresponding target files with exactly the same name, fileA.txt, file-B.txt, file_C.txt) or alternativelly, with a language code attached to the name  fileA-eng.txt, file-B-eng.txt, file_C-eng.txt and fileA-spa.txt, file-B-spa.txt, file_C-spa.txt).

Once you have organized the files in such way, you can start the alignment procedure.

## 1. Alignment with Hunalign

## 2. Alignment with SBERT
