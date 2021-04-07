
                                  Bestdam Logger
            Copyright 1999-2001, Keith Parkansky  All rights reserved.

                           http://www.execpc.com/~keithp/


NOTE:  This document provides a brief overview of the features
       and requirements of Bestdam Logger as well as installation
       instructions.  If you are unfamilier with using CGI scripts,
       a discussion on using the CGI capabilities of your site to
       to run scripts is available at the URL above.

This document has the following sections:

                             Overview
                             Setup & Installation
                             Troubleshooting
                             Optional Variables
                             Upgrading To The Deluxe Edition
                             Software License Agreement


In addition to this document, there are eb pages available which
will feature more up-to-date information.

Step-by-step instructions on setting up and using CGI scripts,
including screen-shots of how to use the WS_FTP program to 
transfer files and set permissions, is available at:

              http://www.execpc.com/~keithp/bdlogcgi.htm

The Web page version of the installation instructions given below
is available at:

              http://www.execpc.com/~keithp/bdlogsu.htm

There is also a Quick Setup page for experienced CGI script users
at:
              http://www.execpc.com/~keithp/bdlogqs.htm

Troubleshooting information, tips, and tools are available at:

              http://www.execpc.com/~keithp/bdloghlp.htm

The Bestdam Logger home page is at:

              http://www.execpc.com/~keithp/bdlogger.htm


###############################################################

Overview
--------

Bestdam Logger is a CGI script written in Perl.  It was tested
with a Perl 5 interpreter but I made an effort to only used commands
that were also supported by Perl 4.  However, it was not tested
with a Perl 4 interpreter.  It requires SSI (Server Side Includes) 
to execute.  It has been tested on Unix and Windows NT systems.  
While it may very well work on Macintosh servers, it has not been 
tested on one.

Bestdam Logger is a combination hit counter script and logging
script.  It has two log files.  A "period.log" and a "history.log".
The period log cotains the log data for the period (day, week or
month) between report e-mailings.  It also has a "pagehits.cnt"
file tracking the number of hits to one or more pages.  E-mailed
reports contain the contents of this hit count file and, with the
Deluxe Edition, the contents of the period log.  Also in the
Deluxe Edition, there is an option to have this "period.log" data
appended to the "history.log" file before it is cleared.

It compiles counts and detailed information about visitors to your 
Website including:
                    - their IP address
                    - their host domain (ISP)
                    - the make and version of the browser they used
                    - the operating system they are using
                    - the pages they viewed
                    - the URL of the site that referred them to yours
                    - the date and time of their visit

all in an easy-to-read columnar format.  The log file layout is as
follows:

Date &   Page        ISP        IP Addr     Browser/OS   Referring
Time    Visited   of Visitor   of Visitor   of Visitor      Site *

  * Deluxe Edition only

In order to maintain the columnar format, some values may get
truncated, but the less important information is what gets
truncated.  For instance, with the ISP information, the node
the visitor was on may get truncated, not the domain name of
the ISP.  The Referring Site information is in the last column
so it will not be truncated.  This allows you to check the
search keys visitors used to find your site if the referring
site was a search engine.


Features include:
                    - "period" log reports, with count summaries, 
                       can be automatically e-mailed to you daily 
                       or weekly (or not at all)

                    - if you choose the "Weekly" option you pick
                      the day of the week they are sent

                    - an optional "history" log can be kept, a
                      culmination of the daily or weekly "period" 
                      logs

                    - you decide which pages to include/exclude in
                      the logging and counting by including a single
                      SSI directive HTML tag in your page(s)

                    - the counter can be "hidden" or displayed on
                      the page(s)

                    - the counter can either be displayed as text or 
                      you can use graphics digits of your choice

                    New in Version 2.0

                    - adjustable IP tracking for more accurate hit counts 
                      and reduced "counter bloat"

                    - optional IP blocking to prevent individual IPs, 
                      or entire sub-nets, from being counted/logged

                    - optional hit statistics Web page to view counts 
                      using a browser

                    - optional creation of a Web page-version of the 
                      daily or weekly "period" logs

                    - support for the Blat freeware NT mail program

                    - improved log layout with more sophisticated 
                      truncating

                    New in Version 3.0

                    - a "hit history" file which records hits for
                      recurring selectable periods (day/week/month)
                      with percentage increases/decreases from one
                      period to the next

                      The above file is saved in a tab-delimited 
                      ASCII .txt file so that it can be imported
                      into a spreadsheet program for analysis,
                      graphing, reporting, and presentation.

                      The selectable periods for the "hit history"
                      file are independent of the selectable periods
                      for the log processing.

                    - the optional creation of a Web page version of
                      the above hit history file

                    - auto-detection of the server operating system
                      (Unix/Linux or NT/2K) for easier setup

                    - the option of having the above file information
                      included in the e-mailed period report

                    - the addition of a "monthly" selection for period
                      processing of log files and e-mail reports

                    - the option of NOT having the period log file
                      data included in the e-mailed reports

                    - improved file locking for more stable count and
                      log files

                    - a fix for leap-year dates on e-mailed reports

                    - improved support for the Blat mail program


