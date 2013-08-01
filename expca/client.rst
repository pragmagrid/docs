.. highlight:: rest
.. include:: expca-rst

.. _client:

CA Cient software installation
==============================

The software is used to request and retrieve user and host certificates.

#. **Prerequisites**

   **Supported platforms**

   + Rocks 4.2, Rocks 6.1 
   + Solaris 2.8 (x86)
   + FreeBSD4.3 (x86) 
   + Turbo Linux6.5 
   + Miracle Linux2.1 
   + RedHat 7.2

   **System requirements:** gcc compiler

   .. note:: Installing on Rocks 6.0 - 6.1 hosts.
      Your Rocks-based host is more likely installed as 64 bit platform. The
      client software neeeds to be compiled in 32 bit mode.
      For this, need to make sure that 32 bit packages for gcc are
      installed: glibc-devel.i686 and libgcc.i686. To check do: ::

         yum list glibc-devel
         yum list libgcc 

      If glibc-devel.i686 and libgcc.i686 are listed under "Available packages" install with ::

         yum install glibc-devel.i686
         yum install libgcc.i686 

#. **Download and extract the PRAGMA-GRID CA client software** ::

      wget http://ca.pragma-grid.net/guide/pragma-ca-client.tar.gz
      tar zxvf pragma-ca-client.tar.gz 
      cd pragma-ca-client 


#. **Compile and install**

   Choose installation directory (any directory where you have write
   access) and run configuration script. For example, to install in /user/local/ca-client: ::

      ./configure --prefix=/usr/local/ca-client CC="gcc -m32" 
      make
      make install 

   A successfull install will show the following at the end of the screen output:
  
   .. role:: stdout

   | :stdout:`...`
   | :stdout:`>> initialize certificate store`
   | 
   | :stdout:`>> installing CA certificates into the store`
   | :stdout:`import a file to the store successfully.`
   | :stdout:`import a file to the store successfully.`
   | :stdout:`import a file to the store successfully.`
   | :stdout:`import a file to the store successfully.`
   | 
   | :stdout:`NAREGI-CA client installation is finished successfully.`
   | 
   | :stdout:`please input "grid-certreq" command to request a certificate.`
   | 

#. **Add installation directory to your $PATH** ::

     export PATH=/usr/local/ca-client/bin:$PATH

Using the CA client software is described in :ref:`userguide`.

