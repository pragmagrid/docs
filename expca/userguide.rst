
.. highlight:: rest
.. include:: expca-rst

.. _userguide:

CA Client Userguide 
====================

**Powered by Naregi-CA** 

.. _usercert:

User Certificates 
------------------

You will need 

+ **an encrypted License ID** that CA sent you in email. Save the attached license key as ``license-id.enc`` file.
+ **L_password** - a password for the license key that CA gave to you. This is a one time password
  to decrypt your License ID. 
+ **C-password** - a password for your certificate. This is your password that will enable you to use
  your certificate. User a strong password that is 12+ characters and contains upper and lower case letters. 

.. _create-usercert:

Request
~~~~~~~~~~
Request user certificate

#. Check the contents of encrypted license ID file: 

   .. role:: stdout

   | **% cat license-id.enc**
   | :stdout:`U2FsdGVkX1+vmRSheB05m10EXNaC82qPHT0cJIa/OSldFHwjI3HW6kKcK/v3i8zs`

#. Decrypt the license key file, use ``L-password`` when prompted. 

   | **% openssl  enc -d -a -des3 -in license-id.enc -out license-id.dec**
   | :stdout:`enter des-ede3-cbc decryption password:`

#. Find your license ID: 

   | **% cat license-id.dec**
   | :stdout:`pragma-4E5F6G-7H8I9J-0KLMNO`

