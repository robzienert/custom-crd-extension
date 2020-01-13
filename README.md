# custom-crd-extension

`custom-crd-extension` is an example of how to build an extension of Clouddriver, specifically for adding a custom CRD Handler.

In this repo you'll find the following:

* A customized extension of Clouddriver (under the `custom-crd-extension` directory).
* Gradle files to build the project and include any dependencies it relies on.
* A Dockerfile for building a container image of the application


## How it works

This project depends on Clouddriver as a library and utilizing Spring components to inject our behavior. At the time of this writing,
we're pulling in the version of Clouddriver available in 1.17.3 of the OSS Spinnaker project. This version can be found in `build.gradle` 
under `clouddriverVersion`.


When the application boots, Clouddriver will scan for components in the `com.netflix.spinnaker.config` package. You'll notice that we have an 
`ExtensionConfig` class in `custom-crd-extension` to satisfy this requirement. This is where we can hook into all of our custom code. 

A `@ComponentScan` for `com.netflix.spinnaker.internal` will pull in our custom handlers and inject them into the project. You 
can add other custom handlers in this area as you like.

## Running the project

Running the extension is the same as you would run upstream Clouddriver. Simply run `./gradlew` and the application will start.


## Building the project

Included is Dockerfile (based on the upstream Dockerfile) for building a container image. Run the following command to build it.

```
$ docker build -t {you-image-name} .
```