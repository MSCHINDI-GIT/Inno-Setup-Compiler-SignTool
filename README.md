# Inno-Setup-Compiler-SignTool
Special Inno Setup Compiler SignTool (It retains the TIME of executable files!)

Now you can automatically SIGN your compiled Inno Setup (Un-)Installer Setup.exe Files and other Files in them!

But there is a the Problem with the Sign Mechanism from Inno Setup Compiler - together with the Microsoft Sign Tool:
When i use the "[Files] Flags: sign, for my various executable files, that all the Source Files Date/Time are set to the compiler time...  Sad

That's - why I created a Signtool Starter now

It retains the Date/Time of executable files!

My program is simply switched between Inno Setup Compiler and MS-SignTool...

This sounds simple, but the evaluation from the command line parameters and pathes is a bit tricky...

The original Microsoft SignTools.exe must be placed in the same folder as Inno Setup Compiler or in the same Folder of INNO SignTool Runner (e.g. in Subfolder "Plugins") or in a Subfolder from them named "CERT"

To use a signing, you must make first an Entry in Inno Setup Compiler Menu under Tools, Configure Sign Tool:

Name of the Sign Tool:
e.g.
SchindiSoft_Code_Sign
Command of the Sign Tool:
e.g.  if you had create a Plugins Folder in InnoSetp Compiler ProgramFiles Folder
".\Plugins\Inno_SignTool.exe" sign /f ".\Plugins\CERT\SchindiSoft_CODE_CERT.pfx" /p Password_PW$ /t "http://timestamp.digicert.com" /fd SHA256 $p

Password_PW$=Your PW...

it makes a Reg-Entry:
Example Reg Entry if you had create a Plugins Folder in InnoSetp Compiler ProgramFiles Folder
REGEDIT4

[HKEY_CURRENT_USER\Software\Jordan Russell\Inno Setup\SignTools]
"SignTool0"="SchindiSoft_Code_Sign=\".\\Plugins\\Inno_SignTool.exe" sign /f \".\\Plugins\\CERT\\SchindiSoft_CODE_CERT.pfx\" /p SchindiSoft-PW$ /t \"http://timestamp.digicert.com\" /fd SHA256 $p"

And then the additions to the Inno Setup Script (see Inno Setup Help too):
in [Setup] Section:
e.g.
[Setup]
;;SignTool=The same name as in Sign Tool Configuration!
SignTool=SchindiSoft_Code_Sign $f
...

and when you wish to Sign own Files too:  (that is the actual purpose of the plugin)
In [Files] Section
e.g.
[Files]
First all Files from Folder Shared...
Source: "D:\Data\Projekte\Shared\MyTools\*.*"; DestDir: "{app}"; Flags: ignoreversion
;and then a second entry so that only the *.exe files are signed...
Source: "D:\Data\Projekte\Shared\MyTools\*.exe"; DestDir: "{app}"; Flags: ignoreversion signonce (or sign)
;or only one exe...
Source: "D:\Data\Projekte\Shared\MyTools\xyz.exe"; DestDir: "{app}"; Flags: ignoreversion signonce (or sign)
...

And of course you also need a suitable (ev. self-created...) SIGN (*.pfx) file for code certification (i put them in the Subfolder ...\CERT)...

wfg. from Schindi aus Austria








Under Construction+
