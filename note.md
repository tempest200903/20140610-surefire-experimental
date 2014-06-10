# 20140610-surefire-experimental #

## リポジトリ ##

- https://github.com/tempest200903/20140610-surefire-experimental
- git clone https://github.com/tempest200903/20140610-surefire-experimental

## pom.xml 最小限 ##

- eclipse で生成してから、 dependency junit を追加した。
- F:\goat-pc-data\ecworkspace\20140610-surefire-experimental\pom.xml

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

## mvn test 実行結果 ##

- bash
- mvn test
- テスト実行している。

    ```
    > -------------------------------------------------------
    >  T E S T S
    > -------------------------------------------------------
    > Results :
    > 
    > Failed tests:   testAdd(com.example.CalcTest): Not yet implemented
    > 
    > Tests run: 1, Failures: 1, Errors: 0, Skipped: 0
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

## pom.xml にシステムプロパティを固定値で記す ##

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

## mvn test 実行結果 ##

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
## mvn test 実行結果 ##

- mvn -Dsurefire_option=commandline test
    - option =: value12345 commandine F:\goat-pc-data\ecworkspace\20140610-surefire-experimental
- mvn コマンドラインで指定した値がそのまま反映された。
- git commit -m "mvn システムプロパティで直接値を渡す"

## pom.xml にプロファイルを記す ##

- 値が多数ある場合は、プロファイルを使うとよいだろう。
- http://www.techscore.com/tech/Java/ApacheJakarta/Maven/6/
- http://javatechnology.net/other/maven-profiles/

## mvn test 実行結果 ##

- mvn test
  - option =: value12345 ${surefire_option}
- mvn -Pprofile_alpha test
  - option =: value12345 alpha_value
- mvn -Pprofile_beta test
  - option =: value12345 beta_value

## maven plugin version ##

- mvn test site
- file:///F:/goat-pc-data/ecworkspace/20140610-surefire-experimental/target/site/plugins.html

    > Project Build Plugins
    > GroupId	ArtifactId	Version
    > org.apache.maven.plugins	maven-clean-plugin	2.5
    > org.apache.maven.plugins	maven-compiler-plugin	3.1
    > org.apache.maven.plugins	maven-deploy-plugin	2.7
    > org.apache.maven.plugins	maven-install-plugin	2.4
    > org.apache.maven.plugins	maven-jar-plugin	2.4
    > org.apache.maven.plugins	maven-resources-plugin	2.6
    > org.apache.maven.plugins	maven-site-plugin	3.3
    > org.apache.maven.plugins	maven-surefire-plugin	2.17

## maven version ##

    > # mvn --version
    > Apache Maven 3.1.1 (0728685237757ffbf44136acec0402957f723d9a; 2013-09-18 00:22:2
    > 2+0900)
    > Maven home: C:\tool\Maven\apache-maven-3.1.1
    > Java version: 1.7.0_17, vendor: Oracle Corporation
    > Java home: C:\tool\Java\jdk1.7.0_17\jre
    > Default locale: ja_JP, platform encoding: MS932
    > OS name: "windows 7", version: "6.1", arch: "amd64", family: "windows"