Two editions of Bestdam Logger are available.  Due to the wide 
variety of server configurations out there, it is recommended
that you try the free Lite Edition first.  If it works with
your configuration and you like the benefits it provides,
please consider upgrading to the Deluxe Edition.

   The Deluxe version includes all of the features mentioned above 
   for only $20.

   The Lite version is FREE and has the following limitations:

     - only hit stats (no log information) are automatically 
       e-mailed and only on a daily basis

     - the counters can be displayed but only in text mode

     - the counters cannot be auto-reset

     - the IP tracking/blocking features are not available

     - the creation of the optional Web pages is not available

     - the hit history function is not available

     - the history log function is not available


Information on ordering the upgrade is available at the
Bestdam Logger home page, the URL for which is given near
the top of this document.


###############################################################

Setup & Installation
--------------------

        NOTE:  Before you begin the installation process,

               A. Make sure you have CGI capabilites !

                    If you have a CGI-BIN folder under your 
                    root Web directory, chances are you do.

                    If you don't, contact your host or ISP
                    and ask them to set it up for you.  It
                    is not a folder that you can set up
                    correctly yourself.
                  
               B. Make sure your CGI capability includes
                  support for SSI (Server Side Includes).
                  Most do, but if you are not sure check
                  with your host or ISP.  The script will
                  NOT execute without SSI.


Note: You may receive a blank e-mail report shortly after 
      installing the script.  This is caused by the "trigger"
      file being reset to the current date.


1. Use a text editor to open the BDLOGGER.PL file


2. The very first line of the file is the path to you're host's
   installation of Perl.  Verify that this path is correct or
   change it if necessary.  If you are not sure of the location
   of your host's Perl installation ask them to provide you with
   the path to it.  Another common location is:
                         #!/usr/bin/perl


3. Around line 60 of the BDLOGGER.PL file is where the list of
   user-specific variables begins.  This list has the heading:

         "YOU ***MUST*** SET THE FIRST  2  VARIABLES !"

   As the heading indicates, the first two variables, which are
   $send_to  and  $mailprgm  must have the correct values entered
   for them.  The remaining variables are for user customization
   but the program will work fine with the default values.  The
   two variables you need to primarily be concerned with are:

   $send_to     Enter, between the quote marks, the e-mail 
                address of the person who is to receive the 
                e-mailed reports.  Be careful not to over-write 
                the quote marks.  The e-mail address must be 
                enclosed in these quote marks as given in the 
                example near the  variable list heading.

   $mail_prgm   This is the path to your host's server-based
                e-mail program.  Verify that this path is 
                correct or change it if necessary.  If you are 
                not sure of the location of your host's e-mail
                installation ask them to provide you with the 
                name and path to it.  Another common location is:
                           '/bin/sendmail'

                As with the $send_to variable, this variable must
                be enclosed in the quote marks.

                For NT Users
                ------------
                If you are using the freeware Blat program, enter
                BLAT (in upper case) in the  $mail_prgm  variable
                and then enter the path to your Blat installation
                in the  $blat_path  variable.  The default value
                of this variable is the default installation path
                of the Blat program.

For a detailed discussion of the optional variables, please see
the "Optional Variables" section below.


