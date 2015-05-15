# Introduction #

If you're a Maven user, you probably know how hard it is to obtain a dependency on an OSGi Bundle (e.g. an Eclipse Plugin) to be used as a part of your Maven build. Not only that you need to deploy a jar into your repository, but you also need to track down all dependencies of that jar and deploy them too. This is an error prone task of manually checking dependencies, writing your own POM files and deploying everything.

Fortunately, this job can be automated. One of my older projects http://code.google.com/p/osgi-to-maven2/ does that for you. In the meantime there are other projects such as http://wiki.eclipse.org/Maven_Tools_4_Eclipse that serve the same purpose.

Although generation of POM files became much easier, deploying all Bundles delivered with Eclipse takes long time. In order to reduce that time, I came up with the idea to implement a Maven repository that will offer OSGi bundles as Maven artifacts: Maven-Osgi-Repo


# Details #

From Maven's point of view, Maven-Osgi-Repo is a normal Maven repository. It contains a standard Maven-2 Repository layout and can be connected to via Http. Internally, content of the Repository is created on the fly based on a directory that contains OSGi Bundles. For each OSGi Bundle in the provided directory, following Maven Artifacts are created:

  * POM file containing proper name of the bundle and all its dependencies
  * Jar file containing the bundle itself. If Bundle is in the unpacked form, the content of the bundle is still offered as a Jar file to Maven (is packed on the fly).
  * Source Jar file if the bundle has a companion source jar
  * MD5 and SHA1 hash values of all previous files


