# utl-altair-slc-powershell-calculating-and-validating-file-hash-using-different-algorithms
Altair slc powershell calculating and validating file hash using different algorithms
    %let pgm=utl-altair-slc-powershell-calculating-and-validating-file-hash-checksum-using-different-algorithms;

    %stop_submission;

    Altair slc powershell calculating and validating file hash checksum using different algorithms

    [GITHUB](https://github.com/rogerjdeangelis/utl-altair-slc-powershell-calculating-and-validating-file-hash-using-different-algorithms)
    https://github.com/rogerjdeangelis/utl-altair-slc-powershell-calculating-and-validating-file-hash-using-different-algorithms

    [SIEMENS POST](https://support.industry.siemens.com/cs/document/109806390/ruggedcom-rox-ii-hash-checksums-?dti=0&lc=en-US)
    https://support.industry.siemens.com/cs/document/109806390

    CONTENTS

       1 create example txt file to generate a SHA-256 checksum.
       2 calculate file hash using different algorithms
       3 validate hash
       4 drop down to powershell macros
        [tools](https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories)

    /*                                  _         __ _ _
    / |   _____  ____ _ _ __ ___  _ __ | | ___   / _(_) | ___
    | |  / _ \ \/ / _` | `_ ` _ \| `_ \| |/ _ \ | |_| | |/ _ \
    | | |  __/>  < (_| | | | | | | |_) | |  __/ |  _| | |  __/
    |_|  \___/_/\_\__,_|_| |_| |_| .__/|_|\___| |_| |_|_|\___|
                                 |_|
    */

    /*--- CREATE EXAMPLE INPUT FILE FOT CHECKING HASH CHECKSUB ----*/

    %slc_psbegin;
    cards4;
    # Create sample text file
    @"
    Hello, this is a test file.
    It is used to generate a SHA-256 checksum.
    Line 3: Checking integrity.
    Line 4: Using PowerShell for hash calculation.
    "@ | Out-File -FilePath "d:/txt/example.txt" -Encoding UTF8

    Write-Host "File 'd:/txt/example.txt' created successfully." -ForegroundColor Green
    ;;;;
    %slc_psend;

    /**************************************************************************************************************************/
    /* d:/txt/example.txt                                                                                                     */
    /*                                                                                                                        */
    /* Hello, this is a test file.                                                                                            */
    /* It is used to generate a SHA-256 checksum.                                                                             */
    /* Line 3: Checking integrity.                                                                                            */
    /* Line 4: Using PowerShell for hash calculation.                                                                         */
    /**************************************************************************************************************************/

    /*                              _        _
      _____  ____ _ _ __ ___  _ __ | | ___  | | ___   __ _
     / _ \ \/ / _` | `_ ` _ \| `_ \| |/ _ \ | |/ _ \ / _` |
    |  __/>  < (_| | | | | | | |_) | |  __/ | | (_) | (_| |
     \___/_/\_\__,_|_| |_| |_| .__/|_|\___| |_|\___/ \__, |
                             |_|                     |___/
    */

    1                                          Altair SLC        17:07 Thursday, April 23, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: AUTOEXEC source line
    1       +  ï»¿ods _all_ close;
               ^
    ERROR: Expected a statement keyword : found "?"

    NOTE: AUTOEXEC processing completed

    1         %slc_psbegin;
    2         cards4;

    NOTE: The file 'c:\temp\ps_pgm.ps1' is:
          Filename='c:\temp\ps_pgm.ps1',
          Owner Name=SLC\suzie,
          File size (bytes)=0,
          Create Time=14:40:04 Mar 21 2026,
          Last Accessed=17:07:44 Apr 23 2026,
          Last Modified=17:07:44 Apr 23 2026,
          Lrecl=32767, Recfm=V

    NOTE: 10 records were written to file 'c:\temp\ps_pgm.ps1'
          The minimum record length was 80
          The maximum record length was 82
    NOTE: The data step took :
          real time : 0.000
          cpu time  : 0.000


    3         $expectedHash = "DF85E0E8C4A714CB053862F60A2F0B0CF54B48F53DC708A4516337878F64F62D"
    4         $actualHash = (Get-FileHash -Path "d:/txt/example.txt" -Algorithm SHA256).Hash
    5
    6         if ($actualHash -eq $expectedHash) {
    7             Write-Host "Checksum matches! File is intact." -ForegroundColor Green
    8         } else {
    9             Write-Host "Checksum MISMATCH! File may be corrupted." -ForegroundColor Red
    10            Write-Host "Expected: $expectedHash" -ForegroundColor Yellow
    11            Write-Host "Actual:   $actualHash" -ForegroundColor Yellow
    12        }
    13        ;;;;
    14        %slc_psend;

    NOTE: The infile rut is:
          Unnamed Pipe Access Device,
          Process=powershell.exe -executionpolicy bypass -file c:/temp/ps_pgm.ps1 >  c:/temp/ps_pgm.log,
          Lrecl=32756, Recfm=V

    NOTE: No records were written to file PRINT

    NOTE: No records were read from file rut
    NOTE: The data step took :
          real time : 0.572
          cpu time  : 0.000

    NOTE: The infile rut is:
          Unnamed Pipe Access Device,
          Process=powershell.exe -executionpolicy bypass -file c:/temp/ps_pgm.ps1 >  c:/temp/ps_pgm.log,
          Lrecl=32767, Recfm=V

    NOTE: No records were written to file PRINT

    NOTE: No records were read from file rut
    NOTE: The data step took :
          real time : 0.538
          cpu time  : 0.015

    NOTE: The infile 'c:\temp\ps_pgm.log' is:
          Filename='c:\temp\ps_pgm.log',
          Owner Name=SLC\suzie,
          File size (bytes)=34,
          Create Time=10:30:46 Mar 22 2026,
          Last Accessed=17:07:45 Apr 23 2026,
          Last Modified=17:07:45 Apr 23 2026,
          Lrecl=32767, Recfm=V

    Checksum matches! File is intact.
    NOTE: 1 record was read from file 'c:\temp\ps_pgm.log'
          The minimum record length was 33
          The maximum record length was 33
    NOTE: 1 record was written to file PRINT

    NOTE: The data step took :
          real time : 0.015
          cpu time  : 0.015


    15
    ERROR: Error printed on page 1

    NOTE: Submitted statements took :
          real time : 1.269
          cpu time  : 0.109
    /*___              _            _       _         _               _
    |___ \    ___ __ _| | ___ _   _| | __ _| |_ ___  | |__   __ _ ___| |__
      __) |  / __/ _` | |/ __| | | | |/ _` | __/ _ \ | `_ \ / _` / __| `_ \
     / __/  | (_| (_| | | (__| |_| | | (_| | ||  __/ | | | | (_| \__ \ | | |
    |_____|  \___\__,_|_|\___|\__,_|_|\__,_|\__\___| |_| |_|\__,_|___/_| |_|

    */

    %slc_psbegin;
    cards4;
    # Create sample text file
    # Function to calculate file hash using different algorithms
    function Get-Checksum {
        param(
            [Parameter(Mandatory=$true)]
            [string]$FilePath,

            [Parameter(Mandatory=$false)]
            [ValidateSet("SHA256", "SHA1", "MD5", "SHA384", "SHA512")]
            [string]$Algorithm = "SHA256"
        )

        # Check if file exists
        if (-not (Test-Path $FilePath)) {
            Write-Error "File '$FilePath' not found."
            return $null
        }

        try {
            # Calculate hash using built-in PowerShell cmdlet
            $hash = Get-FileHash -Path $FilePath -Algorithm $Algorithm
            return $hash
        }
        catch {
            Write-Error "Error calculating hash: $_"
            return $null
        }
    }

    # Example usage
    $inputFile = "d:/txt/example.txt"
    $hashResult = Get-Checksum -FilePath $inputFile -Algorithm "SHA256"

    if ($hashResult) {
        Write-Host "File: $($hashResult.Path)" -ForegroundColor Green
        Write-Host "Algorithm: $($hashResult.Algorithm)" -ForegroundColor Cyan
        Write-Host "Checksum: $($hashResult.Hash)" -ForegroundColor Yellow

        # Save checksum to file
        $hashResult.Hash | Out-File -FilePath "d:/txt/checksum.txt"
        Write-Host "`nChecksum saved to d:/txt/checksum.txt" -ForegroundColor Gray
    }
    ;;;;
    %slc_psend;

    /**************************************************************************************************************************/
    /*  Altair SLC                                                                                                            */
    /* File: D:\txt\example.txt                                                                                               */
    /* Algorithm: SHA256                                                                                                      */
    /* Checksum: DF85E0E8C4A714CB053862F60A2F0B0CF54B48F53DC708A4516337878F64F62D                                             */
    /*                                                                                                                        */
    /* Checksum saved to d:/txt/checksum.txt                                                                                  */
    /**************************************************************************************************************************/

    /*         _            _       _         _
      ___ __ _| | ___ _   _| | __ _| |_ ___  | | ___   __ _
     / __/ _` | |/ __| | | | |/ _` | __/ _ \ | |/ _ \ / _` |
    | (_| (_| | | (__| |_| | | (_| | ||  __/ | | (_) | (_| |
     \___\__,_|_|\___|\__,_|_|\__,_|\__\___| |_|\___/ \__, |
                                                      |___/
    */

    1                                          Altair SLC        17:19 Thursday, April 23, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: AUTOEXEC source line
    1       +  ï»¿ods _all_ close;
               ^
    ERROR: Expected a statement keyword : found "?"
    N
    NOTE: AUTOEXEC processing completed

    1         %slc_psbegin;
    2         cards4;

    NOTE: The file 'c:\temp\ps_pgm.ps1' is:
          Filename='c:\temp\ps_pgm.ps1',
          Owner Name=SLC\suzie,
          File size (bytes)=0,
          Create Time=14:40:04 Mar 21 2026,
          Last Accessed=17:19:20 Apr 23 2026,
          Last Modified=17:19:20 Apr 23 2026,
          Lrecl=32767, Recfm=V

    NOTE: 42 records were written to file 'c:\temp\ps_pgm.ps1'
          The minimum record length was 80
          The maximum record length was 80
    NOTE: The data step took :
          real time : 0.015
          cpu time  : 0.000


    3         # Create sample text file
    4         # Function to calculate file hash using different algorithms
    5         function Get-Checksum {
    6             param(
    7                 [Parameter(Mandatory=$true)]
    8                 [string]$FilePath,
    9
    10                [Parameter(Mandatory=$false)]
    11                [ValidateSet("SHA256", "SHA1", "MD5", "SHA384", "SHA512")]
    12                [string]$Algorithm = "SHA256"
    13            )
    14
    15            # Check if file exists
    16            if (-not (Test-Path $FilePath)) {
    17                Write-Error "File '$FilePath' not found."
    18                return $null
    19            }
    20
    21            try {
    22                # Calculate hash using built-in PowerShell cmdlet
    23                $hash = Get-FileHash -Path $FilePath -Algorithm $Algorithm
    24                return $hash
    25            }
    26            catch {
    27                Write-Error "Error calculating hash: $_"
    28                return $null
    29            }
    30        }
    31
    32        # Example usage
    33        $inputFile = "d:/txt/example.txt"
    34        $hashResult = Get-Checksum -FilePath $inputFile -Algorithm "SHA256"
    35
    36        if ($hashResult) {
    37            Write-Host "File: $($hashResult.Path)" -ForegroundColor Green
    38            Write-Host "Algorithm: $($hashResult.Algorithm)" -ForegroundColor Cyan
    39            Write-Host "Checksum: $($hashResult.Hash)" -ForegroundColor Yellow
    40
    41            # Save checksum to file
    42            $hashResult.Hash | Out-File -FilePath "d:/txt/checksum.txt"
    43            Write-Host "`nChecksum saved to d:/txt/checksum.txt" -ForegroundColor Gray
    44        }
    45        ;;;;
    46        %slc_psend;

    NOTE: The infile rut is:
          Unnamed Pipe Access Device,
          Process=powershell.exe -executionpolicy bypass -file c:/temp/ps_pgm.ps1 >  c:/temp/ps_pgm.log,
          Lrecl=32756, Recfm=V

    NOTE: No records were written to file PRINT

    NOTE: No records were read from file rut
    NOTE: The data step took :
          real time : 0.665
          cpu time  : 0.015



    NOTE: The infile rut is:
          Unnamed Pipe Access Device,
          Process=powershell.exe -executionpolicy bypass -file c:/temp/ps_pgm.ps1 >  c:/temp/ps_pgm.log,
          Lrecl=32767, Recfm=V

    NOTE: No records were written to file PRINT

    NOTE: No records were read from file rut
    NOTE: The data step took :
          real time : 0.600
          cpu time  : 0.031

    NOTE: The infile 'c:\temp\ps_pgm.log' is:
          Filename='c:\temp\ps_pgm.log',
          Owner Name=SLC\suzie,
          File size (bytes)=157,
          Create Time=10:30:46 Mar 22 2026,
          Last Accessed=17:19:21 Apr 23 2026,
          Last Modified=17:19:21 Apr 23 2026,
          Lrecl=32767, Recfm=V

    File: D:\txt\example.txt
    Algorithm: SHA256
    Checksum: DF85E0E8C4A714CB053862F60A2F0B0CF54B48F53DC708A4516337878F64F62D

    Checksum saved to d:/txt/checksum.txt
    NOTE: 5 records were read from file 'c:\temp\ps_pgm.log'
          The minimum record length was 0
          The maximum record length was 74
    NOTE: 5 records were written to file PRINT

    NOTE: The data step took :
          real time : 0.015
          cpu time  : 0.000

    ERROR: Error printed on page 1

    NOTE: Submitted statements took :
          real time : 1.439
          cpu time  : 0.140

    /*____              _ _     _       _             _               _
    |___ /  __   ____ _| (_) __| | __ _| |_ ___   ___| |__   ___  ___| | _____ _   _ _ __ ___
      |_ \  \ \ / / _` | | |/ _` |/ _` | __/ _ \ / __| `_ \ / _ \/ __| |/ / __| | | | `_ ` _ \
     ___) |  \ V / (_| | | | (_| | (_| | ||  __/| (__| | | |  __/ (__|   <\__ \ |_| | | | | | |
    |____/    \_/ \__,_|_|_|\__,_|\__,_|\__\___| \___|_| |_|\___|\___|_|\_\___/\__,_|_| |_| |_|

    */

    /*--- CUT AND PASTE THE CHECKSUM INTO THE POWERSHELL CODE BELOW ---*/

    %slc_psbegin;
    cards4;
    $expectedHash = "DF85E0E8C4A714CB053862F60A2F0B0CF54B48F53DC708A4516337878F64F62D"
    $actualHash = (Get-FileHash -Path "d:/txt/example.txt" -Algorithm SHA256).Hash

    if ($actualHash -eq $expectedHash) {
        Write-Host "Checksum matches! File is intact." -ForegroundColor Green
    } else {
        Write-Host "Checksum MISMATCH! File may be corrupted." -ForegroundColor Red
        Write-Host "Expected: $expectedHash" -ForegroundColor Yellow
        Write-Host "Actual:   $actualHash" -ForegroundColor Yellow
    }
    ;;;;
    %slc_psend;

    /**************************************************************************************************************************/
    /* Altair SLC                                                                                                             */
    /* Checksum matches! File is intact.                                                                                      */
    /**************************************************************************************************************************/

    /*          _ _     _       _         _
    __   ____ _| (_) __| | __ _| |_ ___  | | ___   __ _
    \ \ / / _` | | |/ _` |/ _` | __/ _ \ | |/ _ \ / _` |
     \ V / (_| | | | (_| | (_| | ||  __/ | | (_) | (_| |
      \_/ \__,_|_|_|\__,_|\__,_|\__\___| |_|\___/ \__, |
                                                  |___/
    */

    1                                          Altair SLC        17:23 Thursday, April 23, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: AUTOEXEC source line
    1       +  ï»¿ods _all_ close;

    NOTE: AUTOEXEC processing completed

    1         %slc_psbegin;
    2         cards4;

    NOTE: The file 'c:\temp\ps_pgm.ps1' is:
          Filename='c:\temp\ps_pgm.ps1',
          Owner Name=SLC\suzie,
          File size (bytes)=0,
          Create Time=14:40:04 Mar 21 2026,
          Last Accessed=17:23:30 Apr 23 2026,
          Last Modified=17:23:30 Apr 23 2026,
          Lrecl=32767, Recfm=V

    NOTE: 10 records were written to file 'c:\temp\ps_pgm.ps1'
          The minimum record length was 80
          The maximum record length was 82
    NOTE: The data step took :
          real time : 0.007
          cpu time  : 0.000


    3         $expectedHash = "DF85E0E8C4A714CB053862F60A2F0B0CF54B48F53DC708A4516337878F64F62D"
    4         $actualHash = (Get-FileHash -Path "d:/txt/example.txt" -Algorithm SHA256).Hash
    5
    6         if ($actualHash -eq $expectedHash) {
    7             Write-Host "Checksum matches! File is intact." -ForegroundColor Green
    8         } else {
    9             Write-Host "Checksum MISMATCH! File may be corrupted." -ForegroundColor Red
    10            Write-Host "Expected: $expectedHash" -ForegroundColor Yellow
    11            Write-Host "Actual:   $actualHash" -ForegroundColor Yellow
    12        }
    13        ;;;;
    14        %slc_psend;

    NOTE: The infile rut is:
          Unnamed Pipe Access Device,
          Process=powershell.exe -executionpolicy bypass -file c:/temp/ps_pgm.ps1 >  c:/temp/ps_pgm.log,
          Lrecl=32756, Recfm=V

    NOTE: No records were written to file PRINT

    NOTE: No records were read from file rut
    NOTE: The data step took :
          real time : 0.629
          cpu time  : 0.000

    NOTE: The infile rut is:
          Unnamed Pipe Access Device,
          Process=powershell.exe -executionpolicy bypass -file c:/temp/ps_pgm.ps1 >  c:/temp/ps_pgm.log,
          Lrecl=32767, Recfm=V

    NOTE: No records were written to file PRINT

    NOTE: No records were read from file rut
    NOTE: The data step took :
          real time : 0.570
          cpu time  : 0.000

    NOTE: The infile 'c:\temp\ps_pgm.log' is:
          Filename='c:\temp\ps_pgm.log',
          Owner Name=SLC\suzie,
          File size (bytes)=34,
          Create Time=10:30:46 Mar 22 2026,
          Last Accessed=17:23:31 Apr 23 2026,
          Last Modified=17:23:31 Apr 23 2026,
          Lrecl=32767, Recfm=V

    Checksum matches! File is intact.
    NOTE: 1 record was read from file 'c:\temp\ps_pgm.log'
          The minimum record length was 33
          The maximum record length was 33
    NOTE: 1 record was written to file PRINT

    NOTE: The data step took :
          real time : 0.015
          cpu time  : 0.000


    15
    ERROR: Error printed on page 1

    NOTE: Submitted statements took :
          real time : 1.364
          cpu time  : 0.093
    /*  _         _                       _
    | || |     __| |_ __ ___  _ __     __| | _____      ___ __   _ __ ___   __ _  ___ _ __ ___  ___
    | || |_   / _` | `__/ _ \| `_ \   / _` |/ _ \ \ /\ / / `_ \ | `_ ` _ \ / _` |/ __| `__/ _ \/ __|
    |__   _| | (_| | | | (_) | |_) | | (_| | (_) \ V  V /| | | || | | | | | (_| | (__| | | (_) \__ \
       |_|    \__,_|_|  \___/| .__/   \__,_|\___/ \_/\_/ |_| |_||_| |_| |_|\__,_|\___|_|  \___/|___/
                             |_|
    /*--- also in https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories ---*/

    %macro slc_psbegin;
    %utlfkil(c:/temp/ps_pgm.ps1);
    %utlfkil(c:/temp/ps_pgm.log);
    data _null_;
      file "c:/temp/ps_pgm.ps1";
      input;
      put _infile_;
    %mend slc_psbegin;


    https://support.industry.siemens.com/cs/document/109806390/ruggedcom-rox-ii-hash-checksums-?dti=0&lc=en-US
    %macro slc_psend(returnvar=N);
    options noxwait noxsync;
    filename rut pipe  "powershell.exe -executionpolicy bypass -file c:/temp/ps_pgm.ps1 >  c:/temp/ps_pgm.log";
    run;quit;
      data _null_;
        file print;
        infile rut recfm=v lrecl=32756;
        input;
        put _infile_;
        putlog _infile_;
      run;
      * use the clipboard to create macro variable;
      %if %upcase(%substr(&returnVar.,1,1)) ne N %then %do;
        filename clp clipbrd ;
        data _null_;
         length txt $200;
         infile clp;
         input;
         putlog "macro variable &returnVar = " _infile_;
         call symputx("&returnVar.",_infile_,"G");
        run;quit;
      %end;
    data _null_;
      file print;
      infile rut;
      input;
      put _infile_;
      putlog _infile_;
    run;quit;
    data _null_;
      infile "c:/temp/ps_pgm.log";
      input;
      putlog _infile_;
      file print;
      put _infile_;
    run;quit;
    %mend slc_psend;


    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
