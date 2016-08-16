# LPB-mediainfo-batch
Steps LPB used to batch create PBCore 2.0 compliant xml files with MediaInfo

# About
So, I'm totally new to GitHub. I'm posting this documentation of LPB's process for batch creating MediaInfo files (admittedly not exactly rocket science), in order to introduce myself to the interface (probably also not rocket science). So apologies for any bonehead mistakes in here.

Our goal at LPB was to run MediaInfo on all of our web media files (videos that are available streaming at: http://ladigitalmedia.org/), and export a separate XML file for each one. These xml files will later be used to populate our MySQL database.  

# Dependencies
+ You'll need the CLI version of MediaInfo which can be downloaded here: https://mediaarea.net/en/MediaInfo/Download
+ Microsoft Excel (or equivalent)
+ LPB works in a Windows environment, not sure about compatibility with other OS.

#Basics
To create one xml file through MediaInfo use this command:
  mediainfo --Output=PBCore2 'input file name' > 'output file name.xml'

Thanks to Dave Rice for creating the PBCore 2 output in mediainfo, more here: https://github.com/dericed/MediaInfo

#Batch
Creating more than one xml file is a bit more complicated, so we chose to create a batch file, or .bat file, and run that through the Windows command line. The batch file is just the command from the section above, written over and over again, with the file name of the input and output changed accordingly. 

We exported a list of our files through the command line using the Windows "DIR" command (similar to the Mac/Linux "ls" command). Looks like this:
  C:\Media\IPutMyVideoFilesHere> DIR > 'files.txt'

Then we used Excel to create the list of commands that would eventually be our batch file.

#Excel
I've attached an Excel file to this repo with the different formulas "baked in" but I'll list them here as well. 

1. The first column, A, is populated with the file names output from the DIR command. 
2. Column B is populated with the MediaInfo command "mediainfo --output=PBCore2"
  * note that the "PBCore2" part of that command is case sensitive 
3. Column C uses the formula:
=LEFT(A01,LEN(A01)-3)&"xml"
4. Column D uses the formula:
=CONCATENATE(B01,A01,">",C01)

The contents of column D from step five made up the contents of our batch file.

#All set
From there just run the batch file in the same directory the DIR command was run (since the file names don't have the full path).

Big thanks to John Tooraen of LPB, who really did all of this, and I just watched.
