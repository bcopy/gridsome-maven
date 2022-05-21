# Gridsome starter project with Maven

Why even ? Maven and the excellent [frontend plugin](https://github.com/eirslett/frontend-maven-plugin) provide a virtual environment for NPM-based development.

## How to boostrap your own Maven and NPM project

You need to register a Maven POM file using the Frontend plugin, as described on the [plugin homepage](https://github.com/eirslett/frontend-maven-plugin). Your configuration should specify the Node and NPM installation, like so, for instance node v12 and npm v6 :

```xml
<plugin>
               <groupId>com.github.eirslett</groupId>
               <artifactId>frontend-maven-plugin</artifactId>
               <version>1.12.1</version>
               <configuration>
                   <workingDirectory>${project.basedir}</workingDirectory>
                   <nodeVersion>v12.18.3</nodeVersion>
                   <npmVersion>6.14.8</npmVersion>
               </configuration>
               <executions>
                   <execution>
                       <id>install node and npm</id>
                       <goals>
                           <goal>install-node-and-npm</goal>
                       </goals>
                   </execution>
                   <execution>
                       <id>npm install</id>
                       <goals>
                           <goal>npm</goal>
                       </goals>
                   </execution>
                   <execution>
                       <id>npm run build</id>
                       <goals>
                           <goal>npm</goal>
                       </goals>
                       <configuration>
                           <arguments>run build</arguments>
                       </configuration>
                   </execution>
               </executions>
           </plugin>

```

Create a source folder, install NPM, extend your PATH then use ``npm init`` to create your ``package.json`` :

```bash
mvn com.github.eirslett:frontend-maven-plugin:install-node-and-npm
export PATH=`pwd`/node:`pwd`/bin:$PATH
npm init
```

You can then install the Gridsome CLI with :

```bash
npm install --global --save @gridsome/cli
```

And create your new website :
```bash
gridsome create site
```

Happy coding 🎉🙌