#. Run ``grid-certreq`` with your license ID. This will create a user
   certificate request and send it to ra.pragma-grid.net.  The command will prompt for:
   
   + *ou* - use your abbreviated institution name
   + *user name* - use your first and last name
   + *user email* - your email
   + *PASS Phrase* - your certificate password (C-password)

   For example (here the command is broken into multiple lines for readability: 

   .. role:: red

   .. role:: stdout

   | **% grid-certreq -sv ra.pragma-grid.net:pragma-exp_ra \\**
   | **-new** :red:`pragma-4E5F6G-7H8I9J-0KLMNO` **\\**
   | **-g "SMIME user" -sou**
   | :stdout:`-------------------------------------------`
   | :stdout:`creating a certificate signing request`
   | :stdout:`-------------------------------------------`
   | :stdout:`generate private key (size 1024 bit)`
   | :stdout:`...................................................oo`
   | :stdout:`....................oo`
   | :stdout:`-------input user subject information --------`
   | :stdout:`input ou :` :red:`SDSC`
   | :stdout:`input user name :` :red:`Cindy Zheng`
   | :stdout:`input user email :` :red:`cindy@sdsc.edu`
   | :stdout:`-------please confirm your inputs ------------`
   | :stdout:`GROUP : SMIME user`
   | :stdout:`SUBJECT : OU=SDSC, CN=Cindy Zheng, Email=cindy@sdsc.edu`
   | :stdout:`do you continue operation? (yes/no/retry)[y]: press return`
   | :stdout:`trying to connect RA server : ra.pragma-grid.net (11412) ... ok.`
   | :stdout:`request for issuing a new certificate ... ok.`
   | :stdout:`your request is accepted. (AcceptID=0000003)`
   | :stdout:`CA operator will send an email to tell a result.`
   | :stdout:`save a CA certificate file : /home/cindy/.globus/cacert.pem`
   | :stdout:`save a private key file : /home/cindy/.globus/userkey.pem`
   | :stdout:`Input PASS Phrase:` :red:`type your C-password`
   | :stdout:`Verifying - Input PASS Phrase:` :red:`type your C-password`

   .. note::  make sure that you remember the email address you entered
      and the AcceptID given in the output. You will need them to retrieve
      the certificate later.

#.   Email `CA admin`_ to inform that you have done with the request and provide your request AcceptID.

.. _renew-usercert:

Renew 
~~~~~~
The procedure for a user certificate renewal is very similar to :ref:`create-usercert`.
The only diffenrece is that the license ID is used from the previous certificate and the
information that one needs to provide for OU and CN (user name) is also from your
prevoious certificate. Run ``grid-certreq`` with your license ID and ``-renew`` option.
For example (here the command is broken into multiple lines for readability:

   | **% grid-certreq -sv ra.pragma-grid.net:pragma-exp_ra \\**
   | **-renew** :red:`pragma-4E5F6G-7H8I9J-0KLMNO` **\\**
   | **-g "SMIME user" -sou**

.. _retrieve-usercert:

Retrieve 
~~~~~~~~~
When the CA administrator informs you that your user certificate is ready
for retrieval, run ``grid-certreq`` in your home directory.  You will need to
provide your AcceptID and email. For example:

   .. role:: red

   .. role:: stdout

   | **% grid-certreq -sv ra.pragma-grid.net:pragma-exp_ra \\**
   | **-em** :red:`your@email.address`  **-recv** :red:`0000003`
   | :stdout:`trying to connect RA server : ra.pragma-grid.net (11412)`
   | :stdout:`request for exporting a certificate ... ok`
   | :stdout:`save a CA certificate file : /home/cindy/.globus/cacert.pem`
   | :stdout:`save a certificate file : /home/cindy/.globus/usercert.pem`

The certificates are saved in your ``$HOME/.globus/`` directory. 

.. _test-usercert:

Test
~~~~~
Test your user certificate

#.  Obtain an access to a host with Globus tools installed

    Globus tools can be a part of globus (vdt) installation or they can be installed
    separately. A system administrator of your site will tell you what host to use. 
    More liekly it is the same host where you created your certificate. 

    Make a request to the appropriate contacts, email all the info required, including your DN
    string and `CA URL`_ to PRAGMA-GRID CA certificate files. To find a DN: 

    | **openssl x509 -in $HOME/.globus/usercert.pem -subject -noout**

    When you are informed that the Globus authentication has been setup
    for you on a remote system, proceed with the next step.

#. Create a grid proxy

   .. role: red

   .. role: stdout

   | **% grid-proxy-init**
   | :stdout:`Your identity: /C=us/O=pragma/OU=pragma-grid/CN=Cindy Zheng/emailAddress=cindy@sdsc.edu`
   | :stdout:`Enter GRID pass phrase for this identity:` :red:`type your C-password`
   | :stdout:`Creating proxy`
   | :stdout:`.......................................................... Done`
   | :stdout:`Your proxy is valid until: Thu Sep 7 02:18:11 2006`

   .. note:: the string after ``Your identity:`` is your DN string.

#. Check your authentication and authorization. 

   For example, if the remote system's name is system.domain.edu, run a command: 

   | **globusrun -a -r system.domain.edu**

   The command should return successful status. If not, copy the error
   message and contact the appropriate support personnel for help.

#. If authorization is successful, test job submission to the remote system. 

   For example, if the remote system is running SGE: 

   | **globus-job-run system.domain.edu/jobmanager-sge /bin/hostname**

   You can substitute the appropriate job manager and replace
   ``/bin/hostname`` with any other simple command. The test should return
   the output for the command. If you get error message instead, copy it
   and contact the appropriate support personnel for help.

.. _hostcert:

Host Certificates 
------------------

.. _create-hostcert:

Request 
~~~~~~~~~~
Request host or gfarm server certificate.

#. Check the contents of encrypted license ID file: 

   .. role: stdout

   | **% cat license-id.enc**
   | :stdout:`U2FsdGVkX1+vmRSheB05m10EXNaC82qPHT0cJIa/OSldFHwjI3HW6kKcK/v3i8zs`

#. Decrypt the license key file, use ``L-password`` when prompted. 

   | **% openssl  enc -d -a -des3 -in license-id.enc -out license-id.dec**
   | :stdout:`enter des-ede3-cbc decryption password:`

#. Find your license ID: 

   | **% cat license-id.dec**
   | :stdout:`pragma-4E5F6G-7H8I9J-0KLMNO`

#. Run ``grid-hostreq`` with your license ID and a directory name for storing certificates.
   This will create a host certificate request and send it to ra.pragma-grid.net.  The command will prompt for:
   
   + *ou* - use your abbreviated institution name
   + *user name* - use your host FQDN. If requesting for gfsrm server see Note below.
   + *user email* - your personal email or type ``.``.

   For example (here the command is broken into multiple lines for readability: 

   .. role:: red

   .. role:: stdout

   | **% grid-hostreq -sv ra.pragma-grid.net:pragma-exp_ra \\**
   | **-new** :red:`pragma-4E5F6G-7H8I9J-0KLMNO` **\\**
   | **-g host -dir** :red:`/home/cindy/certdir` **-sou**
   | :stdout:`-------------------------------------------`
   | :stdout:`creating a certificate signing request`
   | :stdout:`-------------------------------------------`
   | :stdout:`generate private key (size 1024 bit)`
   | :stdout:`...................................................oo`
   | :stdout:`....................oo`
   | :stdout:`-------input user subject information --------`
   | :stdout:`input ou :` :red:`SDSC`
   | :stdout:`input user name :` :red:`rocks-96.sdsc.edu`
   | :stdout:`input user email :` :red:`.`
   | :stdout:`-------please confirm your inputs ------------`
   | :stdout:`GROUP : host`
   | :stdout:`SUBJECT : OU=SDSC, CN=rocks-96.sdsc.edu`
   | :stdout:`do you continue operation? (yes/no/retry)[y]:` :red:`press return`
   | :stdout:`trying to connect RA server : ra.pragma-grid.net (11412) ... ok.`
   | :stdout:`request for issuing a new certificate ... ok.`
   | :stdout:`your request is accepted. (AcceptID=0000003)`
   | :stdout:`CA operator will send an email to tell a result.`
   | :stdout:`save a CA certificate file : /home/cindy/certdir/cacert.pem`
   | :stdout:`save a private key file : /home/cindy/certdir/hostrkey.pem`

   .. note::  make sure that you remember the AcceptID given in the output. You will need them to retrieve
      the certificate later.

   .. note::  When requesting a certificate for any gfarm service (file
      server, meta-server, client) make sure that you prepend ``gfsd/`` string
      to the host name. For example, for a gfarm file server certificate for
      host rocks-96.sdsc.edu use: ``gfsd/rocks96.sdsc.edu``

#.   Email `CA admin`_ to inform that you have done with the request and provide your request AcceptID.


.. _renew-hostcert:

Renew 
~~~~~~
The procedure for a host certificate renewal is very similar to :ref:`create-hostcert`.
The only diffenrece is that the license ID is used from the previous certificate and the
information that one needs to provide for OU and CN (user name) is also from your
prevoious certificate. Run ``grid-hostreq`` with your license ID and ``-renew`` option.
For example (here the command is broken into multiple lines for readability:

   .. role:: red

   | **% grid-hostreq -sv ra.pragma-grid.net:pragma-exp_ra \\**
   | **-renew** :red:`pragma-4E5F6G-7H8I9J-0KLMNO` **\\**
   | **-g host -dir** :red:`/home/cindy/certdir` **-sou**

.. _retrieve-hostcert:

Retrieve 
~~~~~~~~~
When the CA administrator informs you that your host certificate is ready
for retrieval, run ``grid-hostreq`` in your home directory.  You will need to
provide your AcceptID and a directory where certificate request is stored. For example:

   .. role:: red

   .. role:: stdout

   | **% grid-hostreq -sv ra.pragma-grid.net:pragma-exp_ra \\**
   | **-recv** :red:`0000003` **-dir** :red:`/home/cindy/certdir`
   | :stdout:`trying to connect RA server : ra.pragma-grid.net (11412)`
   | :stdout:`request for exporting a certificate ... ok`
   | :stdout:`save a CA certificate file : /home/cindy/certdir/cacert.pem`
   | :stdout:`save a certificate file : /home/cindy/certdir/usercert.pem`

The certificates are saved in the directory specified by ``-dir`` option.

.. _install-hostcert:

Install 
~~~~~~~~~

#. Install PRAGMA-GRID CA certificate files ::

     # wget http://ca.pragma-grid.net/ca-certs/5456d9ca.0 
     # wget http://ca.pragma-grid.net/ca-certs/5456d9ca.0.signing_policy

   Install the above certificate files in ``/etc/grid-security/certificates/``
   directory and set file ownerships and permissions as following: ::

     # chmod 644 /etc/grid-security/certificates/5456d9ca.0
     # chmod 644 /etc/grid-security/certificates/5456d9ca.signing_policy 

#. Install your host certificate 

   If you requested a host certificate, copy the certificate files
   from the directory where they were created to ``/etc/grid-security/`` 
   directory and set the correct permissions. For example: ::

     # cp /home/cindy/certidir/*.pem /etc/grid-security/
     # chmod 644 /etc/grid-security/cacert.pem
     # chmod 644 /etc/grid-security/hostcert.pem
     # chmod 400 /etc/grid-security/hostkey.pem


#. Install your Gfarm service certificate 

   If you requested a Gfarm service sertificate, copy the certificate
   files to ``/etc/grid-security/gfsd/`` directory and set the correct permissions: ::

      # mkdir -p /etc/grid-security/gfsd/
      # cp /home/cindy/hostcerts.new/hostcert.pem /etc/grid-security/gfsd/gfsdcert.pem
      # cp /home/cindy/hostcerts.new/hostkey.pem /etc/grid- security/gfsd/gfsdkey.pem
      # chown -R _gfarmfs:_gfarmfs /etc/grid-security/gfsd/
      # chmod 644 /etc/grid-security/gfsd/gfsdcert.pem
      # chmod 600 /etc/grid-security/gfsd/gfsdkey.pem

.. _test-hostcert:

Test
~~~~~~

To test your host certificate setup do :ref:`user certificate testing <test-usercert>` 

