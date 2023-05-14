# TCR2Rep_win64
### Pipeline description :  
The pipeline processes raw TCR sequences and exports a data table containing all IgBlast annotation, clonal assignment and clonal frequency data.
The pipeline also performs bioinformatic analyses, such as: clonal size distribution ,  CDR3 lengths distribution and VDJ segments frequencies.

### Installation (manual): 
1. Download and Install the latest version of Anaconda from here: https://www.anaconda.com/download
2. From the Start menu, search for and open "Anaconda Prompt".
3. From "Anaconda Prompt" install git by typing:  ```conda install -c anaconda git```
5. From "Anaconda Prompt" download TCR2Rep pipeline scripts by typing: ```git clone https://github.com/morhavap/TCR2Rep_win64.git```
7. Get into "TCR2Rep_win64" folder: ```cd TCR2Rep_win64```
9. Create the environment for TCR2Rep in "Anaconda Prompt" by typing:	
```conda env create -f TCR2Rep.yml ```
```conda activate TCR2Rep```
12. Run this commands at "Anaconda Prompt":
a.	Add bash cmd environment:
```conda install m2-base``` 
b. Add PERL cmd environment:
```conda install -c anaconda perl```
c.	Add seqkit package:
```conda install -c derkevinriehl seqkit```
13. download and install IGBlast for windows from here: https://ncbi.github.io/igblast/cook/How-to-set-up.html
(Important - Save your IgBlast download directory. This is usually saved under a folder "C:\Program Files\NCBI")
Move "igblast-1.21.0 " folder into "TCR2Rep" folder. (you can find "TCR2Rep" path by typing: "pwd" in "Anaconda Prompt").
14. Download Imgt database: (You can get a more extensive explanation here.)
1.	At "igblast-1.21.0 " folder create new folder with the name – "database" by typing:
```mkdir database```
```cd database```
2.	Create 3 new txt file at "database" folder. (right button -> new -> text document)
Save the files with this names: "Human_TRV","Human_TRD","Human_TRJ".
3.	Go here, and copy all Human v genes of TCR (i.e. -  TRAV, TRBV, TRGV, TRDV) into "Human_TRV" file (one after the other), all D genes of TCR into " Human_TRD" file and all J genes of TCR into "Human_TRJ" file. 
4.	Now, run this commands for each file to filter out duplicate sequences and prepare the files to igblast: (change just the gene segment V\D\J in the filename)

```seqkit rmdup -s < Human_TRV > human_TRV_filtered```

```<your_path_to_bin_dir>/edit_imgt_file.pl human_TRV_filtered > "human_TRV_igblast" ```

```<your_path_to_bin_dir>/makeblastdb -parse_seqids -dbtype nucl -in "human_TRV_igblast" ```

Note: "database" folder contains IMGT VDJ TCR database. It is important to update this folder once in a while according to the changes published here. 
14. Run TCR2Rep pip by typing at "Anaconda Prompt":

```bash "<your/tcR2Rep_pipeline_folder/path>TCR2Rep_pipeline.bash" <fastq_file_path> <sample_name> <length_threshold> <quality_threshold> <output_path> <igblastn_path> <igblast_dir_path> <TCR2Rep_pipeline_folder_path>```




