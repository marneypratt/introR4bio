# Intro to R for Biology

### by Marney Pratt

This webpage details how to download and install the **Intro to R for Biology** Swirl course. Please visit the **[Swirl website](https://swirlstats.com/)** for more information about how to install or develop interactive Swirl lessons.<br>

Please feel free to download and use the **Intro to R for Biology** Swirl course for educational purposes, no commercial uses are allowed.

## Install/Update R and RStudio

The directions below assume you have access to R and RStudio. Check with your instructor to see if you will be using a cloud-based version of RStudio. Even if you will be using a cloud-based version, it is good to have a backup of the software on your computer. If you need or want to install R and RStudio on your computer, you can follow these instructions - **[Installing R and RStudio](https://moderndive.com/1-getting-started.html#installing)**. 

If you already have R and RStudio installed on your computer, update them if you do not have the latest versions. You can use the general instructions for how to update here (just note to use the latest versions of the programs and packages rather than the version listed here) - **[I have R Installed](https://jennhuck.github.io/workshops/install_update_R.html#%E2%80%9Ci_have_r_installed%E2%80%9D)**


## Clone this repository from GitHub

(note: it might be helpful to open a duplicate window of this page next to this one or on a separate device so you can more easily read and follow the instructions while you complete these steps)

1. First, click on the green "Code" button in the upper right of this page. 
2. Click on the clipboard icon next to the URL under "Clone with HTTPS" to copy the location of this GitHub repository.
3. Open RStudio, and select "File" --> "New Project" --> "Version Control" --> "Git" and paste the URL you copied above in the "Repository URL:"   (to paste, use ctrl+V (Windows) or cmd+V (Mac) or right-click and select paste).  Leave the default Project directory name as "introR4bio." Feel free to Browse to find a good location for this project folder to be created.
4. Click "Create Project" and then all the files you need will download into a folder called "introR4bio"

## Install Swirl and Intro to R for Biology Course

1. The first time you use swirl, you will have to install the package. You will only need to do this once. It is similar to downloading an app to your phone or computer. To install swirl, type this code into the RStudio console and press Enter:

`install.packages("swirl")`


