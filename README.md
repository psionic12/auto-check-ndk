# auto-check-ndk

Sometimes all developer in you group do not write c/c++ code except you. Neither you colleagues nor the server gets a NDK environment.

How to write native code in you app while be build on other environment without a NDK:

1. Hide jni directory is there's no NDK:
      
		sourceSets {
	        main {
	            if (!android.ndkDirectory) {
	                jniLibs.srcDirs = ["src/main/libs"]
	                jni.srcDirs = []
	            } else {
	                jniLibs.srcDirs = []
	            }
	        }
	    }

2. Hide externalNativeBuild if there's no NDK:
        
        externalNativeBuild {
            ndkBuild {
                path 'src/main/jni/Android.mk'
            }
        }
        
3. Some other config:

	    defaultConfig {

	        if (ndkDirectory) {
	            ndk {
	                abiFilters  'armeabi-v7a'
	            }
	        }
	    }
