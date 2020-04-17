# jsPsych Online Experiments

This is the repository created by Bradley C. Smith (BCS) to document one method of running an online experiment like this one: https://smithbradleyc.github.io/jsPsych_Online_Experiments/. This method uses jsPsych (a JavaScript library for running behavioural experiments in a web browser) to create the experiment, GitHub Pages to host the experiment, and a real-time Firebase database to collect participant's responses. All of these services can be used completely free (as of April 2020). Anything written by someone other than BCS will be clearly tagged to that person with either a hyperlink to that person's GitHub account or with one of the tags below:
- [Matt Cook](https://github.com/cookm346): #MC
- [Jackie Spear](https://github.com/jackiespear): #JS
- [Matt Crump](https://github.com/CrumpLab): #MJC

Below you will find a [step-by-step explanation](#step-by-step-guide) of how you can host your own experiment. It will not describe how to program your own experiment except as it pertains to collecting data (and granted credit through the [SONA system](https://www.sona-systems.com/default.aspx)) but all of the examples will use the jsPsych JavaScript library. In theory, you should be able to switch this library out for your personal favourite and this guide should still work for you; but I have not tested this.

## Where is this coming from?

I wrote this (April 2020) as a PhD student in Psychology at the University of Manitoba working in [The Cognitive Science Laboratory](https://umcognitivesciencelaboratory.weebly.com/).

At that time, I programmed an experiment for the class "Open and Collaborative Science" taught by [Dr. Melanie Soderstrom](https://home.cc.umanitoba.ca/~soderstr/) ([GitHub](https://github.com/melsod)). That experiment can be found on the [Open Science Framework](https://osf.io/2a6b4/) ([GitHub Repo](https://github.com/melsod/OCSWinter2020)). That project's GitHub repository includes a step-by-step guide for reproducing the experiment that will look a lot like the one included here. That's because I wrote that one and then adapted it here to be a somewhat more generalizable.

## The Goal

The goal of this repository is to document the method I used (and plan to continue using for the forseeable future) to run online experiments. I hope to offer this explanation at a level so that even a novice GitHub user and/or novice programmer could run their own experiment (unfortunately I must leave creating the actual experiment for another tutorial). It is also a way to promote open science because this method facilitates open and collaborative science practices (using GitHub pages requires that the repository is made public).

I'm indebted to the creators of the [jsPysch Library](https://www.jspsych.org/) and countless others have posted thier experiments using the jsPsych library online. In particular, I used code from [The Experiment Factory](https://www.expfactory.org/) ([GitHub Pages](https://expfactory.github.io/)), and [Matt Crump](https://crumplab.github.io/)'s [jspsychrexamples](https://github.com/CrumpLab/jspsychrexamples) to help me learn how to structure and run my own jsPsych experiments. Thanks are also due to [Danielle Navarro](https://djnavarro.net/)'s [xprmntr package](https://github.com/djnavarro/xprmntr) and [Matt Crump](https://crumplab.github.io/)'s [vertical package](https://github.com/CrumpLab/vertical). Although I didn't end up using either of these packages, they greatly informed the method I describe here (in fact, the instructions for using Google's Firebase is almost directly lifted from [Crump's FirebaseDemo](https://crumplab.github.io/jspsychrexamples/FirebaseDemo/Instructions_FirebaseDemo.html))

# Getting Started

First, I'll give a conceptual overview of what this guide will cover in the [Overall Summary](overall-summary) section. Then, I'll give a detailed explanation of how to host your own experiments online in the [Step-by-Step Guide](#step-by-step-guide).

## Overall Summary

The [Step-by-Step Guide](#step-by-step-guide) will walk you through:
- [Downloading important software](#download-important-software):
  - [Download R](#download-r)
  - [Download rStudio](#download-rstudio)
  - Other potentially useful [code editors](#other-potentially-useful-code-editors)
- [Copying this example experiment](#copying-this-example-experiment):
  - [Creating your own GitHub account](#sign-up-for-a-github-account)
  - [Getting/forking your own copy of the repository](#fork-the-repository)
  - [Downloading the software used to easily transfer data between GitHub and a local machine (GitHub Desktop)](#download-github-desktop)
  - [Making a local copy of the repository](#clone-the-repository)
- Running this example experiment:
  - General editing/testing of the experiment
  - Saving your edits to GitHub
  - Hosting the experiment
  - Collecting data remotely
  - Automatically granting SONA credits
  - Saving and unpacking FireBase data
- General Tips:
  - Tips for testing code/debugging 
  - Tips for data analysis
  - Tips for experimental structure
  - Tips for repository structure
  - Tips for naming conventions

Keep in mind that there are many methods to acomplish any one of these steps and I have only described one. Just because you do it differently does not make it wrong, as long as it works.

Dependencies/things needed to for any step to work (packages/libraries/etc) will be described in the first section that they are important for. So, although I encourage you to skip to the sections relevant to you, if you skip a section it may include dependencies required for future steps. If it seems like you are missing something to get your experiment working I suggest backing up to make sure you have all of the software needed. In the future I may spend the time to include dependencies in all steps they are required for.

## Examples

Here are several examples of experiments hosted on GitHub. These experiment's are officially "dead" meaning that you are free to test out the experiment without causing problems for the researchers hosting these experiments. Those that I know have used Firebase to save data are flagged with #FIREBASE. The host account of each example will be tagged:
- [Contingency Practice Phase](https://smithbradleyc.github.io/jsPsych_Online_Experiments/) #BCS #FIREBASE
- [What can we percieve in infant vocalizations?](https://melsod.github.io/OCSWinter2020/)(Hosted by [melsod](https://github.com/melsod) written by #BCS) #FIREBASE
- Matt Crump's [jsPsychrExamples](https://github.com/CrumpLab/jspsychrexamples) #MJC
  - [Flanker Demo](https://crumplab.github.io/jspsychrexamples/Flanker/experiment/index.html) #MJC
  - [Stroop Demo](https://crumplab.github.io/jspsychrexamples/Stroop/experiment/index.html) #MJC
  - [Stroop Demo (multiple responses)](https://crumplab.github.io/jspsychrexamples/Stroop_multiple_response/experiment/index.html) #MJC
  - [Recognition Memory](https://crumplab.github.io/jspsychrexamples/RecognitionMemory/experiment/index.html) #MJC
  - [Stroop Demo with Firebase Demo](https://crumplab.github.io/jspsychrexamples/FirebaseDemo/experiment/index.html) #MJC #FIREBASE
- Jackie's Distinctiveness Experiment
- MORE EXAMPLES **#HELP HERE**

## Step-by-Step Guide

### Download Important Software:

If you already have R and rStudio then skip to [Other Code Editors](#other-potentially-useful-code-editors). If not then follow the instructions below. My goal is to make all of the instructions so that you can follow them with no-exposure/minimal-exposure to R or programming in general. However, if you want to learn programming in R (and you should) I can recommend a couple free resources to get you going:
- [The Pirate's Guide to R](https://bookdown.org/ndphillips/YaRrr/) (Yes ... seriously, it is a good resource)
- [Programming for Psychologists](https://crumplab.github.io/programmingforpsych/programming-in-r.html) #MJC

#### Download R:

- Go to https://www.r-project.org/
- In the first paragraph click [download R](https://cran.r-project.org/mirrors.html)
- Choose a CRAN mirror geographically close to you (For Manitoba choose [Manitoba Unix user Group](https://muug.ca/mirror/cran/))
- Click on the Download link near the top of the page for your operating system
  - Windows: 
    - Click on the link to "install R for the first time"
    - Click on "Download R ... for Windows"
    - Once the file is downloaded, open it and go through the installation process
  - Mac:
    - **#HELP HERE**
  - Linux:
    - **#HELP HERE**
  
- **You will not need or want to open this base program instead proceed to Downloading rStudio**

#### Download rStudio:
- Go to https://rstudio.com/
- Near the top right hand side of the page, click [download](https://rstudio.com/products/rstudio/download/)
- Under the RStudio Desktop *Open Source License* option, click "Download"
- Download the appropriate software for your operating system. Normally the website will recognize the appropriate choice and offer it under "Recommended for your system:"
- Once the file is downloaded, open it and go through the installation process

- Opening rStudio gives you access the R programming language, but in a nicer format than just opening the basic R program
- However, if you are just following through this Step-by-Step then you will not need to open rStudio yet.

#### Other Potentially Useful Code Editors:

Personally, I use rStudio as a code editor for R, HTML, rMarkdown (including Latex and/or HTML), Javascript, Python, and even a little bit of C++. It is generally accepted as the best editor for R, but nothing else. So none of these extra code editors are needed for editing/coding your experiments or getting them online. However, some people will find them useful as code editors that are "better" than rStudio:

- [Visual Studio](https://code.visualstudio.com/)
- [NetBeans](https://netbeans.org/)
- **#HELP HERE**


## Copying This Example Experiment:

The easiest way copy this experiment is to fork this repository into your own GitHub account, and then clone it (so that it is saved locally on your machine). If you understand these instructions then you can skip to the section [Running This Example Experiment](#running-this-example-experiment), otherwise we'll explain how to do that:

#### Sign-Up For a GitHub Account

If you already have a GitHub Account then skip to [Fork the Repository](#fork-the-repository), otherwise:

- Go to www.github.com
- Click the "Sign Up" button in the top right hand side of the site (or click [here](https://github.com/join?source=header-home))
- Create a Username and provide the requested information
- Click "Select a Plan"
- Click "Choose Free" unless you have a reason to get the paid service
- Provide whatever level of information you want to GitHub and then scroll down and click "Complete setup"
- Verify your email address
- There is no need to "Create a new repository" if you do not want to

#### Fork the Repository

- Go to https://github.com/SmithBradleyC/jsPsych_Online_Experiments (but you're already here)
- Click on the "Fork" button near the top, right hand side of the page
- Wait for the repository to complete it's fork
- You now own your very own copy of this repository!

#### Download GitHub Desktop

If you already have the GitHub Desktop Client then skip to [Clone the Repository](clone-the-repository)

- Go to https://desktop.github.com/ and download the application
- Install the application
- Open application that you just installed
- Sign in with your GitHub account
- (Optional) you can learn about Git and GitHub with [this tutorial](https://help.github.com/en/desktop/getting-started-with-github-desktop/creating-your-first-repository-using-github-desktop)

- You can also avoid using the GitHub Desktop client by using the Git command line functions by downloading the program here https://git-scm.com/downloads, I will leave it up to you and Google to work through how to do it that way. It is too difficult to explain in this tutorial.

#### Clone the Repository

- Make a folder on your computer where you would like to save the repository
- In the GitHub Desktop program, click on the File menu (in the top, left hand corner)
- Click on Clone Repository
- Select the "GitHub.com" tab if it is not already selected
- Your repositories should be visible, assuming that you successfully signed into GitHub on the Desktop Client
- Select the YourGitHubUsername/jsPsych_Online_Experiments option
- Choose the local path where you want to save the repository (just below the repository options)
- Click the "Clone" button
- This saves a local copy of the repository on your device

### Running This Example Experiment

Now that you have a local copy of the example experiment on your machine you can begin to make and save your own edits. When you save the edits they will only be saved on your local machine until you [push them back to GitHub](#saving-edits-to-github). You can use [any code editing software](#other-potentially-useful-code-editors) that you like, even Notepad, but I'll be describing how I use rStudio. This helps keep the experiment/repository tidy.

#### Editing/Testing the Experiment

The best way to keep organized in rStudio is to use R Projects. When you create an R Project in rStudio it creates a folder with the project name and every new file that you create and save within that rStudio session will be saved to the folder. The R Project also creates a .Rproj file. This is the core of the R Project. It will save data between sessions and is the pointer for your "working directory" (meaning that calls to other files will be in reference to the .Rproj file). For more information on R Projects see [here](https://support.rstudio.com/hc/en-us/articles/200526207-Using-Projects) or one of the R resources I pointed out in the [Download Important Software](#download-important-software) section. **Many of the functions/files I have in my example repository rely on being run inside an R Project.**

- Open the local repository folder (there should be a button in the middle of the screen in the GitHub Desktop application)
- Open *jsPsych_Online_Experiments.Rproj* with rStudio
- You will/may have 4 sections/quadrants to your screen:
  - Top left: file open in rStudio (this may not open your first time meaning the console will take up the whole left side)
  - Top right: the **Environment**/History/Connections tabs (Environment shows what data you have loaded, should be blank for now)
  - Bottom left: the **Console**/Terminal/Jobs tabs (console is the most important)
  - Bottom right: the **Files**/Plots/Package/Help/Viewer tabs (open the files tab)
- In the Files tab, you should see a list from .gitattributes to a folder called stimuli (if you're organizing alphebetically)
- These are all of the files/folders in the repository. Here's a quick explanation for all of them:
  - *.gitattributes*: does some work for your git repository. Probably not needed for this repository but don't edit unless you know what you're doing
  - *.gitignore*: does some work for your git repository. This specifies files/folders that your repository should ignore. These files are made by rStudio and I didn't need/want them backed up to GitHub
  - *.Rhistory*: this file tracks what you do in rStudio. It is also ignored by Git because that file type is included in .gitignore
  - *data*: this is the folder where data is saved by default when you pull it from FireBase
    - *data.csv*: this is the .csv version the the datafile pulled from FireBase. It is created by R/analysis/pull_firedata.R
    - *data.json*: this is the raw data file for 2 'participants' in the experiment. It is the file pulled straight from FireBase. Unless you rename this file it will be overwritten when you pull data from FireBase (R/analysis/pull_firedata.R)
    - *summarized_data.csv*: this is a .csv with data summarized to a percent correct for each participant (and with extracted survey data)
  - *forms*: this is where I store the HTML code for the consent and debriefing forms
    - *consent.html*: the code for the consent form. It is called by the index.html file
    - *no_consent_deb.html*: this is the debreifing form for those who decline to participate in the experiment. It is called by the index.html file
  - *img*: this is where I expect images that are important to the experiment would be saved
    - *UM_Logo.png*: this is the University of Manitoba Logo. It is called by the consent and debreifing forms
  - *index.html*: this is the main part of the experiment. It will be explained in greater detail
  - *jspsych-6-2*: this is the jsPsych Library
    - *css*: the folder containing the default jspsych .css file
    - *examples*: the folder containing examples of all the default jsPsych plugins. Open any of them in a web browser to see how it works, or open them in rStudio/code editor to see how they are programmed. Good for learning how to program your own experiments
    - *jspsych.js*: the main file for the jsPsych library. Needs to be called in index.html
    - *license.txt*: the license relevant to the jsPsych library
    - *plugins*: the folder containing the jsPsych library plugins. Examples of how to use these are in the examples folder. These files will need to be called by the index.html file if you want to use those plugins
  - *jsPsych_Online_Experiments.Rproj*: the R project file to keep everything organized
  - *R*: the folder containing all of my R code
    - *analysis*: the folder containing all of the code used in analyzing the data
      - *data_analysis.R*: the file where the data analysis is done. The example summarizes the data and saves the summarized data #MC
      - *figures*: the folder where I save my figures (empty in this repository)
      - *pull_firedata.R*: the file used to download the data from FireBase and save a .csv version of the data
    - *pre_experiment*: the folder containing all the R code used in setting up the experiment
      - *create_stimuli.R*: the file used to create all of the stimuli used in the example experiment
      - *functions_to_create_stimuli.R*: a file containing the functions used in create_stimuli.R
  - *README.md*: the file that GitHub uses to create the ReadMe (the document you are currently reading)
  - *stimuli*: the folder containing all of the experimental stimuli
    - *exp_text.js*: a javascript file that sets up all of the text that will be presented by the experiment. This file is called by the index.html file
    - *practice_stimuli.js*: a javascript file that defines the stimuli used in the example experiment. This file is created by create_stimuli.R and called by index.html


# MORE HERE

# GONE UP TO HERE SO FAR

#### Saving Edits to GitHub

To save them to GitHub you will first need to commit the changes to your local git repository (automatically created when you cloned the repository). You can do this through the GitHub Desktop Client. When you commit to your local git repository it is a form of version control (essentially it keeps a record of all the changes you make and allows you to revert to a previous iteration of the experiment if you want). Once you have committed changes to your local repository you can then push those changes to your GitHub repository (think of "pushing" as saving your edits to the "cloud"). Once changes are on your GitHub repository, others can see your work and contribute to it. You can also host the experiment there (using GitHub Pages, this will be explained  in [Hosting the Experiment](#hosting-the-experiment)).

We'll leave it to you to learn how to push changes to your GitHub repository and work collaboratively with others from there (it's much the same way you are "working" on our experiment) but we will show you how to host the experiment in the section [Running the Experiment](#running-the-experiment).


#### Reproduce the Experiment

- In your local repository (the folder that you downloaded/cloned the repo to), open OCSWinter2020.Rproj with rStudio. This will open rStudio project for the experiment. What that means is that it sets a working directory so that any file calls will be in reference to this file. If you work on a different task (other than related to this experiment) then you should create a new R project by using the drop down menu in the top right hand of the rStudio window.
- Then in the bottom right panel of the rStudio screen select the files tab
- Select the [index.html](index.html) file, and "Open in Editor"
- This is the experiment file. It is written in JavaScript and HTML using the jsPsych library (found in the jspsych-6-2 folder in the repository). Hopefully it is documented well enough for you to follow. We'll leave it to you to learn jsPsych if you want to adapt the experiment for your own purposes.
- If you open the [index.html](index.html) file in your web browser or with the rStudio Preview button it should open. Unfortunately, due to permissions settings you will probably be unable to run through the experiment on your web browser, and some features of the experiment may not work in the rStudio preview. There are ways around these problems to test the experiment (commenting out lines of code tagged with "#TESTING" in the [index.html](index.html) file) but it will all work when hosted online
- Audio for the experiment is found in the [audio folder](audio) of the repository
- Consent and Debriefing forms, written in HTML code, is found in the [forms folder](forms)
- Images for the experiment are found in the [img folder](img)
- Almost all of the text that appears in the experiment is found in the [stimuli folder](stimuli) in the [exp_text.js file](stimuli/exp_text.js)
- The original sample of audio clips were selected using the [R/pre_experiment/sample_clips_2.r](R/pre_experiment/sample_clips_2.r) file but we suggest using [R/pre_experiment/sample_clips.r](R/pre_experiment/sample_clips.r) because it has been adapted to work better with the repositories organizational structure (this may mean a different original sample but have not tested it)
- After being manually screened by 3 of the contributors (the files they decided to exclude can be found at [audio/Exclusion_files](audio/Exclusion_files) and [R/pre_experiment/files_to_exclude.RData](R/pre_experiment/files_to_exclude.RData)) the final selection of clips was done using the [R/pre_experiment/narrow_sample.R](R/pre_experiment/narrow_sample.R) file
- The stimuli that are presented to the participants were also created with the [R/pre_experiment/narrow_sample.R](R/pre_experiment/narrow_sample.R) file and are found in [stimuli/age_language_test_stimuli.js](stimuli/age_language_test_stimuli.js) and [stimuli/sex_test_stimuli.js](stimuli/sex_test_stimuli.js)

#### Reproduce the Results

Our results should be reproduced by compiling/knitting the [data_analysis](R/analysis/data_analysis.Rmd) file and then by running the analyses found in the [followup_analysis](R/analysis/followup_analysis.R) file. For completeness, here is a description of the files relevant to our results:

- All data collected were temporarily stored on a Google Firebase server
- They were then downloaded using the [R/analysis/pull_firedata.R](R/analysis/pull_firedata.R) file
- The downloaded data is stored in the [data](data) folder
- Files in the [data](data) folder:
  - [short_exp_test_data](data/short_exp_test_data.json): Data from contributors while proofing the experimental procedure. Only includes 1 trial in each block. Used to quickly test the experiment for obvious errors and remote database collection.
  - [private_pilot_test_data](data/private_pilot_test_data.json): Data from contributors for testing a more finalized version of the task. Used to test whether we were collecting all the relevant data for our analysis
  - [3_participant_pilot_data](data/3_participant_pilot_data.json) and [2_additional_part_pilot_data](data/2_additional_part_pilot_data.json): Data from a pilot test of 6 "real" participants (3 at a time). Data was used to confirm that automatic crediting for the online system worked. Only includes 5 data points because 1 participants declined to participate at the consent phase. Data is not included in the final sample.
  - [final_data](data/final_data.json): The final data collected from 626 participants. File size is 105.5 MB so it uses [Git LFS](https://git-lfs.github.com/) in order to be uploaded to GitHub. It should work with the process described but may cause problems (we have very little experience with Git LFS). In any case, [final_data](data/final_data.json) has already been processed into the following files:
    - [summarized_data](data/summarized_data.csv): A .csv file containing a single line for all 626 participants summarizing their performance and survey responses.
    - [w_exclusions](data/w_exclusions.csv): A .csv file containing a single line for all 460 participants who were not excluded, summarizing their performance and survey responses.
    - [trial_data](data/trial_data.csv): A .csv file containing a single line per trial for all 626 participants. Each line contains the participant's survey responses
    - [w_exclusions_trial_data](data/w_exclusions_trial_data.csv): A .csv file containing a single line per trial for all 460 participants who were not excluded. Each line contains the participant's survey responses
- Files in the [R/analysis](R/analysis) folder:
  - [pull_firedata](R/analysis/pull_firedata.R): An .R file that pulls all data saved in the Firedata database and saves it in the [data](data) folder in a file called "data.json"
  - [data_cleaning](R/analysis/data_cleaning.R): An .R file that reads in the final_data.json file, tidies the data, and summarizes individual participant's results. Saves csv files of the summarized data with and without exclusion criteria
  - [data_analysis](R/analysis/data_analysis.Rmd): An .Rmd file (markdown) that reads in the csv produced by [data_cleaning](R/analysis/data_cleaning.R). When compiled/knitted, the resulting html document provides an informal explanation of the data, exclusions, and main analysis
  - [followup_analysis](R/analysis/followup_analysis.R): An .R file that reads in the trial data and computes the results of our follow-up analyses

### Running the Experiment

Simply by forking the original repository of this experiment you should be set up to run the experiment with minimal changes. We have broken this process into three steps:

#### Hosting the Experiment

With your forked copy of the repository it should be a simple matter of turning on GitHub pages in order to host our version of the experiment. To do so do the following:
- Navigate to your repository (github.com/YourYourGitHubUsername/OCSWinter2020)
- Click on the "Settings" tab near the top of the screen (github.com/YourGitHubUsername/OCSWinter2020/settings)
- Ensure your repository is public (select the "Manage access" tab on the left)
- Return to the "Settings" page
- Scroll down to the GitHub Pages section of the page
- Enable GitHub Pages by changing the source to the master branch
- You do not need to select a theme
- In a few minutes the pages site should be published. The URL will appear at the top of the GitHub Pages section (https://<i></i>YourGitHubUsername.github.io/OCSWinter2020)
- Going to this URL will begin the experiment as it is hosted on your GitHub repository
- Any changes to files in your GitHub repository will affect the experiment, but it may take a few minutes for those changes to be reflected on the Pages URL (it is not instantaneous)

#### Collecting the Data

Unfortunately GitHub pages is only for static websites so we can't directly save the data on your repository. Instead we will save the data to Google's Firebase servers. We will explain how to do this with this particular experiment but we learned this process from the instructions found on [Matt Crump's FirebaseDemo](https://crumplab.github.io/jspsychrexamples/FirebaseDemo/Instructions_FirebaseDemo.html) repository.
- Create an account with firebase https://firebase.google.com/ (free unless you need lots of data or other options). You may not want this associated with your "personal" google account.
- Create a new project:
  - Go to Console (top, right hand side of the screen)
  - "Create a project"
  - Give the project a name (probably the same as your GitHub Repo)
  - I disabled Google Analytics but I suspect it doesn't make a difference
  - Wait for your project to be ready
- Click on the Develop tab on the left hand side of the screen, then select "Database"
- Scroll down to find the Realtime Database and create that type of database
- Choose "Start in test mode" and "Enable". This will enable you to read and write to the database. It will also allow anyone else with credentials to read and write to the database. These credentials will be publicly posted on your GitHub repo so there is a security concern if you are saving any private data. These security settings can be changed later (under the "Rules" tab).
- Now you have a live database. You just need the configuration codes to interact with the database.
- Click on the gear symbol next to "Project Overview"
- Select "Project settings"
- In the first tab, "General", you will need to register an app. Add a web app (symbol looks like this </>).
- You do not need to turn on hosting unless you decide to host your experiment here instead of GitHub Pages.
- Give the app a nickname and click "Register app"
- Firebase will give you some html code that will look something like this:
<pre class="js"><code>var firebaseConfig = {
    apiKey: &quot; stuff here&quot;,
    authDomain: &quot;stuff here &quot;,
    databaseURL: &quot;stuff here &quot;,
    projectId: &quot;stuff here &quot;,
    storageBucket: &quot;&quot;,
    messagingSenderId: &quot;stuff here &quot;,
    appId: &quot;stuff here &quot;
</code></pre>
- Copy this portion of the code, go to the [index.html](index.html) file in your local repository, scroll down until you find similar code (about line 70), and replace our Firebase configuration with yours.
- You may notice that we have included three lines of source code (e.g., <script src="https://<i></i>www<i></i>.gstatic.com/firebasejs/6.3.4/firebase-app.js"></script>) rather than Firebase's one in the code that they provide you. All three of these are needed for our procedure. Do not delete or overwrite them. You may update the version number (e.g., from 6.3.4 to 7.13.2) but this is probably not needed.
- Now go back to your Browser and "Continue to console" (Go back to "Project settings")
- In the left hand menu, under Develop, select "Authentication"
- Select "Sign-in method" or "Set up sign-in method"
- Select "Anonymous" and change the settings so that it is enabled and save

- Your database is now fully set up and ready to accept anonymous data. However, to remotely pull off the data we will need to find your "secret key"
  - Go back to your "Project settings"
  - Go to the "Service accounts" tabs
  - Click on "Database secrets"
  - Under your projects database, click to show the secret key. Copy and paste this somewhere you can use it later. The only place you'll probably use it is in the [R/analysis/pull_firedata.R](R/analysis/pull_firedata.R) file to pull off the data. You will also need your projectURL (found in the code provided by firebase).

The rest of the references to firebase should be explained well enough in the comments of the [index.html](index.html) file. To more easily find this code I have tagged those lines with "#FIREBASE". Now when someone finishes the experiment their data should be saved to your Firebase realtime database.

#### Crediting SONA Participants

Our university uses the SONA system to credit participants with course credit. SONA allows online experiments and automatic crediting for those experiments. To do this:
- Set up a SONA online experiment
- Go to your SONA experiment's "Change Study Information" page
- Set the SONA Study URL to your experiments URL with "?id=%SURVEY_CODE%" added onto the end of the URL (without the quotation marks). For example, you might set the Study URL to: https://<i></i>YourGitHubUsername.github.io/OCSWinter2020/?id=%SURVEY_CODE%
- Then go back to the Study Information page and find the "Completion URLs:"
- Copy the client-side Completion URL, this will be important to include as a redirect at the end of your study
- There is then some important code to include in the [index.html](index.html) file (including the client-side URL) in order to automatically grant the participants credit. These will be tagged with "#SONA" so that they are easier to find. The most vital one will look something like this:
  - window.location.href = "https://<i></i>umanitobapsych.sona-systems.com/webstudy_credit.aspx?experiment_id=XXXX&credit_token=11X11X111X1X1X1XX1X11111111XX11X&survey_code="+SONA_ID;
  - This code uses the client-side_URL that you have copied from your SONA experiment page, except that you need to replace the end of the client-side_URL (the end looks like this: survey_code=XXXX) with this code: survey_code="+SONA_ID
  - You are replacing the default XXXX at the end of the code with +SONA_ID because SONA_ID is a variable that contains the correct information so that participants can be granted their credit
- So long as you include the code in the [index.html](index.html) tagged with "#SONA", and change the client-side URL to the one provided by your study, then it should automatically grant credit at the completion of the experiment
- You will also need to put the client-side_URL into the debriefing form for those participants who decline to participate during the consent phase of the experiment

# Acknowledgements 

Thank you to Cychosz et al. for providing the BabbleCor dataset (BabbleCor: https://osf.io/rz4tx/). 