# angular.io tutorial

See [tutorial](https://angular.io/start)

To compile:
```bash
$ mvn clean install
```

To execute:
```bash
$ java -jar sw.angular.io-example.launcher/target/sw-angular.io-example-launcher-1.0.0-SNAPSHOT.war
```

See `webapp` [overview](sw.angular.io-example.webapp/README.md)

See `launcher` [overview](sw.angular.io-example.launcher/README.md)

`git` history shows the commits for each step in [tutorial](https://angular.io/start), 
eg.

```bash
$ git log

commit 36886887046c3e98846f0dbbb6362dfbe32d2f26
Author: stewart.witchalls <stewart.witchalls@cdl.co.uk>
Date:   Fri Feb 28 09:50:56 2020 +0000

    Step 4. Add product descriptions

commit beee21eef4687c7226a201222fed7362a680363a
Author: stewart.witchalls <stewart.witchalls@cdl.co.uk>
Date:   Fri Feb 28 09:47:04 2020 +0000

    Step 3. List products
```

## Extra reading

* [Internationalisation](https://angular.io/guide/i18n)

* [Material components](https://material.angular.io/components/)

* [Angular vs React vs Vue](https://www.codeinwp.com/blog/angular-vs-vue-vs-react/)

* [Pros & cons](https://medium.com/@TechMagic/reactjs-vs-angular5-vs-vue-js-what-to-choose-in-2018-b91e028fa91d)

## Lessons learnt (so far)

### Always start with a new `np-app` project

Project files are Angular version related. Using the wrong ones will break 
the application.

I originally started by copying the project files provided by [angular.io](https://angular.io/start).

These triggered browser errors on launch, eg.

```java
compiler.js:2175 Uncaught Error: Can't resolve all parameters for ProductDetailsComponent: (?).
    at syntaxError (compiler.js:2175)
    at CompileMetadataResolver._getDependenciesMetadata (compiler.js:20401)
    at CompileMetadataResolver._getTypeMetadata (compiler.js:20296)
    at CompileMetadataResolver.getNonNormalizedDirectiveMetadata (compiler.js:19925)
    at CompileMetadataResolver._getEntryComponentMetadata (compiler.js:20496)
    at compiler.js:20488
    at Array.forEach (<anonymous>)
    at CompileMetadataResolver._getEntryComponentsFromProvider (compiler.js:20487)
    at compiler.js:20458
    at Array.forEach (<anonymous>)
```

The application only launched (as expected) after copying the [angular.io](https://angular.io/start)
files into a clone of the `np-app` project.

### Avoid manually fixing build errors

[angular.io](https://angular.io/start) declares the following dependencies 

```json
  "devDependencies": {
    "@angular-devkit/build-angular": "~0.10.0",
    "@angular/cli": "~7.0.2",
```

The build (Mac OS X 10.15.3) failed with 

```bash
[INFO] > node-gyp rebuild
[INFO]
[ERROR] No receipt for 'com.apple.pkg.CLTools_Executables' found at '/'.
[ERROR]
[ERROR] No receipt for 'com.apple.pkg.DeveloperToolsCLILeo' found at '/'.
[ERROR]
[ERROR] No receipt for 'com.apple.pkg.DeveloperToolsCLI' found at '/'.
[ERROR]
[ERROR] gyp: No Xcode or CLT version detected!
[ERROR] gyp ERR! configure error
[ERROR] gyp ERR! stack Error: `gyp` failed with exit code: 1
[ERROR] gyp ERR! stack     at ChildProcess.onCpExit (/Users/stewartw/Desktop/My Stuff/sw-angular.io-example/sw.angular.io-example.webapp/target/node/node_modules/npm/node_modules/node-gyp/lib/configure.js:351:16)
[ERROR] gyp ERR! stack     at ChildProcess.emit (events.js:321:20)
[ERROR] gyp ERR! stack     at Process.ChildProcess._handle.onexit (internal/child_process.js:275:12)
[ERROR] gyp ERR! System Darwin 19.3.0
[ERROR] gyp ERR! command "/Users/stewartw/Desktop/My Stuff/sw-angular.io-example/sw.angular.io-example.webapp/target/node/node" "/Users/stewartw/Desktop/My Stuff/sw-angular.io-example/sw.angular.io-example.war/target/node/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
[ERROR] gyp ERR! cwd /Users/stewartw/Desktop/My Stuff/sw-angular.io-example/sw.angular.io-example.webapp/src/main/angular.io-example/node_modules/fsevents
[ERROR] gyp ERR! node -v v13.9.0
[ERROR] gyp ERR! node-gyp -v v5.0.7
[ERROR] gyp ERR! not ok
```

The issue is known ; see `d3-scale-cluster` [issue](https://github.com/schnerd/d3-scale-cluster/issues/7)

... and workarounds exist ; see `node-gyp` [installation notes](https://github.com/nodejs/node-gyp/blob/master/macOS_Catalina.md)

After installing the required Mac OS dependencies, the build failed with

```bash
[INFO]   c++ '-DNODE_GYP_MODULE_NAME=binding' '-DUSING_UV_SHARED=1' '-DUSING_V8_SHARED=1' '-DV8_DEPRECATION_WARNINGS=1' '-DV8_DEPRECATION_WARNINGS' '-DV8_IMMINENT_DEPRECATION_WARNINGS' '-D_DARWIN_USE_64_BIT_INODE=1' '-D_LARGEFILE_SOURCE' '-D_FILE_OFFSET_BITS=64' '-DOPENSSL_NO_PINSHARED' '-DOPENSSL_THREADS' '-DBUILDING_NODE_EXTENSION' -I/Users/stewartw/.node-gyp/12.16.1/include/node -I/Users/stewartw/.node-gyp/12.16.1/src -I/Users/stewartw/.node-gyp/12.16.1/deps/openssl/config -I/Users/stewartw/.node-gyp/12.16.1/deps/openssl/openssl/include -I/Users/stewartw/.node-gyp/12.16.1/deps/uv/include -I/Users/stewartw/.node-gyp/12.16.1/deps/zlib -I/Users/stewartw/.node-gyp/12.16.1/deps/v8/include -I../../nan -I../src/libsass/include  -Os -gdwarf-2 -mmacosx-version-min=10.7 -arch x86_64 -Wall -Wendif-labels -W -Wno-unused-parameter -std=gnu++1y -stdlib=libc++ -fno-rtti -fno-exceptions -std=c++11 -MMD -MF ./Release/.deps/Release/obj.target/binding/src/create_string.o.d.raw   -c -o Release/obj.target/binding/src/create_string.o ../src/create_string.cpp
[INFO] ../src/create_string.cpp:17:25: error: no matching constructor for initialization of 'v8::String::Utf8Value'
[INFO]   v8::String::Utf8Value string(value);
[INFO]                         ^      ~~~~~
[INFO] /Users/stewartw/.node-gyp/12.16.1/include/node/v8.h:3142:5: note: candidate constructor not viable: no known conversion from 'v8::Local<v8::Value>' to 'const v8::String::Utf8Value' for 1st argument
[INFO]     Utf8Value(const Utf8Value&) = delete;
[INFO]     ^
[INFO] /Users/stewartw/.node-gyp/12.16.1/include/node/v8.h:3135:5: note: candidate constructor not viable: requires 2 arguments, but 1 was provided
[INFO]     Utf8Value(Isolate* isolate, Local<v8::Value> obj);
[INFO]     ^
[INFO] 1 error generated.
```

This issue is known ; see `node-gyp` [issue](https://github.com/nodejs/node-gyp/issues/1763/)

After wasting many hours trying to fix the build, I eventually found `angular-cli` [issue](https://github.com/angular/angular-cli/issues/14339)

Cloning a working `np-app` project fixed the issue.

### Not all application files live under `src/app`

Some `src` files are used to launch the application.

* `src/styles.css` defines global CSS used across all pages.

* `src/index.html` imports the CSS for Angular plugins, eg.
  [stackoverflow](https://stackoverflow.com/questions/33855829/materializecss-icons-not-working)