4. Add the following SSI directive tag to each Web page that you 
   want to "monitor", i.e. log and count hits.

            <!--#exec cgi="/cgi-bin/bdlogger/bdlogger.pl" -->

   If your CGI-BIN folder is called something other than CGI-BIN,
   modify the folder name in the tag accordingly.

   Notes On Tag Placement

   It is best to put the tag near the bottom of the page, but
   be sure to put it BEFORE the </body> tag.  Putting it near
   the bottom of the page will help ensure that the first part
   of your page is not delayed in loading.  The first person
   of a new "period" to view one of your monitored pages may
   notice a delay in the complete loading of the first monitored
   page as the "period process" executes.  However, any server
   with reasonable power should process the script very quickly.
   In addition, the first hit of the day is likely to be early
   in the morning when server loads are low.

   If you have the $display_count variable (see below) set to 
   "Yes" (1), the placement of the tag will dictate where the 
   counter appears on your page.  The counter location will 
   also be influenced by any formatting tags, such as <center>
   that you have on your page.

   In addition, if you have the $graphics_count variable (see
   below) variable set to "No" (0), the count will be displayed
   one the page as text and will be influenced by formatting
   tags such as <font>, <b>, etc.


5. Use an FTP program such as WS-FTP or Cute FTP to access your
   Web directory on the server.

   Go to the CGI-BIN directory (i.e. open the CGI-BIN folder).

   Make a new directory (folder) under CGI-BIN with the name
   of bdlogger

   USE  ASCII  MODE !!!  to transfer all 5 of the following files
   to your new bdlogger directory:

                  bdlogger.pl
                  period.log
                  trigger.dat
                  pagehits.cnt
                  iptrack.num     (if Deluxe Edition)
                  history.log     (if Deluxe Edition)
                  hithistory.txt  (if Deluxe Edition)

   NOTE: If you are using any version of Windows, the file names
         may have been changed so that the first letter of the
         file names is upper-case.  Make sure the file names are
         all lower-case letters once they are on the server.  If
         they are not, use the "Rename" function of your FTP 
         program to change the file names to all lower-case letters.
                 

6. On a Unix server, CHMOD the files as follows:           

                  bdlogger.pl     755
                  period.log      666
                  trigger.dat     666
                  pagehits.cnt    666
                  iptrack.num     666      (if Deluxe Edition)
                  history.log     666      (if Deluxe Edition)
                  hithistory.txt  666      (if Deluxe Edition)


   If you are unfamilier with CHMOD, it is used to set who
   has what permissions to the files.  Using WS-FTP as an
   example, you can CHMOD a file by:

     - clicking once on the file name
     - right-clicking on the file name and selecting CHMOD
       from the drop down menu
     - set the 666 permissions by selecting the following
       in the three columns:

          Under "Owner" - select "Write" and "Read"
          Under "User"  - select "Write" and "Read"
          Under "Other" - select "Write" and "Read"

       repeat this for the other three files to be set to 666

     - set the 755 permissions to the bdlogger.pl file by
       selecting the following in the three columns:

          Under "Owner" - select "Write", "Read", and "Execute"
          Under "User"  - select "Read" and "Execute"
          Under "Other" - select "Read" and "Execute"
                 
     - click on the "Refresh" button to the right of the server
       file display

     - click on the "DirInfo" button to the right of the server
       file display and you should have the following:

               rwxr-xr-x        bdlogger.pl
               rw-rw-rw-        history.log
               rw-rw-rw-        pagehits.cnt
               rw-rw-rw-        period.log
               rw-rw-rw-        trigger.dat
               rw-rw-rw-        iptrack.num     (if Deluxe Edition)
               rw-rw-rw-        history.log     (if Deluxe Edition)
               rw-rw-rw-        hithistory.txt  (if Deluxe Edition)



7. Go up one level to the CGI-BIN folder, and then up one more
   level again to go back to your root Web directory.

   Transfer those Web pages to which you added the SSI directive
   tag from your local drive to the server.


8. If you are going to be using graphics digits for the 
   hit counter function, make a new directory (folder) under
   your root Web directory and name it  digits

   USE  BINARY  MODE !!!  to transfer the graphics files to
   your new digits directory.

   NOTES: The graphics files must have the single character
          name for the number they represent.  For example,
          if they are .gif files, they must be named:
          1.gif  2.gif  3.gif  etc.  Use the "Rename" function
          of your FTP program to rename them if necessary.

          Be sure to update the relevant optional variables 
          in the BDLOGGER.PL file also.

          Do NOT create the digits directory under the
          CGI-BIN directory or people may not be able to
          access them there.



INSTALLATION  COMPLETE  !!!


Look at your Web pages in your browser to make sure the counter
(if you selected to have it displayed) is in the position and
format that you wanted.
 

###############################################################

Troubleshooting
---------------

