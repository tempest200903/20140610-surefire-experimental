# 20140610-surefire-experimental #

## リポジトリ ##

- https://github.com/tempest200903/20140610-surefire-experimental
- git clone https://github.com/tempest200903/20140610-surefire-experimental

## pom.xml ##

- F:\goat-pc-data\ecworkspace\20140610-surefire-experimental\pom.xml
- eclipse で生成しただけ。

    ```
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <groupId>20140610-surefire-experimental</groupId>
      <artifactId>20140610-surefire-experimental</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      <build>
        <plugins>
          <plugin>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.1</version>
            <configuration>
              <source>1.7</source>
              <target>1.7</target>
            </configuration>
          </plugin>
        </plugins>
      </build>
    </project>
    ```

## mvn test ##

- bash
- mvn test
- JUnit dependency がないので失敗。

    ```
    > -------------------------------------------------------
    >  T E S T S
    > -------------------------------------------------------
    > Running com.example.CalcTest
    > Tests run: 1, Failures: 1, Errors: 0, Skipped: 0, Time elapsed: 0.01 sec << < FAI
    > LURE!
    > com.example.CalcTest.testAdd()  Time elapsed: 0.002 sec  << < FAILURE!
    > java.lang.NoClassDefFoundError: org/junit/Assert
    >         at com.example.CalcTest.testAdd(CalcTest.java:16)
    > Caused by: java.lang.ClassNotFoundException: org.junit.Assert
    >         at java.net.URLClassLoader$1.run(URLClassLoader.java:366)
    >         at java.net.URLClassLoader$1.run(URLClassLoader.java:355)
    >         at java.security.AccessController.doPrivileged(Native Method)
    >         at java.net.URLClassLoader.findClass(URLClassLoader.java:354)
    >         at java.lang.ClassLoader.loadClass(ClassLoader.java:423)
    >         at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:308)
    >         at java.lang.ClassLoader.loadClass(ClassLoader.java:356)
    >         ... 19 more
    > 
    > 
    > Results :
    > 
    > Failed tests:   com.example.CalcTest.testAdd(): org/junit/Assert
    > 
    > Tests run: 1, Failures: 1, Errors: 0, Skipped: 0
    > 
    > [INFO] ------------------------------------------------------------------------
    > [INFO] BUILD FAILURE
    > [INFO] ------------------------------------------------------------------------
    ```

## pom.xml ##

- http://stackoverflow.com/questions/10895036/maven-cant-discover-workspace-projects-junit-other-libraries
- F:\goat-pc-data\ecworkspace\20140610-surefire-experimental\pom.xml
- JUnit dependency を追加。

    ```
    >   <dependencies>
    >     <dependency>
    >       <groupId>junit</groupId>
    >       <artifactId>junit</artifactId>
    >       <version>4.8.1</version>
    >       <scope>test</scope>
    >     </dependency>
    >   </dependencies>
    ```

## mvn test ##

