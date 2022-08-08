# Hardware and Software Requirements #

The minimum software requirement to run Juicebox is a working Java installation
(version > 1.6) on Windows, Linux, and Mac OSX.  We recommend using the latest
Java version available, but please do not use the Java Beta Version. Minimum
system requirements for running Java can be found at
http://java.com/en/download/help/sysreq.xml. To download and install the latest
Java Runtime Environment (JRE), please go to http://www.java.com/download.

We recommend having at least 2GB free RAM for the best user experience with
Juicebox.

# Running from the jar #
To launch the Juicebox application from command line, type
```java 
java -Xms512m -Xmx2048m -jar Juicebox.jar
```

Note that the name of the command line tools jar might change depending on the version you downloaded and the name given in the `build.xml` file.

Also note that the `-Xms512m` flag sets the minimum memory heap size at 512 megabytes, and
the `-Xmx2048m` flag sets the maximum size at 2048 megabytes (2 gigabytes). These
values may be adjusted as appropriate for your machine.

# Compiling Jars from Source Files #
1. You should have Java 1.8 JDK and Apache Ant installed on your system. See
   below for more information.
2. Go to the folder containing the Juicebox source files and edit the
   juicebox.properties file with the proper Java JDK Address.
3. Open the command line, navigate to the folder containing the build.xml file
   and type
   ```
     ant
   ```
   The process should take no more than a minute to build on most machines.
4. The jars are written to the directory out/.  You can change this by editing
   the build.xml file.

## Installing Java 1.8 JDK ##

For Windows/Mac/Linux, the Java 1.8 JDK can be installed from here:

http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

(Alternative) For Ubuntu/Linux

http://tecadmin.net/install-oracle-java-8-jdk-8-ubuntu-via-ppa/

## Installing Apache Ant ##

### Mac ###

  Ant should be installed on most Macs. To verify installation via the command
  prompt, type
    `ant -version`
  If Ant is not on your Mac, install it via homebrew. At the command prompt, type
```    
brew update
brew install ant
```
  You may need to install [Homebrew](http://brew.sh/) on your machine
  
  See [this Stackoverflow post](http://stackoverflow.com/questions/3222804/how-can-i-install-apache-ant-on-mac-os-x) for more details.

### Windows ###

  Installing Ant requires some minor changes to your system environment. Follow
  the instructions in [this article](http://www.nczonline.net/blog/2012/04/12/how-to-install-apache-ant-on-windows/).

### Linux ###

  In the command prompt, type
```
sudo apt-get install ant
```
  or
```    
sudo yum install ant
```
  depending on your package installer

# Contributing to Juicebox
We use [the github repository you're browsing](https://github.com/theaidenlab/juicebox) for source control.  Please feel free to report bugs or request features using the [Issues tab](https://github.com/theaidenlab/juicebox/issues).  If you'd like to contribute, feel free to fork our repository and send a pull request with your modifications. 

## Coding in IntelliJ
[https://www.jetbrains.com/idea/](IntelliJ IDEA) is our preferred visual editor for Juicebox. The Community edition is free.

To set up in IDEA, have the Java SDK installed and link it with IntelliJ (IntelliJ has lots of
documentation on this and will bring it up as a popup if it's not done).

* Then go to `VCS` → `checkout from version control`. (You'll need to have forked the Juicebox repo)
* You'll need to do is be sure `*.sizes` is included as a file to be copied over to the class files.
Set this up via IntelliJ `Preferences` -> `Compiler`. Add `?*.sizes` to the list of `Resource Patterns`.
* While there, also go to `Java Compiler` and put this into additional command line options: `-Xlint:all -target 1.7`
The former turns on all warnings, the latter gives some flexibility since some people haven't updated Java to 1.8 yet.
* Then go to `Run` -> `Edit Configurations`.
* With the `+` sign, add `Application`.
* You'll create two of these, one for the GUI (call it Juicebox GUI or whatever you want, really) and one for the command line tools
* Set the main class by clicking the little `...` button next to the text box for main class

        MainWindow.java is the main method class for the visualization/GUI portion of the software.
        HiCTools.java is the main method class for the analysis/CLT portion.

* For the GUI under VM Options:
  ``` 
        -Xmx2000m
        -Djnlp.loadMenu="http://hicfiles.tc4ga.com/juicebox.properties"
  ```
* For the CLT use
   ```
        -Xmx2000m
   ```
* Note that the `Xmx2000m` flag sets the maximum memory heap size to 2GB.
Depending on your computer you might want more or less.
Some tools will break if there's not enough memory and the file is too large,
but don't worry about that for development; 2GB should be fine.
* One last note: be sure to `Commit and Push` when you commit files, it's hidden in
the dropdown menu button in the commit window.