If you have problems getting your script to work please go 
to the Setup & Installation Web page and click on the 
"Troubleshooting" link near the top of the page.  This page 
will have the most up-to-date information because I will add 
to it if a user reports a problem/solution with a not-so-common 
server operating system or Web-server software package.

The URL for the Setup & Installation page is:

          http://www.execpc.com/~keithp/bdlogsu.htm

The URL for the Troubleshooting page is:

          http://www.execpc.com/~keithp/bdloghlp.htm

###############################################################

Optional Variables
------------------

   The following variables can be set optionally.  They are used to
   customize the performance to your preferences.


   $reporting_period  The period between the updating of the logs
                      and the mailing of the report.  Values are:
                      0 = Not-at-all
                      1 = Daily
                      2 = Weekly
                      3 = Monthly

                      NOTE:  With this value set to '0' (not at all)
                             Bestdam Logger will perform like your
                             run-of-the-mill logger/counter.

                      "Updating of the logs" means the "period log"
                      is cleared and if the $keep_history variable
                      (see below) is set to "Yes", the contents of
                      the period log are appended to the history
                      log before the period log is cleared.
                      1 is the default value.
                      1 ("Daily") is the only valid value for this
                      setting with the Lite Edition.

                      CAUTION !!!   Choosing 3 (Monthly) could result
                                    in very big period log files by the
                                    last week of the month which could
                                    slow the execution of the script.
                                    It should only be used if you get
                                    less than several hundred hits a
                                    week or have a very fast server.



   $day_of_week       If you chose "Weekly" (2) for the above 
                      variable, this variable sets which day of the
                      week the logs will be updated and the report
                      will be e-mailed.  Values are:

                      0 = Sunday        1 = Monday     2 = Tuesday
                      3 = Wednesday     4 = Thursday
                      5 = Friday        6 = Saturday

                      The logs are updated and report e-mailed when
                      one of your pages being monitored receives the
                      first hit of the day you specify (probably very 
                      early a.m.).
                      0 is the default value.
                      This variable in non-applicable to the Lite
                      Edition.


   $mail_report       E-mail the "period" log report & stats ?  
                      Values are     1 = Yes      0 = No
                      1 is the default value.


   $log_in_mail       Include the period log in the e-mailed report ?
                      Values are     1 = Yes      0 = No
                      1 is the default value
                      This variable in non-applicable to the Lite
                      Edition.


   $double_space      The log lines can be very long.  The log data
                      that is e-mailed is best viewed with the "wrap"
                      feature turned off in your e-mail program.  If
                      you can't turn off "wrap", or just don't want
                      to, this option will double-space the log lines
                      in the mail report.
                      Values are     1 = Yes      0 = No
                      You must have  $mail_report = 1  and
                       $log_in_mail = 1 
                      0 is the default value.
                      This variable in non-applicable to the Lite
                      Edition.


   $keep_history      Keep a cummulative "history log" ?  
                      Values are     1 = Yes      0 = No
                      1 is the default value.
                      This variable in non-applicable to the Lite
                      Edition.


   $count_hits        Count page hits ?
                      Values are     1 = Yes      0 = No
                      1 is the default value.


   $hit_count_history Keep a history of hit counts for a recurring
                      period to tab-delimited text file for viewing
                      and optional import into into a spreadsheet 
                      program for analysis and graphing ?  Values
                      are:
                      0 = Not-at-all
                      1 = Daily
                      2 = Weekly
                      3 = Monthly
                      If set to 1, 2, or 3, the  $count_hits  variable
                      must be set to 1.
                      0 is the default value.
                      This variable in non-applicable to the Lite
                      Edition.


   $hit_count_history_dow   If you chose "Weekly" (2) for the above 
                            variable, this variable sets which day of
                            the week the current count will be added
                            to the hit history log file.  Values are:

                      0 = Sunday        1 = Monday     2 = Tuesday
                      3 = Wednesday     4 = Thursday
                      5 = Friday        6 = Saturday

                      The log entry is made when one of the pages being
                      monitored receives the first hit of the day you 
                      specify (probably very early a.m.).
                      0 is the default value.
                      This variable in non-applicable to the Lite
                      Edition.


   $hit_count_history_page   If you are counting hits on multiple pages
                             you must specify which of the pages to keep
                             the history on.  History can be kept on only
                             one page.  This should be your site's home
                             page.
                             index.html is the default value.
                             This variable in non-applicable to the Lite
                             Edition.


   $hit_count_history_in_mail    The hit count history file can be
                                 included in the period report that
                                 is e-mailed.
                                 0 is the default value.
                                 This variable in non-applicable to
                                 the Lite Edition.


   $check_ip          Check IP address so multiple hits from 
                      the same address aren't counted  ?
                      Values are     1=Yes         0=No
                      1 is the default value
                      DON'T set to '1' if you are monitoring 
                      mutliple pages.

                      The default level of "back tracking" is 
                      5 addresses. To lower this, open the 
                      'iptrack.num' file in a text editor and 
                      delete the appropriate number of '0.0.0.0' 
                      IP addresses.  To increase it, add the 
                      appropriate number of '0.0.0.0' IP addresses 
                      with each being on their own line.
                      This variable in non-applicable to the Lite
                      Edition.


   $reset_counts      You have the option of resetting the 
                      hit counters to zero after the report 
                      is e-mailed.
                      Values are     1 = Yes      0 = No
                      0 is the default value.
                      You must have  $count_hits = 1
                      This variable in non-applicable to the Lite
                      Edition.


   $display_count     Display the counter on the page ?
                      Values are     1 = Yes      0 = No
                      1 is the default value.
                      You must have  $count_hits = 1
                      This variable in non-applicable to the Lite
                      Edition.


   $graphics_count    Use graphics digits for counter ?
                      Values are     1 = Yes      0 = No
                      0 is the default value.
                      You must have  $display_count = 1
                      This variable in non-applicable to the Lite
                      Edition.

      NOTE:  If you set  $graphics_count = 1  you MUST verify/set
             the three additional variables below and follow the
             "Special Notes" below. 

             The following two variables have example values
             which are the default values.


