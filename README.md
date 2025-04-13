# CBT639
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. GitHub repos will be deleted and created during this period...

```
//***FILE 639 Set System Clock for Time Saving - Hunter Zhou        *   FILE 639
//*                                                                 *   FILE 639
//*           The package SETHOUR is from Hunter Zhou.              *   FILE 639
//*                                                                 *   FILE 639
//*           Hunter Guanghui Zhou                                  *   FILE 639
//*           Phone: 1-(416)-602-9567                               *   FILE 639
//*           E-mail: zhough2000@yahoo.com                          *   FILE 639
//*                                                                 *   FILE 639
//*           The package SETHOUR is used to change the system      *   FILE 639
//*           TOD clock for time saving automatically. The software *   FILE 639
//*           will also update the TIMEZONE statement in current    *   FILE 639
//*           active CLOCKxx member to reflect the new timezone.    *   FILE 639
//*                                                                 *   FILE 639
//*       Program: SETHOUR (HLASM)                                  *   FILE 639
//*       Purpose: Update System Clock and TIMEZONE in CLOCKxx.     *   FILE 639
//*       Parameter:                                                *   FILE 639
//*         1. +1|-1                                                *   FILE 639
//*            Tell program to set clock one hour ahead or back.    *   FILE 639
//*                                                                 *   FILE 639
//*         2. FALL|AUTUMN|WINTER                                   *   FILE 639
//*            Tell program to change clock in fall.                *   FILE 639
//*                                                                 *   FILE 639
//*         3. SPRING|SUMMER                                        *   FILE 639
//*            Tell program to change clock in spring.              *   FILE 639
//*                                                                 *   FILE 639
//*         3. AUTO                                                 *   FILE 639
//*            Tell program to change the TOD clock according to    *   FILE 639
//*            the current month when the program is run:           *   FILE 639
//*            . If current month is between Janurary to June       *   FILE 639
//*              this parm is the same as SPRING.                   *   FILE 639
//*            . Otherwise it is the same as FALL.                  *   FILE 639
//*                                                                 *   FILE 639
//*        The program will issue MVS SET CLOCK command to set the  *   FILE 639
//*        system clock, the date may be also changed according to  *   FILE 639
//*        the time it is run.                                      *   FILE 639
//*                                                                 *   FILE 639
//*        The program will locate the active CLOCKxx member,       *   FILE 639
//*        and update the TIMEZONE statement to reflect the updated *   FILE 639
//*        clock, so that the clock change will be kept after next  *   FILE 639
//*        IPL.                                                     *   FILE 639
//*                                                                 *   FILE 639
//*        Some permissions from the security system may have to    *   FILE 639
//*        be set, for the SETHOUR proc to run.  For notes about    *   FILE 639
//*        RACF, please see member $$RACF from Sam Golob.  Sample   *   FILE 639
//*        procs SETHOUR, SETFALL, SETSPRNG are in member $$PROCS.  *   FILE 639
//*                                                                 *   FILE 639
//*        There are some software are time sensitive, especially   *   FILE 639
//*        set the clock back. In order to make the TOD clock       *   FILE 639
//*        change automatically, you may use the operation          *   FILE 639
//*        package to restart the software and update the clock,    *   FILE 639
//*        such as File #623. Here is example to use this           *   FILE 639
//*        package:                                                 *   FILE 639
//*                                                                 *   FILE 639
//*        //********************************************           *   FILE 639
//*        //* Stop CLOCK sensitive software                        *   FILE 639
//*        //STOPSW   EXEC PGM=IKJEFT01,PARM=AUTOIPL                *   FILE 639
//*        //STEPLIB  DD   DISP=SHR,DSN=SYS1.USER.LINKLIB           *   FILE 639
//*        //SYSEXEC  DD   DISP=SHR,DSN=SYS1.USER.REXXLIB           *   FILE 639
//*        //SYSTSPRT DD   SYSOUT=*                                 *   FILE 639
//*        //SYSTSIN  DD   DUMMY                                    *   FILE 639
//*        //SYSIN    DD   *                                        *   FILE 639
//*          WTOH('STOP SOFTWARE FOR TIME CHANGE')                  *   FILE 639
//*          P RMF                                                  *   FILE 639
//*          P TMONMVS                                              *   FILE 639
//*          P TMVSLFS                                              *   FILE 639
//*          WAIT                                                   *   FILE 639
//*          P TMVSMSTR                                             *   FILE 639
//*          P TMVSHUB                                              *   FILE 639
//*        /*                                                       *   FILE 639
//*        //********************************************           *   FILE 639
//*        //* Change TOD clock and CLOCKxx member                  *   FILE 639
//*        //SETCLK   EXEC PGM=SETHOUR,PARM=AUTO                    *   FILE 639
//*        //SYSPRINT DD   SYSOUT=*                                 *   FILE 639
//*        //* Wait 1 hour in case of set clock back.               *   FILE 639
//*        //WAIT     EXEC PGM=WAIT,PARM=3600     3600 seconds      *   FILE 639
//*        //*********************************************          *   FILE 639
//*        //* Start CLOCK sensitive software                       *   FILE 639
//*        //STARTALL EXEC PGM=IKJEFT01,PARM=AUTOIPL                *   FILE 639
//*        //STEPLIB  DD   DISP=SHR,DSN=SYS1.USER.LINKLIB           *   FILE 639
//*        //SYSEXEC  DD   DISP=SHR,DSN=SYS1.USER.REXXLIB           *   FILE 639
//*        //SYSTSPRT DD   SYSOUT=*                                 *   FILE 639
//*        //SYSTSIN  DD   DUMMY                                    *   FILE 639
//*        //SYSIN    DD   *                                        *   FILE 639
//*          WTOH('START SOFTWARE FOR TIME CHANGE')                 *   FILE 639
//*          S TMVSHUB                                              *   FILE 639
//*          S TMVSMSTR                                             *   FILE 639
//*          S RMF                                                  *   FILE 639
//*          WTOH('TIME SAVING CHANGE IS COMPLETED')                *   FILE 639
//*        //*                                                      *   FILE 639
//*                                                                 *   FILE 639
```
