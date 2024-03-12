# Building blockchain-mpc-crypto 

The **blockchain-mpc-crypto** library is a standard C++ dynamic library, which is compatible with any C++ compiler.

This repository includes build projects and scripts for common platforms as described below.

## Dependencies

The **blockchain-mpc-crypto** library has the following dependencies:

- C++ version "-std=c++0x" or newer
- OpenSSL version 1.0.1 or newer
- Java version 1.7 or newer (Optional - use if you need JNI)
- Python version 2.7 or newer (Optional - only for using Python)


Building your target requires having the required OpenSSL version and optionally having Java if JNI is required.

**Note:** If you are using **JNI**, you must define the JAVA_HOME environment variable. It is used in the [makefile](https://github.com/unbound-tech/blockchain-crypto-mpc/blob/master/makefile).

**Note:** If you do not need **JNI** (the library will not be used from Java), you can disable JNI code generation and build dependency on Java header files by defining `MPC_CRYPTO_NO_JNI` (add  the flag `-DMPC_CRYPTO_NO_JNI` to CPP).

## Build Instructions

The following sections provide build instructions for the various platforms.

### Linux

The repository includes a simple makefile for building in Linux. 
1. Install the *openssl-dev* package.
1. Install Java if required.
1. Review the makefile and modify as needed for your environment.
1. Run *make*.

For example, on Ubuntu Linux, use the following:
```sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
export JAVA_HOME=/usr/lib/jvm/java-8-oracle/

sudo apt install make
sudo apt install make-guile
sudo apt-get install gcc
sudo apt-get install g++
sudo apt-get install openssl
sudo apt-get install libssl-dev

git clone https://github.com/unbound-tech/blockchain-crypto-mpc.git
cd blockchain-crypto-mpc
make
export LD_LIBRARY_PATH=.
```

### Windows

The repository includes a Visual Studio solution.
1. Download and build OpenSSL using its built-in scripts. See [OpenSSL on GitHub](https://github.com/openssl/openssl).
1. Set the environment variable OPENSSL_DEV_HOME to the directory where *openssl* was built.
1. If you are building JNI, make sure JAVA_HOME is set properly.
1. Open the solution and compile.


### macOS

This repository includes a macOS Xcode project (in the *macos* folder).

1. Install OpenSSL.
    - The Xcode project looks for OpenSSL in */usr/local/opt/openssl*.
	- If needed, install OpenSSL using HomeBrew: `brew install openssl`
1. Use the project for building the library. 


### Android

The repository includes an Android Studio project for building (in the *android* folder).


### iOS

TBD

### Java

The repository includes a Java build project (in the *Java* folder).

The Java code is a wrapper over the basic native library.

1. Build the native library (including JNI support) for your platform (see relevant platform instructions). 
1. You can then build the and use the Java code.


### Python

The python module is based on the native library (ctypes).


1. Build the native library for your platform (see relevant platform instructions).
1. The python library can then be used with *mpc_crypto.py*.

See *mpc_demo.py* for an actual implementation of client server communication executing different operations. 

## Troubleshooting

JNI Error:

`fatal error: jni.h: No such file or directory`

If you receive this error, then you need to define the JAVA_HOME environment variable. It is used in the [makefile](https://github.com/unbound-tech/blockchain-crypto-mpc/blob/master/makefile).
To do so you can use the below cmd:
export JAVA_HOME=`type -p java|xargs readlink -f|xargs dirname|xargs dirname`