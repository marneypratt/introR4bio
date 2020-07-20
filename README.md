# Intro to R for Biology

### by Marney Pratt

This webpage details how to download and install the **Intro to R for Biology** Swirl course. Please visit the [Swirl website](https://swirlstats.com/) for more information about how to install or develop interactive Swirl lessons.<br>

Please feel free to download and use the **Intro to R for Biology** Swirl course for educational purposes, no commercial uses are allowed.

## Install/Update R and RStudio

The directions below assume you have access to R and RStudio. Check with your instructor to see if you will be using a cloud-based version of RStudio. Even if you will be using a cloud-based version, it is good to have a backup of the software on your computer. If you need or want to install R and RStudio on your computer, you can follow these instructions - [Installing R and RStudio](https://moderndive.com/1-getting-started.html#installing)

If you already have R and RStudio installed on your computer, then please update them if you do not have the latest versions. You can use the general instructions for how to update here (just note to use the latest versions of the programs and packages rather than the version listed here) - [I have R Installed](https://jennhuck.github.io/workshops/install_update_R.html#%E2%80%9Ci_have_r_installed%E2%80%9D)


## Clone this repository from GitHub

(note: it might be helpful to open a duplicate window of this page next to this one or on a separate device so you can more easily read and follow the instructions while you complete these steps)

This series of instructions will copy all the files you need from here on GitHub to your computer or cloud-based RStudio

1. First, click on the green "Code" button in the upper right of this page. 

2. Click on the clipboard icon next to the URL under "Clone with HTTPS" to copy the location of this GitHub repository.

3. Open RStudio, and select 

"File" --> "New Project" --> "Version Control" --> "Git" and paste the URL you copied above in the "Repository URL:"   
(to paste, use ctrl+V (Windows) or cmd+V (Mac) or right-click and select paste)

Leave the default Project directory name as "introR4bio." Feel free to Browse to find a good location for this project folder to be created.

4. Click "Create Project" and then all the files you need will download into a folder called "introR4bio"

## Install Swirl and Intro to R for Biology Course

1. The first time you use swirl, you will have to install the package. You will only need to do this once. It is similar to downloading an app to your phone or computer. To install swirl, type this code into the RStudio console and press Enter:

`install.packages("swirl","RCurl")`

Be patient, it sometimes takes a little while for the package to download and install.

2. Once the swirl package is installed, then you need to load it. This is similar to opening an app on your phone or computer. You will need to load the swirl package anytime you start a new session of R in RStudio. To load swirl, type this code into the RStudio console and press Enter:

`library(swirl)`

3. After swirl loads, you will need to install the **Intro to R for Biology** Swirl course by typing the following code into the console and pressing Enter:

`install_course()`

When prompted, select the file called "Intro_to_R_for_Biology.swc"

This is a compressed folder full of files in a special file format, .swc, unique to swirl. When you use the `install_course()` function to install this course, it will unpack and load the course for you.


4. Next, type this code into the RStudio console and press Enter:

`swirl()`

5. Swirl will ask you to give a name (it will use this to remember you from session to session, nothing is shared publicly) and then it will give a few other prompts to help you learn how swirl works.  Follow the instructions until you get to a prompt that asks you to "Please choose a course, or type 0 to exit swirl." At this prompt, select the option next to "Intro to R for Biology".

6. Once you are in the course, you will see several lessons. Start with "1: Basics" or choose the lesson your instructor has told you to choose.

If you need help while going through a swirl lesson, you can click on the "swirl-commands.txt" or "swirl-tips.txt" files in the IntroR4bio folder

You can also open the [Resources for the Intro to R for Biology course webpage](https://docs.google.com/document/d/e/2PACX-1vTRMYrJYm4DtGURF6voY0AwhFFGnIvjYleoC5qgH5uVzRmCNXO9EJuKLK5ihvH3rMvWtnuPZ_7qU13i/pub) and keep that open while you work through the lessons.



## Enjoy Learning how to Use R!





