NOTE: This will only work on a Windows operating system.

[Installation](#installation)

[Starting a New Project](#starting-a-new-project)

[Running the Pipeline](#running-the-pipeline)

## Installation

1. Download and install Java: https://www.java.com/en/download/ **NOTE**: You may need to install both the 32-bit and 64-bit versions.

2. Download and install Rtools (this is NOT an R package -- you have to download it from the website): https://cran.r-project.org/bin/windows/Rtools/ **NOTE** Be sure to select the version of Rtools that correspods to your version of R.

3. Install prerequisite packages, as follows:
```
if (!requireNamespace("tidyverse", quietly=TRUE))
  install.packages("tidyverse")
if (!requireNamespace("qqman", quietly=TRUE))
  install.packages("qqman")
if (!requireNamespace("BiocManager", quietly=TRUE))
  install.packages("BiocManager")
if (!requireNamespace("gdsfmt", quietly=TRUE))
	BiocManager::install("gdsfmt")
if (!requireNamespace("SNPRelate", quietly=TRUE))
	BiocManager::install("SNPRelate")
if (!requireNamespace("BEDMatrix", quietly=TRUE))
  BiocManager::install("BEDMatrix")
if (!requireNamespace("zip", quietly=TRUE))
  BiocManager::install("zip")
if (!requireNamespace("Rfast", quietly=TRUE))
  BiocManager::install("Rfast")
if (!requireNamespace("ggrepel", quietly=TRUE))
  BiocManager::install("ggrepel")
if (!requireNamespace("ggpubr", quietly=TRUE))
  BiocManager::install("ggpubr")
if (!requireNamespace("urltools", quietly=TRUE))
  BiocManager::install("urltools")
if (!requireNamespace("xlsx", quietly=TRUE))
  BiocManager::install("xlsx")
```

4. Install the SAM package, as follows. If you have trouble installing, try closing and restarting RStudio (If issues persist, send a message with the error message).
```
install.packages(
  "https://github.com/ericgoolsby/SAM/raw/main/data-raw/SAM_0.0.0.9000.zip",
  repos = NULL)
```

5. Run the following code (this creates a directory for pipeline files):
```
SAM::set_SAM_dir()
```

### Starting a New Project
1. Create a new RStudio project. Give it a name (do not include any spaces), and also make sure there are no spaces in the file path either -- i.e., under "Create project as subdirectory of:" you should see something like "C:/Users/ericg/Documents". An unacceptable path would be something like "C:/Users/ericg/UCF work/projects" (because of the space between "UCF" and "work").
2. Create a csv file and place it in the directory of your RStudio project. You may use this file as a template or for a tutorial:
```
data <- read.csv("https://github.com/ericgoolsby/SAM/raw/main/data-raw/data.csv")
write.csv(data,"data.csv",row.names = FALSE)
```
3. Run the following code:
```
SAM::set_SAM_dir(RStudio_project = TRUE)
````
4. Run the following code (replace "SAM_Example" with your project name).
```
SAM::set_project(name = "SAM_Example",RStudio_project = TRUE)
```


## Running the Pipeline
1. Open the RStudio project and load the SAM R package and SNP data as follows: 
```
library(SAM)
SAM::get_snp_data()
```
2. As you did previously, run the following code (replace "SAM_Example" with your project name).
```
SAM::set_project(name = "SAM_Example",RStudio_project = TRUE)
```
3. Load the csv file as follows:
```
data <- read.csv("data.csv")
```
4. Run the following code to perform GWAS on every trait in the csv file:
```
traits <- colnames(data)[2:ncol(data)]
gwas_output <- vector("list",length = length(traits))

for(i in 1:length(traits))
{
  gwas_output[[i]] <- SAM::gwas(data = data,trait = traits[i])
}
```
5. Finally, run the pipeline:
```
run_pipeline(data = data)
```

Results can be found in the `Results` folder of the RStudio project directory, in a spreadsheet named `results.xlsx`. Manhattan plots are located in the `Plots` folder. More extensive (but less human-readable) pipeline outputs can be found in the `Tables` folder.
