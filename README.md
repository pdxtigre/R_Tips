# R_Tips

## Installing Packages within a Firewall
Here is how we should do when installing within a Firewall. Basically, we will have to disable https (secured connection)

Select **Tool** --> **Global Options**

Then go to *Packages**, uncheck **"Use secure download method for HTTP**, then click **Apply** button

After this the user will be able to install any packages.

## Bonus
to load user libs automatically at startup follow these steps

run this from R prompt
file.edit("~/.Rprofile")

Add these lines and modify per your personal choices to select the user library to run, also set the working directory if needed

```r
# First routine for R initialization

.First <- function() {
  cat("**************************************************************************************\n")
  cat("Initializing R session..\n")
  cat("**************************************************************************************\n")
 
  # User libs
  # .libPaths(c(Sys.getenv("R_LIBS_USER"), .libPaths()))
  # Sys.getenv("USERPROFILE")
  cat(paste("User library located: ", Sys.getenv("R_LIBS_USER"), "\n"))

  # Update your user library list here     
  myLibs <- c("glue", "ggplot2", "tidyr", "readxl")
  for (lib in myLibs) {
    cat(paste("Loading: ", lib, "\n"))
    library(lib, character.only = TRUE)
  }
 
  # Working directory
  setwd(path.expand("~/@SJSU/09-ISE-240/#R_Workspace"))
  cat(paste("Workspace located: ", getwd(), "\n"))
 
 
  cat("**************************************************************************************\n")
  cat("Welcome Boss! Your R session is ready.\n")
  cat("**************************************************************************************\n")
}
```

.First is the first function that will be run on every R session
