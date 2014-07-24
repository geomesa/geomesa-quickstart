GeoMesa Quick-Start Tutorial
============================

This tutorial is the fastest and easiest way to get started with GeoMesa.  It is
a good stepping-stone on the path to the other tutorials that present
increasingly involved examples of how to use GeoMesa.

In the spirit of keeping things simple, the code in this tutorial only does a
few small things:

1.  establishes a new (static) SimpleFeatureType
2.  prepares the Accumulo table to store this type of data
3.  creates a few hundred exmple SimpleFeatures
4.  writes these SimpleFeatures to the Accumulo table
5.  queries for a given geographic rectangle, time range, and attribute filter,
    writing out the entries in the result set

The only dynamic element in the tutorial is the Accumulo destination; that is
a property that you provide on the command-line when running the code.

Prerequisites
-------------

Before you begin, you must have the following:

* an instance of Accumulo 1.5.x running on Hadoop 2.2.x
* an Accumulo user that has both create-table and write permissions
* a local copy of the [Java](http://java.oracle.com/) Development Kit 1.7.x
* Apache [Maven](http://maven.apache.org/) installed
* a GitHub client installed

Download and build GeoMesa
--------------------------

Pick a reasonable directory on your machine, and run:

```
git clone git@github.com:locationtech/geomesa.git
```

From that newly-created directory, run

```
mvn clean install
```

NB:  This step is only required, because the GeoMesa artifacts have not yet
been published to a public Maven repository.  With the upcoming 1.0 release of
GeoMesa, these artifacts will be available at LocationTech's Nexus server, and
this download-and-build step will become obsolete.

Download and build this tutorial
--------------------------------

Pick a reasonable directory on your machine, and run:

```
git clone git@github.com:geomesa/geomesa-quickstart.git
```

The ```pom.xml``` file contains an explicit list of dependent libraries that will be bundled together into the final tutorial.  You should confirm
that the versions of Accumulo and Hadoop match what you are running; if it does not match, change the value in the POM.  (NB:  The only reason these libraries
are bundled into the final JAR is that this is easier for most people to do this than it is to set the classpath when running the tutorial.
If you would rather not bundle these dependencies, mark them as ```provided``` in the POM, and update your classpath as appropriate.)

From within the root of the cloned tutorial, run:

```
mvn clean install
```

When this is complete, it should have built a JAR file that contains all of the code you need to run the tutorial.

Run the tutorial
----------------

On the command-line, run:

```
java -cp ./target/geomesa-quickstart-accumulo1.5-1.0-SNAPSHOT.jar org.geomesa.QuickStart -instanceId somecloud -zookeepers "zoo1:2181,zoo2:2181,zoo3:2181" -user someuser -password somepwd -tableName sometable
```

where you provide the following arguments:

* ```somecloud```:  the name of your Accumulo instance
* ```zoo1:2181,zoo2:2181,zoo3:2181```:  your Zookeeper nodes, separated by commas
* ```someuser```:  the name of an Accumulo user that has permissions to create, and write to, tables
* ```somepwd```:  the password for the previously-mentioned Accumulo user
* ```sometable```:  the name of the destination table that will accept these test records; this table should either not exist or should be empty

You should see output similar to the following (not including some of Maven's output and log4j's warnings):

    Creating feature-type (schema):  QuickStart
    Creating new features
    Inserting new features
    Submitting query
    1.  Bierce|640|Sun Sep 14 15:48:25 EDT 2014|POINT (-77.36222958792739 -37.13013846773835)|null
    2.  Bierce|886|Tue Jul 22 14:12:36 EDT 2014|POINT (-76.59795732474399 -37.18420917493149)|null
    3.  Bierce|925|Sun Aug 17 23:28:33 EDT 2014|POINT (-76.5621106573523 -37.34321201566148)|null
    4.  Bierce|589|Sat Jul 05 02:02:15 EDT 2014|POINT (-76.88146600670152 -37.40156607152168)|null
    5.  Bierce|394|Fri Aug 01 19:55:05 EDT 2014|POINT (-77.42555615743139 -37.26710898726304)|null
    6.  Bierce|931|Fri Jul 04 18:25:38 EDT 2014|POINT (-76.51304097832912 -37.49406125975311)|null
    7.  Bierce|322|Tue Jul 15 17:09:42 EDT 2014|POINT (-77.01760098223343 -37.30933767159561)|null
    8.  Bierce|343|Wed Aug 06 04:59:22 EDT 2014|POINT (-76.66826220670282 -37.44503877750368)|null
    9.  Bierce|259|Thu Aug 28 15:59:30 EDT 2014|POINT (-76.90122194030118 -37.148525741002466)|null