$digits_path = '/digits/';            Specify the path to the digits
                                      files relative to the root URL.
                                      This value MUST begin AND end 
                                      with a slash (/).

                                      Ex: Your root URL could be
                                      something like:
                                       http://www.yourdomain.com
                                      or
                                       http://www.isp.com/~mydomain


$digits_type = '.gif';                File extension of digit graphics
                                      files.  The period MUST be 
                                      included.

                           
SPECIAL NOTES:   If necessary - rename digit files to 1. 2. 3. etc.
                 Example for .gif files:  1.gif  2.gif  3.gif  etc.

                 A large selection of digit graphics files are
                 available at www.digitmania.holowww.com

                 Don't put the digits under the CGI-BIN folder.
                 People may not be able access them there

                 With the above 2 values set correctly you should 
                 be able to view the digits on your browser.  
                 Using the above default values as an example, 
                 you'd be able to see the '1' digit by going to  

                    http://www.yourdomain.com/digits/1.gif

                 If you can't see the digits this way, no one will
                 be able to see them on your Web page.



   $web_count         Create the hits.htm Web page to view 
                      current hit counts using a browser ?
                      Values are      1 = Yes        0 = No
                      0 is the default value.
                      You must have  $count_hits = 1
                      View the page at http://www.mydomain.com/hits.htm
                      This variable in non-applicable to the Lite
                      Edition.

                      NOTE: If you set this value to '1' you MUST enter 
                            the value for the next variable.


   $count_path        If you entered '1' to create a hits.htm page 
                      you MUST enter the SYSTEM path to your Web root 
                      for the hits.htm file (typically where your home 
                      page is located).

                      The value here is just an example of what's needed. 
                      Be sure to leave the   '/   at the beginning and 
                      the   /hits.htm';   on the end.

                      If you wish, you can use a name other than 'hits' 
                      for the page.

        $page_path = '/usr/local/etc/httpd/usersites/mysite/hits.htm';

                      This variable in non-applicable to the Lite
                      Edition.


   $web_report        Create a Web-page version of the period report 
                      (which also contains the hit count data) to view 
                      using a browser ?    (preport.htm)
                      Values are       1 = Yes        0 = No
                      0 is the default value.
                      View the page at http://www.mydomain.com/preport.htm
                      This variable in non-applicable to the Lite
                      Edition.

                      NOTE: If you set this value to '1' you MUST enter 
                            the value for the next variable.


   $report_path       If you entered '1' to create a preport.htm page 
                      you MUST enter the SYSTEM path to your Web root 
                      for the preport.htm file (typically where your 
                      home page is located).

                      The value here is just an example of what's needed. 
                      Be sure to leave the   '/   at the beginning and 
                      the   /preport.htm';   on the end.

                      If you wish, you can use a name other than 
                      'preport' for the page.

        $page_path = '/usr/local/etc/httpd/usersites/mysite/preports.htm';

                      This variable in non-applicable to the Lite
                      Edition.


   $web_history       Display the hit history table in a Web page to 
                      view using a browser ?    (hithistory.htm)
                      Values are       1 = Yes        0 = No
                      0 is the default value.
                      View page at http://www.mydomain.com/hithistory.htm
                      This variable in non-applicable to the Lite
                      Edition.

                      NOTE: If you set this value to '1' you MUST enter 
                            the value for the next variable.


   $web_history_path  If you entered '1' to create a hithistory.htm page 
                      you MUST enter the SYSTEM path to your Web root 
                      for the hithistory.htm file (typically where your 
                      home page is located).

                      The value here is just an example of what's needed. 
                      Be sure to leave the   '/   at the beginning and 
                      the   /hithistory.htm';   on the end.

                      If you wish, you can use a name other than
                      'hithistory.htm' for the page.

        $page_path = '/usr/local/etc/httpd/usersites/mysite/hithistory.htm';

                      This variable in non-applicable to the Lite
                      Edition.



