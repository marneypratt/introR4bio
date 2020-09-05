# Intro to R for Biology

### by Marney Pratt

### Last updated on August 29, 2020

This webpage details how to download and install the **Intro to R for Biology** Swirl course. Please visit the [Swirl website](https://swirlstats.com/) for more information about how to install or develop interactive Swirl lessons.<br>

Please feel free to download and use the **Intro to R for Biology** Swirl course for educational purposes, no commercial uses are allowed.

(note: it might be helpful to open a duplicate window of this page next to this one or on a separate device so you can more easily read and follow the instructions while you complete these steps)

If you already have R and RStudio installed and you just want to install the **Intro to R for Biology** Swirl course, you can follow simpler instructions here: [Intro to R for Biology Swirl Course](https://github.com/marneypratt/Intro_to_R_for_Biology)

## Install/Update R and RStudio

To use the interactive **Intro to R for Biology** Swirl course you need access to R and RStudio. Check with your instructor to see if you will be using a cloud-based version of RStudio (RStudio Server, RStudio Cloud). Even if you will be using a cloud-based version, it is good to have a backup of the software on your computer. If you need or want to install R and RStudio on your computer, you can follow these instructions - [Installing R and RStudio](https://moderndive.com/1-getting-started.html#installing)

If you already have R and RStudio installed on your computer, then please update them if you do not have the latest versions. You can use the general instructions for how to update here (just note to use the latest versions of the programs and packages rather than the version listed here) - [I have R Installed](https://jennhuck.github.io/workshops/install_update_R.html#%E2%80%9Ci_have_r_installed%E2%80%9D)


## Clone/copy this repository from GitHub

This series of instructions will copy all the files you need from here on GitHub to your computer or cloud-based RStudio. 

For **Option 1 (if you have Git): Clone this repository from GitHub**, you must have Git installed and setup to work with RStudio for this to work. If you are working on RStudio Cloud or an RStudio Server then Git is already set up for you and you can follow the **Option 1** instructions

If you don't have Git installed and you are using a local desktop version of R and RStudio, you can follow these instructions to install and setup Git on your computer (note that this is rather involved, but you only have to do it once): [Happy Git and GitHub for the useR](https://happygitwithr.com/index.html)

Alternatively, you can skip this section and go to **Option 2: Download this repository from GitHub using the usethis package** below


### Option 1 (if you have Git): Clone this repository from GitHub

1. First, click on the green "Code" button in the upper right of this page. 

2. Click on the clipboard icon next to the URL under "Clone with HTTPS" to copy the location of this GitHub repository.

3. Open RStudio, and select 

"File" --> "New Project" --> "Version Control" --> "Git" and paste the URL you copied above in the "Repository URL:"   
(to paste, use ctrl+V (Windows) or cmd+V (Mac) or right-click and select paste)

Leave the default Project directory name as "introR4bio." Feel free to Browse to find a good location for this project folder to be created.

4. Click "Create Project" and then all the files you need will download into a folder called "introR4bio"

### Option 2: Download this repository from GitHub using the usethis package

1. In RStudio, install the usethis package by typing this code into the RStudio console and press Enter:

`install.packages("usethis")`

2. Once the package is installed, then you need to load usethis. This is similar to opening an app on your phone or computer. To load usethis, type this code into the RStudio console and press Enter:

`library(usethis)`

3. To download the repository, use this code:

`use_course("https://github.com/marneypratt/introR4bio/archive/master.zip")`

4. When told "Downloading into..." "OK to proceed?" select the number for the option next to "I agree" and note what directory it is putting the zipped file into. (Note that you can move the files later if needed)

5. When asked "Shall we delete the ZIP file" select the number for the option that says "Definitely"

A new session of RStudio will open with the unzipped folder containing all the files you need ready for you.


## Install Swirl and Intro to R for Biology Course

Once you have all the files from the **Intro to R for Biology** repository into RStudio, then you are ready to install swirl and the **Intro to R for Biology** swirl course.

1. The first time you use swirl, you will have to install the package. You will only need to do this once. It is similar to downloading an app to your phone or computer. To install swirl, type this code into the RStudio console and press Enter:

`install.packages("swirl")`

Be patient, it sometimes takes a little while for the package to download and install.  (You will need an internet connection to download packages)

Note that there may be other packages you might need to install. For example, when I recently installed swirl, I had to also install the RCurl package to get swirl to load properly. It is also a good idea to make sure you have the most up to date version of the tidyverse, ggfortify, car, and carData packages since we will use these in the Intro to R for Biology Swirl lessons. To install additional packages, use the `install.packages()` function (make sure to put the package name in quotes within the parentheses). For example, to install the RCurl, tidyverse, ggfortify, car, and carData packages use the following code:

```
install.packages("RCurl")
install.packages("tidyverse")
install.packages("ggfortify")
install.packages("car")
install.packages("carData")
```

2. Once the swirl package is installed (along with any other packages you might need), then you need to load swirl. This is similar to opening an app on your phone or computer. You will need to load the swirl package anytime you start a new session of R in RStudio. To load swirl, type this code into the RStudio console and press Enter:

`library(swirl)`

3. After swirl loads, you will need to install the **Intro to R for Biology** Swirl course by typing the following code into the console and pressing Enter:

`install_course()`

When prompted, select the file called "Intro_to_R_for_Biology.swc"

This is a compressed folder full of files in a special file format, .swc, unique to swirl. When you use the `install_course()` function to install this course, it will unpack this file and load the course for you.


4. Next, type this code into the RStudio console and press Enter:

`swirl()`

5. Swirl will ask you to give a name (it will use this to remember you from session to session, nothing is shared publicly) and then it will give a few other prompts to help you learn how swirl works.  Follow the instructions until you get to a prompt that asks you to "Please choose a course, or type 0 to exit swirl." At this prompt, select the option next to "Intro to R for Biology".

6. Once you are in the course, you will see several lessons. Start with "1: Basics" or choose the lesson your instructor has told you to choose.

If you need help while going through a swirl lesson, you can click on the "swirl-commands.txt" or "swirl-tips.txt" files in the IntroR4bio folder

You can also open the [Resources for the Intro to R for Biology course webpage](https://docs.google.com/document/d/e/2PACX-1vTRMYrJYm4DtGURF6voY0AwhFFGnIvjYleoC5qgH5uVzRmCNXO9EJuKLK5ihvH3rMvWtnuPZ_7qU13i/pub) and keep that open while you work through the lessons.


## Intro to R for Biology Swirl Course

Here is a list of the lessons available in the course

1. Basics
2. Getting_Data_into_R
3. Working_with_Data
4. Descriptive_Statistics
5. Graphing_with_ggplot
6. Graphing_Grouped_Continuous_Data
7. Comparing_2_Groups
8. Linear_Regression
9. Linear_Regression_with_a_Transformation

Note that this course uses the [Tidyverse](https://www.tidyverse.org/) especially the readr, dplyr, and ggplot2 packages as well as ggfortify (an extension for ggplot2).

A few lessons use the car and carData packages from [An R Companion to Applied Regression by John Fox and Sanford Weissberg](https://socialsciences.mcmaster.ca/jfox/Books/Companion/index.html)

## Enjoy Learning how to Use R!





