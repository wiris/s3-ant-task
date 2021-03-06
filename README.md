s3-ant-task
===========

Ant Task For amazon S3. That allows you to delete and upload a directory.

Using with ant
------------------
```xml
<?xml version="1.0"?>
<project name="Clover.Designer" default="build-all" basedir=".">
    <target name="upload-s3">
     <path id="tasks.path">
        	    <fileset dirs="lib" includes="*.jar"/>
    	    </path>
    	 <taskdef resource="org/mule/ant/tasks.properties" classpathref="tasks.path"/>
        <s3delete endpoint="s3.amazonaws.com" key="${aws.key}" secret="${aws.secret}" bucket="${s3.bucket}" dirs="3.5"/>
        <s3upload endpoint="s3.amazonaws.com" key="${aws.key}" secret="${aws.secret}" bucket="${s3.bucket}" dest="3.5" contentType="application/x-whatever">
            <!-- fileset structure -->
    	    <fileset dirs="${basedir}/target/artifact"/>
		</s3upload>
	</target>
</project>
```

Using with maven
--------------

```xml
<plugin>
    <inherited>false</inherited>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-antrun-plugin</artifactId>
    <executions>
        <execution>
            <id>remote-deploy</id>
            <phase>install</phase>
            <configuration>
                <tasks>
                    <taskdef resource="org/mule/ant/tasks.properties" classpathref="maven.plugin.classpath"/>
                    <s3delete endpoint="s3.amazonaws.com" key="${aws.key}" secret="${aws.secret}" bucket="${s3.bucket}" dir="3.5"/>
                    <s3delete endpoint="s3.amazonaws.com" key="${aws.key}" secret="${aws.secret}" bucket="${s3.bucket}" >
                        <element name="images"/>
                        <element name="fonts"/>
                    </s3delete>
                   <s3upload endpoint="s3.amazonaws.com" key="${aws.key}" secret="${aws.secret}" bucket="${s3.bucket}" dest="3.5" contentType="application/x-whatever">
        	<!-- fileset structure -->
    		         <fileset dirs="${basedir}/target/artifact"/>
		           </s3upload>

                </tasks>
            </configuration>
            <goals>
                <goal>run</goal>
            </goals>
        </execution>
    </executions>
    <dependencies>
        <dependency>
             <groupId>org.mule</groupId>
            <artifactId>s3-ant-tasks</artifactId>
            <version>0.1-SNAPSHOT</version>
        </dependency>
        <dependency>
            <groupId>org.apache.ant</groupId>
            <artifactId>ant</artifactId>
            <version>1.7.1</version>
        </dependency>
        <dependency>
            <groupId>org.apache.ant</groupId>
            <artifactId>ant-jsch</artifactId>
            <version>1.7.1</version>
        </dependency>
    </dependencies>
</plugin>
```


