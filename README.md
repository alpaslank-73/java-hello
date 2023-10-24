java-hello-world-webapp
=======================
A simple java web app
=======================
Apache Maven ile deploy etmek icin:

$ oc new-project myproject
$ git clone https://github.com/alpaslank-73/java-hello
$ cd java-hello

deploymenyconfig yerine deployment yaratilmasi icin:

$ vim pom.xml
..  <properties>
    <jkube.build.switchToDeployment>true</jkube.build.switchToDeployment>
  </properties>
  <dependencies>
ekliyorsun ve plugin olarak da openshift-maven-plugin ekliyorsun:
...
    <plugins>
      <plugin>
        <groupId>org.eclipse.jkube</groupId>
        <artifactId>openshift-maven-plugin</artifactId>
        <version>1.2.0</version>
      </plugin>
    </plugins>
  </build>
</project>

$ mvn -DskipTests package oc:build oc:resource ==> dediginde paketleme islemi yapiliyor, build gerceklesiyor ve target/classes/META-INF/jkube/openshift/ altinda deployment, service, route yaml file'lar yaratiliyor. Istenirse deployment oncesinde bu file'lar customize edilebilir (orn: deployment'taki replica adedi veya route'daki host bolumu).

$ oc get pod

En son deploy etmek icin:

$ mvn -DskipTests oc:deploy
$ oc get pod
$ oc get route
