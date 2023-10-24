[Installation](#installation)

[Starting a New Project](#starting-a-new-project)

[Running the Pipeline](#running-the-pipeline)

## Installation

NOTE: This will only work on a Windows operating system.

1. Install prerequisite packages, as follows:
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
```

2. Install the SAM package, as follows:
```
install.packages(
  "https://github.com/ericgoolsby/SAM/raw/main/data-raw/SAM_0.0.0.9000.zip",
  repos = NULL)
```

3. Run the following code (this creates a directory for pipeline files):
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
1. Open the RStudio project and load the SAM R package as follows: 
```
library(SAM)
```
2. As you did previously, run the following code (replace "SAM_Example" with your project name).
```
SAM::set_project(name = "SAM_Example",RStudio_project = TRUE)
```
3. Load the csv file as follows:
```
data <- read.csv("data.csv")
```
4. If you want to run every trait in the csv file, you can simply run the following:
```
run_pipeline(data = data)
```

Alternatively, if you want to select only a subset of traits, you'll need to set that manually:
```
traits <- colnames(data)[2:ncol(data)]
run_pipeline(data = data,traits = traits)
```
