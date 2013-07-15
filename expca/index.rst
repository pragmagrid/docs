.. pragma-ucsd experimental ca documentation 

.. highlight:: rest
.. include:: expca-rst

.. toctree::
   :maxdepth: 2

.. _experimental ca:

PRAGMA Experimental CA
========================
| **Pacific Rim Application and Middleware Assembly (PRAGMA)**
| **University of California, San Diego (UCSD)**

Welcome to PRAGMA Experimental Certificate Authority (CA) Web site.
PRAGMA Experimental Certificate Authority is established as a `PRAGMA Grid`_
PKI service and is working closely with `APGRID`_ PMA. Certificates
issued by the PRAGMA-UCSD CA are compatible with the Globus Toolkit
middleware.

To obtain user or host certificates from PRAGMA Experimental CA, 
you must be a member of PRAGMA or an individual working on *projects involved in PRAGMA* or
*Grid projects in collaboration with PRAGMA*

PRAGMA-UCSD CA Files
--------------------------------
+ |PEM|_ (also available in `CER`_, `P12`_, and `P7B`_ format)

  Please verify at least one of the fingerprints matches (listed below) before installing 
  the root certiifcate using the corresponding command: ::

    # openssl x509 -in DownloadedCert.0 -sha1 -noout -fingerprint
    # openssl x509 -in DownloadedCert.0 -md5 -noout -fingerprint

  .. role:: red

  | :red:`SHA1 Fingerprint=84:9C:7D:2B:A6:2E:D7:4D:97:FD:B2:03:0D:3A:67:76:8F:99:B1:05`
  | :red:`MD5 Fingerprint=4F:F2:CB:6E:CB:48:FD:E4:8F:6E:96:D7:6D:FC:12:72`

+ `CRL`_  (also available in `DER`_ format)
+ `Certificate signing Policy`_
+ `Issued Certificates`_  

Contact Information
-------------------
For inquiries regarding the PRAGMA Experimental GRID PKI service in general, please contact:

| **PRAGMA Experimental CA/RA:**
| Luca Clementi / Nadya Williams       
| PRAGMA Experimental CA Management Team, PRAGMA 
| University of California, San Diego 9500    
| Gilman Dr. San Diego, CA 92093-0440        
| Phone: +1-858-534-1820                    
| Fax: +1-858-534-5035                     
| Email: `CA email`_                      

.. _apply exp:

Apply for certificates
------------------------ 
#. A user downloads the appropriate aplication from the list below and 
   emails filled application  to `CA email`_.

   | `User Certificate Application Form`_  (`user example`_)
   | `Host Certificate Application Form`_ (`host example`_)
#. A registration administrator (RA) will contact the user to verify the user's identity.
#. Uppon verification of user's identity, the RA signs user's application form
   and submits it to a certificate administrator (CA). 
#. The CA will email the user

    + url to PRAGMA-UCSD CA client software package
    + url to PRAGMA-UCSD CA client software user guide
    + an encrypted license id

   and hand or fax the password used to encrypt license id.

#. The user follows instructions in the user guide to install the 
   software package and to request/retrieve the certificate(s).

.. _related sites exp:

Related Sites
-------------

**Policy Management Authorities (PMAs)**

    + `International Grid Trust Federation`_
    + `APGrid Policy Management Authority`_
    + `TAGPMA (The Americas Grid Policy Management Authority)`_
    + `EU Grid PMA`_

**Certificate Authorities (CA) Sites**

    + `PRAGMA Grid trusted CAs`_
    + `PRAGMA-UCSD CA`_
    + `DOE Grids PMA`_
    + `AIST Grid CA, Japan`_
    + `APAC Grid CA, Australia`_
    + `ASGCCA, Taiwan`_
    + `CNIC Grid CA`_
    + `SDG CA`_
    + `IHEP CA, China`_
    + `KEK Grid CA, Japan`_
    + `NAREGI CA, Japan`_


