            ===================================================
	              Running Deskera applications
            ===================================================

It requires the Java Standard Edition Runtime
Environment (JRE) version 6.0 or later.

=============================
Running With JRE 6.0 Or Later
=============================

(1) Download and Install the Java SE Runtime Environment (JRE)

(1.1) Download the Java SE Runtime Environment (JRE),
      release version 6.0 or later, from
      http://www.oracle.com/technetwork/java/javase/downloads/index.html

(1.2) Install the JRE according to the instructions included with the
      release.

      You may also use the full JDK rather than just the JRE. In this
      case set you have to configure your environment variables
      differently - see below.

(2) Configure Environment Variables

Tomcat itself is a Java application and does not use environment variables,
but the startup scripts use them to prepare the command that starts Tomcat.
The full list of supported environment variables is provided as a comment
at the top of catalina.bat (Windows) and catalina.sh (Unix) files.

(2.1) CATALINA_HOME and CATALINA_BASE

The CATALINA_HOME and CATALINA_BASE environment variables are used to
specify location of Tomcat itself and of its active configuration
respectively.

The CATALINA_HOME environment variable should be set as defined in (2.2)
above. The startup scripts have some logic to set this variable
automatically if it is absent (based on the location of the script in
Unixes and on the current directory in Windows), but it might be not
perfect.

The CATALINA_BASE environment variable is optional and is further described
in "Multiple Tomcat Instances" section below. If it is not set it defaults
to be equal to CATALINA_HOME.

(2.2) JRE_HOME and other variables

The third and the last environment variable that is needed to start Tomcat
specifies location of JRE or JDK that should be used to start Tomcat.

There are two different names of this variable, depending on whether JRE or
JDK is used. Use the JRE_HOME variable to specify location of a JRE and
JAVA_HOME variable to specify location of a JDK.

All variables except CATALINA_HOME and CATALINA_BASE can be configured in a
setenv.bat (Windows) or setenv.sh (Unix) file. The setenv file can be either
in CATALINA_BASE/bin or in CATALINA_HOME/bin. If both are present, only the
one in CATALINA_BASE is used.

So, either set JRE_HOME variable by yourselves or create the file. For
example,

On Windows, %CATALINA_BASE%\bin\setenv.bat:

  set "JRE_HOME=%ProgramFiles%\Java\jre6"
  exit /b 0

On Unix, $CATALINA_BASE/bin/setenv.sh:

  JRE_HOME=/usr/java/latest


(3) Start Up Server

(3.1) Server can be started by executing one of the following commands:

      %CATALINA_HOME%\bin\startup.bat         (Windows)

      $CATALINA_HOME/bin/startup.sh           (Unix)

   or

      %CATALINA_HOME%\bin\catalina.bat start  (Windows)

      $CATALINA_HOME/bin/catalina.sh start    (Unix)

(3.2) After startup, Deskera HRMS will be available by visiting:

      http://localhost:7070/hrms/a/hrms/login.html
     
      You can use the following credentials to login 
      username: admin
      password: welcome

(4) Shut Down Server

(4.1) Server can be shut down by executing one of the following commands:

      %CATALINA_HOME%\bin\shutdown.bat       (Windows)

      $CATALINA_HOME/bin/shutdown.sh         (Unix)

   or

      %CATALINA_HOME%\bin\catalina.bat stop  (Windows)

      $CATALINA_HOME/bin/catalina.sh stop    (Unix)

================
Troubleshooting
================

There are only really 3 things likely to go wrong during the stand-alone install:

(1) The most common hiccup is when another web server (or any process for that
    matter) has laid claim to port 7070.  This is the default HTTP port that
    Tomcat attempts to bind to at startup.  To change this, open the file:

       $CATALINA_HOME/conf/server.xml

    and search for '7070'.  Change it to a port that isn't in use, and is
    greater than 1024, as ports less than or equal to 1024 require superuser
    access to bind under UNIX.

    Restart server and you're in business.  Be sure that you replace the "7070"
    in the URL you're using to access the server.  For example, if you change the
    port to 1977, you would request the URL http://localhost:1977/ in your browser.

(2) An "out of environment space" error when running the batch files in
    Windows 95, 98, or ME operating systems.

    Right-click on the STARTUP.BAT and SHUTDOWN.BAT files.  Click on
    "Properties", then on the "Memory" tab.  For the "Initial environment" field,
    enter in something like 4096.

    After you click apply, Windows will create shortcuts which you can use
    to start and stop the container.

(3) The 'localhost' machine isn't found.  This could happen if you're behind a
    proxy.  If that's the case, make sure the proxy configuration for your
    browser knows that you shouldn't be going through the proxy to access the
    "localhost".

    In Firefox, this is under Tools/Preferences -> Advanced/Network ->
    Connection -> Settings..., and in Internet Explorer it is Tools ->
    Internet Options -> Connections -> LAN Settings.
