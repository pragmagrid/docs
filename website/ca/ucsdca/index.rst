.. pragma-ucsd ca documentation 

.. highlight:: rest
.. include:: ca-rst

.. toctree::
   :maxdepth: 2


PRAGMA-UCSD CA
================
| **Pacific Rim Application and Middleware Assembly (PRAGMA)**
| **University of California, San Diego (UCSD)**

Welcome to PRAGMA-UCSD Certificate Authority (CA) Web site.
PRAGMA-UCSD Certificate Authority is established as a `PRAGMA Grid`_
PKI service and is working closely with `APGRID`_ PMA. Certificates
issued by the PRAGMA-UCSD CA are compatible with the Globus Toolkit
middleware.

To obtain user or host certificates from PRAGMA-UCSD CA, 
you must be a member of PRAGMA or an individual working on *projects involved in PRAGMA* or
*Grid projects in collaboration with PRAGMA*

.. note:: For PRAGMA Experimental CA please see `Experimental CA`_

PRAGMA-UCSD CA Files
--------------------------------
+ |PEM|_ (also available in `CER`_, `P12`_, and `P7B`_ format)

  Please verify at least one of the fingerprints matches (listed below) before installing 
  the root certiifcate using the corresponding command: ::

    # openssl x509 -in DownloadedCert.0 -sha1 -noout -fingerprint
    # openssl x509 -in DownloadedCert.0 -md5 -noout -fingerprint

  .. role:: red

  | :red:`SHA1 Fingerprint=35:3D:A7:16:0C:B4:C7:B5:E8:53:EA:9F:96:51:D1:5F:60:87:35:F6`
  | :red:`MD5 Fingerprint=E1:AB:22:FC:20:A0:41:1A:AE:7C:0B:7C:46:0E:BD:FE`

+ `CRL`_  (also available in `DER`_ format)
+ `Certificate signing Policy`_
+ `Issued Certificates`_  
+ |cp-cps|_

Contact Information
-------------------
For inquiries regarding the PRAGMA GRID PKI service in general, please contact:

+------------------------------------------------+-----------------------------------------------------------------------+
| PRAGMA-UCSD CA/RA:                             |   PRAGMA-UCSD PMA:                                                    |
+================================================+=======================================================================+
|  | Luca Clementi / Nadya Williams              |   | Yoshio Tanaka                                                     |
|  | PRAGMA-UCSD CA Management Team, PRAGMA      |   | Grid Technology Research Center                                   |
|  | University of California, San Diego 9500    |   | National Institute of Advanced Industrial Science and Technology  |
|  | Gilman Dr. San Diego, CA 92093-0440         |   | Tsukuba Central 2, 1-1-1, Umezono,                                |
|  | Phone: +1-858-534-1820                      |   | Tsukuba, Ibaraki 305-8568, Japan                                  |
|  | Fax: +1-858-534-5035                        |   | Phone: +81-29-861-5356                                            |
|  | Email: `CA email`_                          |   | Fax: +81-29-862-6601                                              |
|                                                |   | Email: `PMA email`_                                               |
+------------------------------------------------+-----------------------------------------------------------------------+

.. _apply:

Apply for certificates
------------------------ 
#. A user downloads the appropriate aplication from the list below and 
   emails filled application  to `CA email`_.

   | `User Certificate Application Form`_  (`user example`_)
   | `Host Certificate Application Form`_ (`host example`_)
#. A registration administrator (RA) will contact the user to arrange
   a face-to-face or VTC interview to verify the user's identity.
#. Uppon verification of user's identity, the RA signs user's application form
   and submits it to a certificate administrator (CA). 
#. The CA will email the user

    + url to PRAGMA-UCSD CA client software package
    + url to PRAGMA-UCSD CA client software user guide
    + an encrypted license id

   and hand or fax the password used to encrypt license id.

#. The user follows instructions in the user guide to install the 
   software package and to request/retrieve the certificate(s).


.. _related sites:

Related Sites
-------------

**Policy Management Authorities (PMAs)**

    + `International Grid Trust Federation`_
    + `APGrid Policy Management Authority`_
    + `TAGPMA (The Americas Grid Policy Management Authority)`_
    + `EU Grid PMA`_

**Certificate Authorities (CA) Sites**

    + `PRAGMA Grid trusted CAs`_
    + `DOE Grids PMA`_
    + `AIST Grid CA, Japan`_
    + `APAC Grid CA, Australia`_
    + `ASGCCA, Taiwan`_
    + `CNIC Grid CA`_
    + `SDG CA`_
    + `IHEP CA, China`_
    + `KEK Grid CA, Japan`_
    + `NAREGI CA, Japan`_


