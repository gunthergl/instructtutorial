# Basics of clustering

# 1. Introduction 
In this tutorial we will analyse a public data set (Georg et al. 2021, https://doi.org/10.1016/j.cell.2021.12.040) of single cell phospho-proteomics measured with Cytometry by Time of Flight (CyTOF). 

In this study, the authors performed CyTOF of whole blood samples from mild and severe COVID-19 patients during the acute and convalescent phase, and patients with other acute respiratory infections (Flu-like illness), as well as patients chronically infected by human immunodeficiency virus (HIV) or hepatitis B (HBV) and healthy controls. They analysed the T cell space and identified highly activated CD16+ T cells in severe COVID-19, which led the authors to hypothesise about the pathological role of these cytotoxic T cells. This hypothesis was then tested and confirmed with functional analyses, and found suitable mechanisms for their induction.

In this tutorial you will learn how to perform such computational analysis either in T cells, B cells, or monocytes!
We invite you to give a look at the paper before the tutorial.

See you soon!

# 2. How to get the data
Please download the following data in advance! 

https://box.hu-berlin.de/d/a40f4c6d19eb4be68d7e/

# 3. Setup
We will use so called `.Rmd` files which are a combination of R-code and nice formatting. The advantage is that the code and its results are directly connected. 

In the last course, you got an introduction to R and its usage, but we took most of the installation-burden from you. After a year of R-usage you must be R-experts now. Therefore you have to install R locally now, making it easier to use for your own datasets. 

For _Windows_, the installation steps are as follows. For Linux or Mac please reach out to us. 

## 3.1 Setup the necessary `programs`
1. Download R from https://cran.r-project.org/bin/windows/base/
2. Install R. 
3. Download `rtools40-x86_64.exe` from https://cran.r-project.org/bin/windows/Rtools/rtools40.html
4. Install Rtools
5. Download RStudio https://www.rstudio.com/products/rstudio/download/#download
6. Install RStudio 

## 3.2 Setup the necessary `packages`
There are many `packages` in R that hold much functionality you can directly use and do not have to code for yourself. We supply you with a list you should install. 

For that:

1.  Open the installed Rstudio
2.  Create a new file (`File` -> `New File` -> `R Script`)
3.  Copy the following code inside that freshly generated script: 
	```r
	if(!require(pacman)){
		install.packages("pacman") # If not already installed
	}
	pacman::p_install("BiocManager", force=FALSE)
	pacman::p_install("tidyverse", force=FALSE)
	pacman::p_install("cowplot", force=FALSE)
	pacman::p_install("needs", force=FALSE)
	pacman::p_install("pheatmap", force=FALSE)
	pacman::p_install("uwot", force=FALSE)
	
	
	pacman::p_install("ComplexHeatmap", force=FALSE)
	pacman::p_install("devtools", force=FALSE)
	
	devtools::install_github("JinmiaoChenLab/cytofkit")
	devtools::install_github("JinmiaoChenLab/Rphenograph")
	
	
	library(tibble)
	library(tidyr)
	library(readr)
	library(stringr)
	library(ggplot2)
	library(dplyr)
	library(cowplot)
	library(uwot)
	library(Rphenograph)
	library(cytofkit)
	library(ComplexHeatmap)
	library(pheatmap)
	# library(needs)
	theme_set(theme_cowplot())
	```
4. Either run each line of the code (`Ctrl+Enter per line`) or all of the code at once (`Ctrl+Shift+s`)
5. There will be some red messages, but there should be no warnings nor errors.

## 3.3 Project setup
Rstudio has a nice feature to organize projects. 

- On the top right corner there is a button stating `Project: (None)`
- Click on that button and select `New Project`
- --> Select `New Directory`
- --> Select `New Project`
- --> Type in `InstructTutorial_II` as Directory name and select a folder where you want to place it inside. `InstructTutorial_II` must not exist in the selected folder already.

After you set up this project, on the bottom right, find the button `More` and click `Show Folder in New Window`. 

This opens the explorer in the freshly created directory. In this directory: 
	
1. Create a new directory called `code` where you will later place all of the code. 
2. Create a new directory called `data`
3. Copy the `data_norm_sub5.csv` from 2. (https://box.hu-berlin.de/d/a40f4c6d19eb4be68d7e/) into the new `data` directory. 
4. In 3.2 you generated a new code file but did not save it anywhere. Create the file again, now inside the project and save it in the `code` directory under the filename `01_setup.R`


# 4. Github 
You can get all information, the code under https://github.com/gunthergl/instructtutorial as soon as we open it publicly. You do not necessarily go through all of that by yourself. Therefore we will open it rather late before the actual course. 

# 5. Help
Just let us know if you need help: 
	
- Gunther Glehr (`prename`.`surname`@ukr.de)
- Rosario Astaburuaga Garcia (`prename`.`midname`@charite.de)
- Lev Petrov (`prename`.`surname`@charite.de)