Using IP Blocking  (Deluxe Edition only)

  If you want to use IP blocking, you must create a text file with 
  the name 'ipblock' (no extension) and transfer it with the other 
  files and CHMOD it 666 also.

  In the file, enter one IP address (or partial IP address for entire 
  sub-net blocking) per line to be blocked from the counting and logging.  
  You can enter as many IP addresses or partial addresses as you like.

  Examples:

      Entering  123.45.678.9  will block this one IP address

      Entering  123.45  will block all IP addresses that start 
      with '123.45'.

  Sample file:

       123.45.678.9
       123.45.678.20
       434.22
       765.43.21



###############################################################

Upgrading To The Deluxe Edition
-------------------------------

Please visit the Bestdam Logger Website at

   http://www.execpc.com/~keith/bdlogger.htm

for details on ordering the Deluxe Edition.

Thank you for your interest !


###############################################################

                         SOFTWARE LICENSE

UPON USE OF THE BESTDAM LOGGER SCRIPT THE INDIVIDUAL OR ENTITY  
(THE "END USER"),  AGREES TO THE TERMS OF, AND TO BE BOUND BY, 
THE TERMS OF THIS LICENSE.  IF THE END USER DOES NOT AGREE WITH 
THE TERMS USE IS TO BE DISCONTINUED IMMEDIATELY.

The enclosed computer files ("Software") and the accompanying 
documentation are provided to the End-User by Keith Parkansky 
("Licensor") for use only under the following terms.  Licensor 
reserves any right not expressly granted to the End-user.  The 
software is protected by United States copyright laws and 
international treaty provisions.  The Licensor retains ownership 
of all copies of the Software.  The End-User assumes sole 
responsibility for the installation, use and results obtained 
from use of the Software.

1.  License.
The End-User is granted a limited, non-exclusive license to do 
only the following:

A.  Install and maintain the Software on one computer at any time 
for use only in the End-User's own home or business.  Provided the 
End-User is the sole user of the Software, the Software may be 
installed on a second computer.

B.  Make one copy in machine-readable form solely for backup or 
archival purposes for the computer which the Software is installed.
The Software is protected by copyright law.  As an express condition 
of this License, the End-User must reproduce on the copy the 
Licensor's copyright notice and any other proprietary legends on the 
original copy supplied by Licensor.

C.  Transfer the Software and all rights under this License to 
another party together with a copy of this License and all written 
materials accompanying the Software, provided (i) the End-User gives 
Licensor written notice of the transfer (including in such notice 
the identity of the transferee), and (ii) the other party reads and 
agrees to accept the terms and conditions of this License.

2.  Restrictions.
The End-User may NOT sublicense, assign, or distribute copies of the 
Software to others, except as provided in the agreement above.  The 
Software contains trade secrets.  THE END-USER MAY NOT MODIFY, ADAPT, 
TRANSLATE, RENT, LEASE, LOAN, RESELL FOR PROFIT, DISTRIBUTE, OR 
OTHERWISE ASSIGN OR TRANSFER THE SOFTWARE, OR CREATE DERIVATIVE WORKS 
BASED UPON THE SOFTWARE OR ANY PART THEREOF, EXCEPT AS EXPRESSLY 
PROVIDED IN SECTION 1 ABOVE.

