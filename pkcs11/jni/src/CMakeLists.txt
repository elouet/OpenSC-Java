
# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.18.1)

# Declares and names the project.

project("keystoretest")

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds them for you.
# Gradle automatically packages shared libraries with your APK.

add_library( # Sets the name of the library.
             keystoretest

             # Sets the library as a shared library.
             SHARED

             # Provides a relative path to your source file(s).
		    ./jnix/jnix.c ./jniP11/org_opensc_pkcs11_wrap_PKCS11Slot.c ./jniP11/org_opensc_pkcs11_spi_PKCS11SignatureSpi.c ./jniP11/org_opensc_pkcs11_wrap_PKCS11KeyPairGenerator.c ./jniP11/pkcs11_module.c ./jniP11/org_opensc_pkcs11_spi_PKCS11CipherSpi.c ./jniP11/org_opensc_pkcs11_wrap_PKCS11Object.c ./jniP11/pkcs11_error.c ./jniP11/org_opensc_pkcs11_wrap_PKCS11Session.c ./jniP11/pkcs11_slot.c ./jniP11/org_opensc_pkcs11_PKCS11Provider.c )

add_library( ckteec
		SHARED
		IMPORTED )

find_library(
		ckteec-DEV
		ckteec
)
set_target_properties( # Specifies the target library.
		ckteec

		# Specifies the parameter you want to define.
		PROPERTIES IMPORTED_LOCATION

		# Provides the path to the library you want to import.
		lib/libckteec-DEV.so )


# Searches for a specified prebuilt library and stores the path as a
# variable. Because CMake includes system libraries in the search path by
# default, you only need to specify the name of the public NDK library
# you want to add. CMake verifies that the library exists before
# completing its build.

find_library( # Sets the name of the path variable.
              log-lib

              # Specifies the name of the NDK library that
              # you want CMake to locate.
              log )

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in this
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( # Specifies the target library.
                       keystoretest
					${ckteec}

                       # Links the target library to the log library
                       # included in the NDK.
                       ${log-lib} )
