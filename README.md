
# Get open TELEMAC-MASCARET

Go to the developer's website ([opentelemac.org](http://www.opentelemac.org/)), register with your e-mail address, and log in.

Download the latest version of open TELEMAC-MASCARET from the [Download](http://www.opentelemac.org/index.php/download) page.

## Compile and install from scratch 

### Get pre-requisites

On Windows download and install the following programs:

* [TortoiseSVN](https://tortoisesvn.net/downloads.html) (requires admin rights
* [Python 3](https://www.python.org/)
     + With `numpy`, `scipy`, and `matplotlib` libraries (installing `numpy` involves the installation of `scipy` and `matplotlib`, too).
     + Consider to install *Anaconda* as described on [hydroinformatics.github.io](https://hydro-informatics.github.io/hypy_install.html).
     + When using *Anaconda*, `python` might be reserved to a local environment. Therefore, make sure to install `numpy`, `scipy`, and `matplotlib` in the *conda base* environment through *Anaconda Prompt* ([read more](https://hydro-informatics.github.io/hypy_install.html#install-pckg)).
     + Add the PATH of the *conda base* environment to the system PATH *Variable* in *Windows* (follow instructions provided for *MinGW*, but replace `C:\MinGW\bin` with `C:\Users\YOUR-USER-NAME\Anaconda3`).
     + Read more about the link between *Python* scripts and TELEMAC in the [developer's Wiki](http://wiki.opentelemac.org/doku.php?id=python:python_for_telemac).
* TELEMAC developers describe the installation of *mpich*, which is cannot be installed anymore in Windows 10. Here is a work-around:<a name="mpi-win"></a>
    + WARNING: THE MPICH INSTRUCTIONS ARE NOT VERIFIED!
    + Download (choose the *msi* file) and install Microsoft's latest MPI software development kit from [Microsoft's Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=100593)
    + After the installation, the compiled MPI executables should be located in *C:\Program Files\Microsoft MPI\Bin* (verify that *smpd.exe* and *mpiexec.exe* are in the directory). 
    + **Alternatively** download a pre-compiled version of TELEMAC from the [developer's Installation files] page (e.g., [v6p3 64b](http://www.opentelemac.org/index.php/binaries/summary/40-manual-installation-pre-compiled-binaries/162-compiled-windows-gfortran480-mpi-64b)) and copy the *mpich2* and *metis* folders to a new folder called *C:\opentelemac*.
    + Add the *MPI* PATH to the system PATH *Variable* in *Windows* (follow instructions provided for *MinGW*, but replace `C:\MinGW\bin` with `C:\Program Files\Microsoft MPI\Bin` OR, for the alternative, `C:\opentelemac\metis;C:\opentelemac\mpich2\include`).
* [MinGW](http://www.mingw.org/) (includes Fortran compiler repositories)

After the installation of MinGW, open *MinGW Installer* (either from *Start* and look for *MinGW Installation Manager* or use the desktop icon), go to *Basic Setup* > right-click on `mingw32-gcc-fortran-bin` (latest version) and select *Mark for Installation*. Then go to the *Installation* menu (top-left of the *MinGW Installation Manager* window) and click on *Apply Changes*. A window pops up and informs about the installation status. Close the pop-up window after successful installation.
The *MinGW* directory should now contain a *gfortran.exe* that is recognized by the system as environment variable. To test if your system recognizes the `gfortran` environment variable, open a command line (e.g., click on *Start*, type `cmd` and hit *Enter*), and type `gfortran`. If the system answers *'gfortran' is not regonized as an internal or external command, operable program or batch file.*, further action is required:<a name="mingw"></a>

* To tell *Windows* to look in *C:\MinGW\bin* for the compiler, open a *Windows* *Explorer* window (e.g., press the *Windows* and *E* keys on the keyboard).
* Go to your *MinGW* installation directory and identify where *gfortran.exe* is located (e.g., use the *search* box on the top right of the *Windows* *Explorer* window). The following steps assume that the file is stored as *C:\MinGW\bin\gfortran.exe*.
* Click on *Start* and type `env`. Select *Edit the system environment variables* (requires admin rights). A *System Properties* window pops up.
* In the *System Properties* window go to the *Advanced* tab and click on *Environment Variables ...* button near the bottom of the window.
* In the *System variables* box (important: *User variables for [...]* will not work if your admin account is not the same as your standard user account, which is good practice) check if there is a *Variable* called *PATH*.
    + If there already is a *PATH* Variable, click *Edit...* and add the following to the end of the line: `;C:\MinGW\bin`
    + If there is no *PATH* Variable, click *New...* and enter:
    
```
Variable Name: PATH
Variable Value: C:\MinGW\bin
```

* Click *OK* in the *Environment Variables* and *System Properties* windows.
* Close all open command line windows (if any), and re-open a new command line window (must be successively done). Type `gfortran`. Now, the system's reponse should be *gfortran: fatal error: no input files* (which is OK here, because we only want to test if the system recognizes the `gfortran` command).

> ***Note***: More information about Fortran compilers for *Windows* can be found in the [GCC Wiki](https://gcc.gnu.org/wiki/GFortranBinariesWindows).


On Linux download and install the following programs:

* [kdesvn](https://kde.org/applications/en/development/org.kde.kdesvn)


## Download files form TELEMAC SVN repository
Download the latest version of open TELEMAC from the SVN repository indicated on the [developer's website](http://www.opentelemac.org/index.php/sources-svn).

At the time of writing this article, the address of the latest SVN repository is [http://svn.opentelemac.org/svn/opentelemac/tags/v8p1r0/](http://svn.opentelemac.org/svn/opentelemac/tags/v8p1r0/).

## Install (compile)
http://www.opentelemac.org/index.php/documentation/installation13?lang=en


### Windows <a name="compile-win"></a>

Follow the [installation instructions](http://wiki.opentelemac.org/doku.php?id=installation_on_windows) on the developer's website. The following instructions are a slightly modified version of the [installation website](http://wiki.opentelemac.org/doku.php?id=instructions_to_finish_installing_the_telemac_system_manually_after_a_failure_of_the_automatic_installation):

1. Open command line
1. Enter (replace `v8p1r0` with the desired version and `C:\opentelemac\v8p1` with the target installation directory) - may take a while:
```
svn co http://svn.opentelemac.org/svn/opentelemac/tags/v8p1r0 "C:\opentelemac\v8p1" --username ot-svn-public --password telemac1*
```
1. Copy configuration file (see github file)
1. Create a shortcut on your Desktop (right-click > *New shortshut*)
    * Define `C:\Windows\System32\cmd.exe` as location item
    * Enter "Telemac v8p1" as name
1. Right-click on the new shortcut and edit properties:
    * **Target** box: `C:\Windows\System32\cmd.exe E:ON /V:ON /K set SYSTELCFG=C:\opentelemac\v8p1\configs\systel.cis-windows.cfg && PATH=C:\opentelemac\v8p1\scripts\python3;!PATH!`
    * **Start in** box: `C:\telemac\v8p1\`
1. Verify and modify (if necessary) *C:\opentelemac\v8p1\configs\**systel.cis-windows.cfg***:
    * Go to the *windows 7 gfortran scalar* section (typically line 82 onward) and identify the call to *gfortran*<br> - typically: `gfortran -c -O3 -fopenmp -fconvert=big-endian [...]`.
    * If `-cpp` is not included in the call, add it, for example, like this:<br>`gfortran -c -cpp -O3 -fopenmp -fconvert=big-endian [...]`
    * With MPI installed according to the [above descriptions](#mpi-win), find all *strings* containing `C:\opentelemac\mpi\bin\mpiexec.exe` and replace them with `mpiexec` (i.e., an environment variable).
1. Doubleclick on the new shortcut and type:
    * `python scripts/python3/compile_telemac.py`
    * *Hint: Grab a beverage now. Compiling may take up to 30 minutes.*
    * If you encounter errors and need to recompile use<br>`python scripts/python3/compile_telemac.py --clean`
    

To test if the installation was successful, go to the [Run > Test on *Windows*](#run-win) section and try to start one of the provided TELEMAC test cases.


### Linux

Follow the [installation instructions](http://wiki.opentelemac.org/doku.php?id=installation_on_linux) on the developer's website.


## OpenTelemac Docker

Download and install [Docker](https://www.docker.com/).

Go to Frédéric Deniger's [GitLab](https://gitlab.com/capedev-labs/telemac-docker/blob/master/README.md) pages.


# Run

## Test TELEMAC
To get familiar with the usage of TELEMAC, use one of the open TELEMAC test cases (e.g., as described on the [developer's website](http://wiki.opentelemac.org/doku.php?id=how_to_run_a_simulation)), which are typically located in the installation directory (e.g., *C:\opentelemac\v8p1\examples*).

### Test on *Windows* <a name="run-win"></a>

The following workflow builds on the steps described on the [developer's website](http://wiki.opentelemac.org/doku.php?id=how_to_run_a_simulation) and uses the *bump* example (typically located in *C:\opentelemac\v8p1\examples\telemac2d\bump*):

1. Start the open TELEMAC command line environment [created in the installation (compilation)](#compile-win) by double clicking on the *Telemac v8p1* symbol on the desktop.
1. Go to the test case directory (e.g., `cd examples\telemac2d\bump`)
1. Run the telemac2d *Python* script:<br>`python scripts/python3/telemac2d.py t2d_bump_FE.cas`


# *Blue Kenue* (graphical user interface for pre- and post-processing)

## Download and install the program

*Blue Kenue* is a convenient graphical user interface (GUI) provided by the *National Research Council* (NRC) ot the *Government of Canada*, for pre- and post-processing data for use with TELEMAC. *Blue Kenue* is primarily designed for Windows platforms, but should also run with the *Wine* environment on Linux platform.
To get *Blue Kenue*, go to the NRC's [*Blue Kenue* landing page](https://nrc.canada.ca/en/research-development/products-services/software-applications/blue-kenuetm-software-tool-hydraulic-modellers) and download the program. Follow the normal installation routines.

## Get the documentation and beta dvelopments

To get the documentation and/or newer beta-releases of *Blue Kenue*, go to [chyms.nrc.gc.ca](https://chyms.nrc.gc.ca/) and log in with the following credentials (source: [Telemac forum](http://opentelemac.org/index.php/kunena/blue-kenue/10589-blue-kenue-beta-release-download-site#25570)):

* User: `Public.User`
* Password: `anonymous`

Got to the **Public Download Area** section and enter the requested information (First and Last name, affiliation, Email, and Telephone). Then click on the button **Agree and proceed to public download area**. Now, the CHyMS should open.

Scroll down to the **Blue Kenue** section to download beta releases and/or documentation/support files. The list of provided files is long and here are some recommendations:

* *Blue Kenue* tutorial by Maron Faure ([zip file](https://chyms.nrc.gc.ca/download_public/KenueClub/BlueKenue/Data/2013_BlueKenue_Tutorial_Maron-Faure_fr-en.zip))
* TELEMAC Baxter tutorial ([zip file](https://chyms.nrc.gc.ca/download_public/KenueClub/BlueKenue/Data/TELEMAC_2D_Baxter_tutorial_files_en.zip))
* Post-processing TELEMAC output [Video by Julian Cousineau](https://chyms.nrc.gc.ca/download_public/KenueClub/BlueKenue/Videos/JulienCousineau_IntroToAnimatingTelemacResultsInBlueKenue.mpeg)
*






