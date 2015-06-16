This template project aims to facilitate the quick production of visual languages towards a later migration, or not, to larger more standardized frameworks, such as ECORE. The main outcome of this project are binaries  self-contained versions of editors implementing a visual language defined by the user. The work bases on the INGENME framework (http://ingenme.sf.net). 

The development of a visual language with INGENME requires a maven multimodule structure. There is a main folder containing two subfolders or modules, according to the maven terminology. I reccommend at least two modules, one for defining the visual language and another to show how to use the generated visual modeling language. In a practical development, several of the later are needed. 

The notation used to define the visual modeling language is inspired on GOPRR, but goes beyond it. Defining a visual modeling language is a matter of determining the diagrams you allow, the entities and relationships to be allowed in each diagram, and the properties of all of them. This is what is technically called *abstract syntax*. 

If only these elements are described, there is just a UML-like notation produced by default. Entities, diagrams, and relationships representation can be customized to an important extent. Defining explicitly their representation is what is called *concrete syntax*. Usually, concrete and abstract syntax are decoupled in other solutions, such as Eclipse's GMF. 

#Required software
This template requires JDK, Maven, and Ant installed. Instructions for installing them can be found in their corresponding sites:

- Java. http://java.sun.com
- Ant.  http://ant.apache.org
- Maven. http://maven.apache.org

#Configuring environment variables
The most troublesome part for installing the software is properly configuring the environment variables, specially for maven.  

Relevant environment variables to have are:
* JAVA_HOME. It will point to the JDK install folder. JRE is not enough, the full JDK is needed.
* M2_HOME. The home folder for maven. In ubuntu, it is /usr/share/maven. In windows, it will depend where the 

Also, it is necessary to include JDK, Maven, and Ant binaries into the PATH environment variable.

#Installing/using the template

Copy or fork this template and go to the main folder. From there, run
```Shell
	mvn clean install
```

To modify the visual language, open the meta-model editor and proceed to create new entities and attach them to the diagram, as in the example

```Shell
	cd editor
	ant edit
```

Produce a self-contained editor, run the following, from the main folder

```Shell
	cd editor
	mvn clean install

```
In the editor/target folder you will find several jars:

- *editor-1.0.0-SNAPSHOT-installer.jar*. This is an installer to distribute among your colleagues. It creates a folder where the jar executable is copied. It also provides instructions and license warnings.  
- *editor-1.0.0-SNAPSHOT-selfcontained.jar*. It is a self-contained file that can be distributed and used directly. If JDK is properly installed, a double click on this file from a file explorer ought to open the resulting editor. If not, from command line, a *java editor-1.0.0-SNAPSHOT-selfcontained.jar*  will do the trick.

The previous instructions allow to start creating models followign the constraints of your visual modeling language. However, it is more disciplined to create those examples as modules of the development. Also, it helps to convey a development process where the modeling language has a very well defined role. The example reuses directly the installed editor, if the developer previosly did a *mvn install* at some point. Working with the example, is easy. To open a specification with the generated editor:

```Shell
	cd example
	ant edit
```


#Creating the site
Documenting your visual language is a basic task. The project is prepared to produce sites containing documentation of your project. Description fields in the specification are processed as markdown code. The result will be added to the resulting site.

Run the following from your main project folder
```Shell
	mvn clean site site:deploy
```
The generated site will be in your target/finalsite folder.

For Ubuntu 14.04, if you find this error:
```
	[ERROR] Number of foreign imports: 1
	[ERROR] import: Entry[import  from realm ClassRealm[maven.api, parent: null]]
	[ERROR] 
	[ERROR] -----------------------------------------------------:
 org.apache.commons.lang.StringUtils
```

Try the following workaround
```Shell
	cd /usr/share/maven/lib
	sudo ln -s ../../java/commons-lang.jar .
```

#Acknowledgements

This software was produced along several national projects, namely INGENIAS, INGENIAS2, Psycossys, and SociAAL. The main developer is Jorge J. Gomez-Sanz.


