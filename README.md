# Get-KapeModuleBinaries
Downloads binaries used by KAPE

This script will discover and download all available EXE, ZIP, and PS1 files referenced in KAPE Module files and download them to $Des. Optionally it can be fed a txt file containing URLs to download or used to view the list of binaries to be downloaded. See examples below for usage. 

This was created from Eric Zimmerman's Get-ZimmermanTools script. I just modified a few things to have it parse the KAPE module (mkape) files and download binaries.  

Rerunning the script will download a new copy of Eric's tools only if a newer version exists. All other tools will be download again even if a newer version is not available. To force Eric's tools to download a new copy, delete the line for that tool in the "!!!RemoteFileDetails.csv" file from the directory specified in the -Dest parameter.

## Prerequisites
* KAPE must be installed prior to running this script - https://binaryforay.blogspot.com/2019/02/introducing-kape.html
* PowerShell 5 or later required

## Installation

Download and extract zip. Set PowerShell execution policy to allow execution of scripts by launching PowerShell as an administrator and running the following: 

PS C:\Tools> Set-ExecutionPolicy -executionpolicy bypass

## Examples

### Example 1
Downloads/extracts and saves binaries and binary details to "C:\Forensic Program Files\Zimmerman\Kape\Modules\Bin" directory.

    PS C:\Tools> .\Get-KapeModuleBinaries.ps1 -Dest "C:\Forensic Program Files\Zimmerman\Kape\Modules\Bin" -ModulePath "C:\Forensic Program Files\Zimmerman\Kape\Modules"

### Example 2
Scans modules directory for mkape files, extracts URLs and dumps to console. This can be used to create a text file for use 
with the -UseBinaryList and -BinaryList path parameters or just to verify which tools will be downloaded prior to running
.\Get-KapeModuleBinaries.ps1 -Dest <desired tool path> -ModulePath "<Kape Modules Path>"    

    PS C:\Tools> .\Get-KapeModuleBinaries.ps1 -ModulePath "C:\Forensic Program Files\Zimmerman\Kape\Modules" -CreateBinaryList

### Example 3
Downloads/extracts and saves binaries and binary details for files specified in C:\tools\binarylist.txt to C:\Forensic Program Files\Zimmerman\Kape\Modules\Bin directory.

    PS C:\Tools> .\Get-KapeModuleBinaries.ps1 -Dest "C:\Forensic Program Files\Zimmerman\Kape\Modules\Bin" -UseBinaryList -BinaryListPath C:\tools\binarylist.txt
    

## Change log
* 10/2/19
    - Updated script to support new module sub-folder paths (thanks @mattnotmax)
    - Added check for illegal file name charcters prior to saving files
    - Fixed path typo in examples

* 7/5/19
    - Modified path files are extracted to for more consistency with KAPE module paths
    - Added -CreateBinary list parameter to dump list of URLs avaialble to donwload to console
    - Added -UseBinaryList and -BinaryList parameters to provide greater control over which binaries are donwloaded
    - Added Example_BinaryList.txt as an example of format of files used by -UseBinaryList and -BinaryList parameters 
    - Added additional error handling
    - Removed 7Zip dependency- Now uses Expand-Archive cmdlet instead of 7zip to extract files