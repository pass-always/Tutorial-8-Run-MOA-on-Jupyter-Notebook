# Tutorial 8: Run MOA on Jupyter Notebook

By Ethan Wang, Heitor Muril Gomes, Albert Bifet on November 15, 2021 using MOA 2021.07

## Introduction

The idea of this project is creating a more flexible tool for testing, learning machine learning algorithms by combining the strength of [MOA](https://moa.cms.waikato.ac.nz/blog/) via [moa-flow API](https://github.com/Waikato/moa-flow/blob/master/README.md) with the dynamic and interactive abilities of script languages. You can export a IPYNB file for a task from MOA, then run it interactively on a web-browser with Jupyter Notebook. Jupyter Notebooks nowadays can run the code written in various programming languages by connecting to the corresponding kernels. MOA use Java language, so that we will use a Jupyter kernel for Java called [IJava](https://github.com/SpencerPark/IJava).

This tutorial will show you how to export Jupyter Notebooks from MOA as well as how to configure the Jupyter Notebooks for running the exported tasks. We expect that you have already Python and Jupyter Notebooks installed on your machine. If not, please install them before reading furthermore. This tutorial describes the configuration process on a Windows 10 computer, but it is possibly applied as well for other operating systems without many modifications.

## Disclaimer

- During the development of this tutorial the latest version of MOA was 2021.07.
- We assume you are already familiar with what is MOA and MOA GUI. If that is not the case, you probably should read previous tutorials.
- You may want to fork the repository before cloning it, so that you have your own ‘copy’ of the repository.

## Requirments

- Windows 10
- Intellij IDEA
- Java JDK 9
- Python 3.8 or later
- Git (optional) It is easier to obtain the source code if you use Git. Download and install it from [here](https://git-scm.com/). Optionally, you can ‘git clone‘ the repository and ‘import‘ the project in Intellij IDEA, there are other options like downloading a zip with all the code, but importing it directly is easier.

## moa-flow API

With moa-flow API, you can simplify your work with MOA by using a predesigned workflow API. You can download from [here](https://github.com/Waikato/moa-flow/blob/master/README.md).

---

## Get Started

## Set up Java and Python

In this project, we can only use Java JDK 9, Python 3.8 or later.

**Hint**: JDK, not JRE.

Ensure that Java command must be in the PATH and is using version is 9. For example:

```batch
> java -version
java version "9"
Java(TM) SE Runtime Environment (build 9+181)
Java HotSpot(TM) 64-Bit Server VM (build 9+181, mixed mode)
```

Next ensure that Python command be in the PATH and its version is 3.8 or later. For example:

```batch
> python --version
Python 3.9.0
```

In Windows 10, you can manully add Java to the PATH by command:

```batch
> set PATH=%PATH%;"<absolute path to Java>\bin"
```

Form more information about setting the [PATH system variable](https://www.java.com/en/download/help/path.html).

If the Python scripts folder is not added to the PATH. In Windows 10, you can manually add it to the PATH by command:

```batch
> set PATH=%PATH%;"<absolute path to Python>\Scripts"
```

## Install Jupyter Notebook

Anaconda is a distribution of the Python and R programming languages for scientific computing (data science, machine learning applications, large-scale data processing, predictive analytics, etc.), that aims to simplify package management and deployment.

Anaconda Navigator is a desktop graphical user interface included in Anaconda distribution that allows users to launch applciation and manage conda packages, envirnment and channeds with using command-line commands. There are Free and Paid version you can choose. In this project, free edition is enough, as Individual Edition.
The Jupyter NoteBook is avaiable by default in Navigator.

Download and install [Anaconda](https://www.anaconda.com/).

## Setting up IJava for Jupyter Notebook

If you already installed Anaconda Nvaigator, then run all commands in **Anaconda Prompt** is stead of **Windows console**.  
![Anaconda Prompt](images\anaconda-prompt.png "Anaconda Prompt")

You can download the latest version of IJava from [IJava Github repository](https://github.com/SpencerPark/IJava) and install following the document.

There are two methods to install IJava, **Install pre-built binary** and **Install from source**. We recommand use **Install from source**.

To confirm available kernels for Jupyter Notebooks, run `jupyter kernelspec list` from Anaconda Prompt. For example:

```batch
> jupyter kernelspec list
Available kernels:
  python3    d:\anaconda3\share\jupyter\kernels\python3
  java       C:\ProgramData\jupyter\kernels\java
```

Next, edit the configuration file for Java kernel in the folder
C:\ProgramData\jupyter\kernels\java:

![Jupyter Notebook configuration folder](images\jp-kernelfolder.png "Jupyter Notebook homepage")

Open kernel.json in any text editor and change "java" to the absoute path to where Java is corrently installed on your computer.  
**Hint**: Change "\\" to "/" in the path you copied. "\\" is not the path format used by JSON.  
For example:

```batch
D:/Java/jdk-9.0.4/bin/java.exe
```

![Jupyter Notebook homepage](images\jp-javakernel-config.png "Jupyter Notebook homepage")

Open Anaconda Prompt and type `jupyter notebook` to start it, or click the Juputer Notebook icon. The Jupyter Notebooks will be opened on the web browser:

![Jupyter Notebook icon](images\jp-icon.png "Jupyter Notebook icon")

The Jupyter Notebooks will be opened on the web browser:

![Jupyter Notebook homepage](images\jb-homepage.png "Jupyter Notebook homepage")

Click "New", then choose "Java".

![Jupyter Notebook create new file](images\jp-new-file.png "Jupyter Notebook create new file")

If you can have this that means Jupyter Notebook and IJava are working properly:

![Jupyter Notebook sussess](images\jp-kernel-success.png "Jupyter Notebook create new file")

## Exporting tasks from MOA GUI to a IPYNB files

Currently, there are 6 tasks that can be exported to Jupyter Notebooks files:

**Hint**: You can paste the configurtion to MOA directly.

- EvaluateInterleavedTestThenTrain

```batch
WriteConfigurationToJupyterNotebook -t (EvaluateInterleavedTestThenTrain -l (meta.AdaptiveRandomForest -l (ARFHoeffdingTree -e 2000000 -g 75 -s GiniSplitCriterion -c 0.01 -l MC) -m 80 -x (ADWINChangeDetector -a 0.001) -p (ADWINChangeDetector -a 0.01)) -s (ArffFileStream -f D:\Dataset\Useless\elecNormNew.arff)) -j C:\Users\GGPC\Outputs.ipynb
```

- EvaluatePrequential

```batch
WriteConfigurationToJupyterNotebook -t (EvaluatePrequential -l (meta.AdaptiveRandomForest -l (ARFHoeffdingTree -e 2000000 -g 75 -s GiniSplitCriterion -c 0.01 -l MC) -m 80 -x (ADWINChangeDetector -a 0.001) -p (ADWINChangeDetector -a 0.01)) -s (ArffFileStream -f D:\Dataset\Useless\elecNormNew.arff) -i 100000 -f 4532) -j C:\Users\GGPC\Outputs.ipynb
```

- EvaluatePrequentialCV

```batch
WriteConfigurationToJupyterNotebook -t (EvaluatePrequentialCV -l (meta.AdaptiveRandomForest -l (ARFHoeffdingTree -e 2000000 -g 75 -s GiniSplitCriterion -c 0.01 -l MC) -m 80 -x (ADWINChangeDetector -a 0.001) -p (ADWINChangeDetector -a 0.01)) -s (ArffFileStream -f D:\Dataset\Useless\elecNormNew.arff) -i 100000 -f 4532) -j C:\Users\GGPC\Outputs.ipynb -e
```

- EvaluatePrequentialDelayed

```batch
WriteConfigurationToJupyterNotebook -t (EvaluatePrequentialDelayed -l (meta.AdaptiveRandomForest -l (ARFHoeffdingTree -e 2000000 -g 75 -s GiniSplitCriterion -c 0.01 -l MC) -m 80 -x (ADWINChangeDetector -a 0.001) -p (ADWINChangeDetector -a 0.01)) -s (ArffFileStream -f D:\Dataset\Useless\elecNormNew.arff) -i 100000 -f 4532) -j C:\Users\GGPC\Outputs.ipynb -e
```

- EvaluatePrequentialDelayedCV

```batch
WriteConfigurationToJupyterNotebook -t (EvaluatePrequentialDelayedCV -l (meta.AdaptiveRandomForest -l (ARFHoeffdingTree -e 2000000 -g 75 -s GiniSplitCriterion -c 0.01 -l MC) -m 80 -x (ADWINChangeDetector -a 0.001) -p (ADWINChangeDetector -a 0.01)) -s (ArffFileStream -f D:\Dataset\Useless\elecNormNew.arff) -i 100000 -f 4532) -j C:\Users\GGPC\Outputs.ipynb -e
```

- EvaluatePrequentialRegression

```batch
WriteConfigurationToJupyterNotebook -t (EvaluatePrequentialRegression -l (meta.AdaptiveRandomForestRegressor -l (ARFFIMTDD -s VarianceReductionSplitCriterion -g 50 -c 0.01 -l 0.01) -m 80 -a 1.0 -x (ADWINChangeDetector -a 0.001) -p (ADWINChangeDetector -a 0.01)) -e BasicRegressionPerformanceEvaluator -i 100000 -f 4532) -j C:\Users\GGPC\Outputs.ipynb -e
```

Open MOA GUI. Under "Other Tasks" tab and select "WriteConfigurationToJupyterNotebook":

![WriteConfigurationToJupyterNotebook homepage](images\moa-jb-home.png "WriteConfigurationToJupyterNotebook homepage")

Select “Configure” to open “Configure task”. In the field “NotebookFile”, locate the place where you want to save the exported file and input its name.

![WriteConfigurationToJupyterNotebook savefile](images\moa-jb-savefile.png "WriteConfigurationToJupyterNotebook savefile")

You can click “Edit” button and configure the task with desired parameters:

![WriteConfigurationToJupyterNotebook edittasks](images\moa-jb-edittasks.png "WriteConfigurationToJupyterNotebook edittasks")

(Optional) You can export IPYNB files with or without running the tasks by tick or untick the runConfig option corresponding. By default, MOA exports the files without running the task.

![WriteConfigurationToJupyterNotebook runconfig](images\moa-jb-runconfig.png "WriteConfigurationToJupyterNotebook runconfig")

You need to tick "exportAdvancedNotebook", or will be unsuccessful:

![WriteConfigurationToJupyterNotebook export advanced notebook](images\moa-jb-advancednotebook.jpg "WriteConfigurationToJupyterNotebook export advanced notebook")

Open the exported IPYNB file on Jupyter Notebooks, change "%classpath" to "moa-flow-core-0.0.1-SNAPSHOT.jar" located before you run all code cells.

**Hint**: Use "/" in "classpath".

```java
%classpath "D:/moa-flow/moa-flow-core/target/moa-flow-core-0.0.1-SNAPSHOT.jar"
```

## Displaying the output result in table format

The result table has long rows, but the CSS style of Jupyter Notebooks is designed to wrap the long rows by default, which makes the table distorted. To come up with that, we need to customise the default CSS file of Jupyter Notebooks by adding a file named custom.css following the instruction as bellow:

- Type following command to the console to find your configuration directory by :

```batch
> jupyter --config-dir
C:\Users\username\.jupyter
```

- Create a new folder (if not existed yet) named custom inside .jupyter\, then copy & paste the file custom.css into that folder (mine is: C:\Users\username\.jupyter\custom\custom.css).

- Restart the Jupyter Notebooks.

---

Click "Run" and if the output like this means that you have successfully export a task from MOA GUI and run it on Jupyter Notebooks.

![WriteConfigurationToJupyterNotebook outputs](images\moa-jb-outputs.png "WriteConfigurationToJupyterNotebook outputs")
