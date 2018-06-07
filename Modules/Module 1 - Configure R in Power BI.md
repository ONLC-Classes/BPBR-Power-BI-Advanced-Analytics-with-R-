INSTALLING R
------------

You can run R scripts directly in **Power BI Desktop**, and import the
resulting datasets into a Power BI Desktop data model.

Install R
---------

To run R scripts in Power BI Desktop, you need to install **R** on your
local machine. You can download and install **R** for free from many
locations, including the [Revolution Open download
page](https://mran.revolutionanalytics.com/download/), and the [CRAN
Repository](https://cran.r-project.org/bin/windows/base/). The current
release of R scripting in Power BI Desktop supports Unicode characters
as well as spaces (empty characters) in the installation path.

Using R in Query Editor
-----------------------

To show how to use **R** in **Query Editor**, take this example from a
stock market dataset, based on a .CSV file that you can [download from
here](http://download.microsoft.com/download/F/8/A/F8AA9DC9-8545-4AAE-9305-27AD1D01DC03/EuStockMarkets_NA.csv)
and follow along. The steps for this example are the following:

1.  First, load your data into **Power BI Desktop**. In this example,
    > load the *EuStockMarkets\_NA.csv* file and select **Get Data \>
    > CSV** from the **Home** ribbon in **Power BI Desktop**.

![](.//Media/img1mod1.png)

2.  Select the file and select **Open**, and the CSV is displayed in the
    > **CSV file** dialog.

![](.//Media/img2mod1.png)

3.  Once the data is loaded, you\'ll see it in the **Fields** pane in
    > Power BI Desktop.

![](.//Media/img3mod1.png)

4.  Open **Query Editor** by selecting **Edit Queries** from the
    > **Home** tab in **Power BI Desktop**.

![](.//Media/img4mod1.png)

5.  In the **Transform** tab, select **Run R Script** and the **Run R
    > Script** editor appears (shown in the next step). Notice that rows
    > 15 and 20 suffer from missing data, as do other rows you can\'t
    > see in the following image. The steps below show how R can (and
    > will) complete those rows for you.

![](.//Media/img5mod1.png)

6.  For this example, enter the following script code:

> Copy
>
> library(mice)
>
> tempData \<- mice(dataset,m=1,maxit=50,meth=\'pmm\',seed=100)
>
> completedData \<- complete(tempData,1)
>
> output \<- dataset
>
> output\$completedValues \<- completedData\$\"SMI missing values\"
>
> Note
>
> You\'ll need to have the *mice* library installed in your R
> environment for the previous script code to work properly. To install
> mice, run the following command in your R installation: \| \>
> install.packages(\'mice\')
>
> When put into the **Run R Script** dialog, the code looks like the
> following:
>
![](.//Media/img6mod1.png)

7.  After selecting **OK**, **Query Editor** displays a warning about
    > data privacy.

![](.//Media/img7mod1.png)

8.  For the R scripts to work properly in the Power BI service, all data
    > sources need to be set to *public*. For more information about
    > privacy settings and their implications, see [Privacy
    > Levels](https://docs.microsoft.com/en-us/power-bi/desktop-privacy-levels).

![](.//Media/img8mod1.png)
>
> Notice a new column in the **Fields** pane called *completedValues*.
> Notice there are a few missing data elements, such as on row 15 and
> 18. Take a look at how R handles that in the next section.

With just five lines of R script, **Query Editor** filled in the missing
values with a predictive model.

Run R scripts

With just a few steps in Power BI Desktop, you can run R scripts and
create a data model, from which you can create reports, and share them
on the Power BI service. R scripting in Power BI Desktop now supports
number formats that contain decimals (.) and commas (,).

Prepare an R script

To run an R script in Power BI Desktop, create the script in your local
R development environment, and make sure it runs successfully.

To run the script in Power BI Desktop, make sure the script runs
successfully in a new and unmodified workspace. This means that all
packages and dependencies must be explicitly loaded and run. You can use
*source()* to run dependent scripts.

When preparing and running an R script in Power BI Desktop, there are a
few limitations:

-   Only data frames are imported, so make sure the data you want to
    > import to Power BI is represented in a data frame

-   Columns that are typed as Complex and Vector are not imported, and
    > are replaced with error values in the created table

-   Values that are N/A are translated to NULL values in Power BI
    > Desktop

-   Any R script that runs longer than 30 minutes times out

-   Interactive calls in the R script, such as waiting for user input,
    > halts the script's execution

-   When setting the working directory within the R script, you *must*
    > define a full path to the working directory, rather than a
    > relative path

Run your R script and import data

1.  In Power BI Desktop, the R Script data connector is found in **Get
    > Data**. To run your R Script, select **Get Data \> More\...**,
    > then select **Other \> R script** as shown in the following image:

2.  If R is installed on your local machine, the latest installed
    > version is selected as your R engine. Simply copy your script into
    > the script window and select **OK**.

3.  If R is not installed, is not identified, or if there are multiple
    > installations on your local machine, expand **R Installation
    > Settings** to display installation options, or to select which
    > installation you want to run the R script.

![](.//Media/img9mod1.png)
>
> If R is installed and is not identified, you can explicitly provide
> its location in the text box provided when you expand **R Installation
> Settings**. In the above image, the path *C:\\Program
> Files\\R\\R-3.2.0* is explicitly provided in the text box.
>
> R installation settings are centrally located in the R Scripting
> section of the Options dialog. To specify your R installation
> settings, select **File \> Options and settings** and then **Options
> \> R scripting**. If multiple installations of R are available, a
> drop-down menu appears that allows you to select which installation to
> use.

4.  Select **OK** to run the R Script. When the script runs
    > successfully, you can then choose the resulting data frames to add
    > to the Power BI model.

Refresh

You can refresh an R script in Power BI Desktop. When you refresh an R
script, Power BI Desktop runs the R script again in the Power BI Desktop
environment.