- bash
- mvn test
- テスト実行している。

    ```
    > -------------------------------------------------------
    >  T E S T S
    > -------------------------------------------------------
    > Running com.example.CalcTest
    > Tests run: 1, Failures: 1, Errors: 0, Skipped: 0, Time elapsed: 0.057 sec << < FA
    > ILURE!
    > testAdd(com.example.CalcTest)  Time elapsed: 0.013 sec  << < FAILURE!
    > java.lang.AssertionError: Not yet implemented
    >         at org.junit.Assert.fail(Assert.java:91)
    >         at com.example.CalcTest.testAdd(CalcTest.java:16)
    >         at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
    >         at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.
    > java:57)
    >         at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAcces
    > sorImpl.java:43)
    >         at java.lang.reflect.Method.invoke(Method.java:601)
    >         at org.junit.runners.model.FrameworkMethod$1.runReflectiveCall(Framework
    > Method.java:44)
    >         at org.junit.internal.runners.model.ReflectiveCallable.run(ReflectiveCal
    > lable.java:15)
    >         at org.junit.runners.model.FrameworkMethod.invokeExplosively(FrameworkMe
    > thod.java:41)
    >         at org.junit.internal.runners.statements.InvokeMethod.evaluate(InvokeMet
    > hod.java:20)
    >         at org.junit.internal.runners.statements.RunBefores.evaluate(RunBefores.
    > java:28)
    >         at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRun
    > ner.java:76)
    >         at org.junit.runners.BlockJUnit4ClassRunner.runChild(BlockJUnit4ClassRun
    > ner.java:50)
    >         at org.junit.runners.ParentRunner$3.run(ParentRunner.java:193)
    >         at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:52)
    >         at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:191)
    >         at org.junit.runners.ParentRunner.access$000(ParentRunner.java:42)
    >         at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:184)
    >         at org.junit.runners.ParentRunner.run(ParentRunner.java:236)
    >         at org.apache.maven.surefire.junit4.JUnit4Provider.execute(JUnit4Provide
    > r.java:252)
    >         at org.apache.maven.surefire.junit4.JUnit4Provider.executeTestSet(JUnit4
    > Provider.java:141)
    >         at org.apache.maven.surefire.junit4.JUnit4Provider.invoke(JUnit4Provider
    > .java:112)
    >         at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
    >         at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.
    > java:57)
    >         at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAcces
    > sorImpl.java:43)
    >         at java.lang.reflect.Method.invoke(Method.java:601)
    >         at org.apache.maven.surefire.util.ReflectionUtils.invokeMethodWithArray(
    > ReflectionUtils.java:189)
    >         at org.apache.maven.surefire.booter.ProviderFactory$ProviderProxy.invoke
    > (ProviderFactory.java:165)
    >         at org.apache.maven.surefire.booter.ProviderFactory.invokeProvider(Provi
    > derFactory.java:85)
    >         at org.apache.maven.surefire.booter.ForkedBooter.runSuitesInProcess(Fork
    > edBooter.java:115)
    >         at org.apache.maven.surefire.booter.ForkedBooter.main(ForkedBooter.java:
    > 75)
    > 
    > 
    > Results :
    > 
    > Failed tests:   testAdd(com.example.CalcTest): Not yet implemented
    > 
    > Tests run: 1, Failures: 1, Errors: 0, Skipped: 0
    > 
    > [INFO] ------------------------------------------------------------------------
    > [INFO] BUILD FAILURE
    > [INFO] ------------------------------------------------------------------------
    > [INFO] Total time: 1.768s
    > [INFO] Finished at: Tue Jun 10 23:51:09 JST 2014
    > [INFO] Final Memory: 8M/245M
    > [INFO] ------------------------------------------------------------------------
    ```

## CalcTest.java ##

- F:\goat-pc-data\ecworkspace\20140610-surefire-experimental\src\test\java\com\example\CalcTest.java
- システムプロパティを読み取る。

    ```
    > @Test
    > 	public void testAdd() {
    > 		String option = System.getProperty("option");
    > 		System.out.println("option =: " + option);
    > 		fail("Not yet implemented");
    > 	}
    ```

## pom.xml ##

- システムプロパティを与える。
- http://maven.apache.org/surefire/maven-surefire-plugin/examples/system-properties.html
- F:\goat-pc-data\ecworkspace\20140610-surefire-experimental\pom.xml

    ```
    > </build>
    >     <plugins>
    >       <plugin>
    >         <groupId>org.apache.maven.plugins</groupId>
    >         <artifactId>maven-surefire-plugin</artifactId>
    >         <version>2.17</version>
    >         <configuration>
    >           <systemPropertyVariables>
    >             <option>value12345</option>
    >           </systemPropertyVariables>
    >         </configuration>
    >       </plugin>
    >     </plugins>
    >   </build>
    ```

## mvn test ##

    ```
    > -------------------------------------------------------
    >  T E S T S
    > -------------------------------------------------------
    > Running com.example.CalcTest
    > option =: value12345
    ```

## mvn システムプロパティで直接値を渡す ##

- F:\goat-pc-data\ecworkspace\20140610-surefire-experimental\pom.xml

    ```
    > <systemPropertyVariables>
    >             <option>value12345 ${surefire_option} ${basedir}</option>
    >           </systemPropertyVariables>
    ```
## mvn test ##

- mvn -Dsurefire_option=commandline test

    ```
    option =: value12345 commandine F:\goat-pc-data\ecworkspace\20140610-surefire-experimental
    ```

- mvn コマンドラインで指定した値がそのまま反映された。
- git mvn システムプロパティで直接値を渡す

## プロファイル ##

- 値が多数ある場合は、プロファイルを使うとよいだろう。
- http://www.techscore.com/tech/Java/ApacheJakarta/Maven/6/