3.  Protection and Security.
The End-User agrees to use its best efforts and to take all reasonable 
steps to safeguard the Software to ensure that no unauthorized person 
shall have access thereto and that no unauthorized copy, publication, 
disclosure or distribution in whole or in part, in any form, shall be 
made.  The End-User acknowledges that the Software contains valuable 
confidential information and trade secrets and that unauthorized use 
and/or copying are harmful to Licensor.

4.  Termination.
This License is effective until terminated.  This License will 
terminate immediately without notice from Licensor if the End User 
fails to comply with any of its provisions.  Upon termination the 
End User must destroy the Software and all copies thereof, and the 
End-User may terminate this License at any time by doing so.

5.  Limited Warranty.
No oral or written information or advice given by Licensor or its 
dealers, distributors, employees or agents shall in any way extend, 
modify or add to the foregoing warranty.

THE WARRANTY AND REMEDY PROVIDED ABOVE ARE EXCLUSIVE AND IN 
LIEU OF ALL OTHER WARRANTIES, EXPRESS OR IMPLIED, INCLUDING BUT 
NOT LIMITED TO THE IMPLIED WARRANTIES OF MERCHANTABILITY AND 
FITNESS FOR A PARTICULAR PURPOSE.  THE END-USER ASSUMES ALL RISK AS 
TO THE SUITABILITY, QUALITY, AND PERFORMANCE OF THE SOFTWARE.  IN 
NO EVENT WILL LICENSOR, OR EMPLOYEES, OR AFFILIATES, BE LIABLE TO 
THE END-USER FOR ANY CONSEQUENTIAL, INCIDENTAL, INDIRECT, SPECIAL 
OR EXEMPLARY DAMAGES (INCLUDING DAMAGES FOR LOSS OF BUSINESS 
PROFITS, BUSINESS INTERRUPTION, LOSS OF DATA OR BUSINESS 
INFORMATION, AND THE LIKE) ARISING OUT OF THE USE OF OR INABILITY 
TO USE THE SOFTWARE OR ACCOMPANYING WRITTEN MATERIALS, EVEN IF 
LICENSOR HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGES.

LICENSOR'S LIABILITY TO THE END-USER (IF ANY) FOR ACTUAL DIRECT 
DAMAGES FOR ANY CAUSE WHATSOEVER, AND REGARDLESS OF THE FORM 
OF THE ACTION, WILL BE LIMITED TO, AND IN NO EVENT SHALL EXCEED, 
THE AMOUNT ORIGINALLY PAID TO LICENSOR FOR THE LICENSE OF THE 
SOFTWARE.

6.  Enhancements.
From time to time Licensor may, in its sole discretion, advise the 
End-User of updates, upgrades, enhancements or improvements to the 
Software and/or new releases of the Software (collectively, 
"Enhancements"), and may license the End-User to use such
Enhancements upon payment of prices as may be established by Licensor 
from time to time.  All such Enhancements to the Software provided to 
the End-User shall also be governed by the terms of this License.

7.  General.
This License will be governed by and construed in accordance with the 
laws of the State of Wisconsin, and shall inure to the benefit of 
Licensor and End-User and their successors, assigns and legal 
representatives.  If any provision of this License is held by a court 
of competent jurisdiction to be invalid, illegal, or unenforceable to 
any extent under applicable law, that provision will be enforced to the 
maximum extent permissible, and the remaining provisions of this 
License will remain in full force and effect.  

This Agreement constitutes the entire agreement between the parties 
with respect to the subject matter hereof, and all prior proposals, 
agreements, representations, statements and undertakings are hereby 
expressly canceled and superseded.  This Agreement may not be changed 
or amended except by a written instrument executed by a duly authorized 
officer of Licensor.

8.  Acknowledgment.
BY PRECEDING WITH THE INSTALLATION OF THIS SOFTWARE, THE END-USER 
ACKNOWLEDGES THAT THEY HAVE READ THIS LICENSE, UNDERSTAND IT, 
AND AGREE TO BE BOUND BY ITS TERMS AND CONDITIONS.  Should you have 
any questions concerning this License, contact Licensor at the 
address set forth below.

Keith Parkansky
P.O. Box 1264
Milwaukee, WI  53201

Bestdam Logger and the Bestdam Logger graphic logo are trademarks of 
Keith Parkansky.  
