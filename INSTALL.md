NDN-CPP:  A Named Data Networking client library for C++ and C
-------------------------------------------------------------

Prerequisites
-------------
(These are prerequisites to build NDN-CPP.  To do development of NDN-CPP code and update the build system, 
 see Development Prerequisites.)

Required: libcrypto
Optional: libsqlite3 (for key storage)
Optional: OSX Security framework (for key storage)

Following are the detailed steps for each platform to install the prerequisites.

* Mac OS X 10.7.3, Mac OS X 10.8.4
Install Xcode.
In Xcode Preferences > Downloads, install "Command Line Tools".

* Mac OS X 10.9
Install Xcode.  (Xcode on OS X 10.9 seems to already have the Command Line Tools.)

* Ubuntu 12.04 (64 bit and 32 bit), Ubuntu 13.04 (64 bit)
In a terminal, enter:
sudo apt-get install build-essential
sudo apt-get install libssl-dev

* Windows Cygwin
Cygwin is tested on Windows 7 64-bit. 
In the Cygwin installer, select and install the "Devel" packages at the top level of the installer.
(The "Devel" packages include libcrypto and libsqlite3.)

Build
-----
(These are instructions to build NDN-CPP. To do development of NDN-CPP code and update the build system, see Development.)

To build in a terminal, change directory to the NDN-CPP root.  Enter:

./configure
make
sudo make install

NDN-CPP uses NDN-TLV as the default wire format:
http://named-data.net/doc/ndn-tlv/tlv.html
To revert to Binary XML (ndnb) as the default wire format, instead of ./configure, use
./configure --enable-binary-xml=yes

To make documentation, enter:
make doxygen-doc

Files
-----

This makes the following libraries:

.libs/libndn-c.a: The core C code for encoding and communication.
.libs/libndn-cpp.a: The C++ library API.  (If linking to libndn-cpp, don't link to libndn-c since it is included.)

This makes the following test files:

bin/test-get-async: Connect to one of the NDN testbed hubs, express an interest and display the received data.
bin/test-publish-async-ndnx: Connect to the local NDNx hub, accept interests with prefix /testecho and echo back a data packet. See test-echo-consumer.
bin/test-publish-async-nfd: Connect to the local NFD hub, accept interests with prefix /testecho and echo back a data packet. See test-echo-consumer.
bin/test-echo-consumer: Prompt for a word, send the interest /testecho/<word> to the local hub which is echoed by test-publish-async-nfd (or test-publish-async-ndnx).
bin/test-encode-decode-interest: Encode and decode an interest, testing interest selectors and the name URI.
bin/test-encode-decode-data: Encode and decode a data packet, including signing the data packet.
bin/test-encode-decode-forwarding-entry: Encode and decode a data packet, including signing the data packet.

Running make doxygen-doc puts code documentation in:
doc/html

Supported platforms
-------------------

NDN-CPP is tested on the following platforms:
Ubuntu 12.04 (64 bit and 32 bit) (gcc 4.6.3)
Ubuntu 13.04 (64 bit) (gcc 4.7.3)
Mac OS X 10.8.4 (clang 4.2)
Mac OS X 10.8.4 (gcc 4.2)

Development Prerequisites
-------------------------
These steps are only needed to do development of NDN-CPP code and update the build system.
First follow the Prerequisites above for your platforms.

* Mac OS X 10.7.3, Mac OS X 10.8.4, Mac OS X 10.9
Install MacPorts from http://www.macports.org/install.php
In a terminal, enter:
sudo port install automake autoconf libtool doxygen

* Ubuntu 12.04 (64 bit and 32 bit), Ubuntu 13.04 (64 bit)
In a terminal, enter:
sudo apt-get install automake libtool doxygen

Development
-----------
Follow Development Prerequisites above for your platform.
Now you can add source code files and update Makefile.am.  
After updating, change directory to the NDN-CPP root and enter the following to build the Makefile:
./autogen.sh
To build again, follow the instructions above (./configure, make, etc.)
