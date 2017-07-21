# data_streaming
Infra de streaming des messages venant du nodemcu

## Choix technique

J'en suis à l'étude des solutions. Je n'y connais rien mais je pense me diriger vers mapR + Flink pour deux raisons :
1. J'avais vu une présentation de Tugdual Grall alias tgrall dans une session big data et ça m'a plu. C'est d'ailleurs suite à sa présentation que j'ai acheté le NodeMCU.
1. C'est conseillé pour l'IOT et c'est le but de ce projet, je pourrais certainement plus facilement trouver des exemples ou ressources sur le sujet.

NB : Depuis je suis convaincu d'utiliser flink mais au niveau de MapR, pas encore. Je vais commencer par utiliser flink en standalone puis sans doute avec elasticsearch et kibana mais bon ce n'est plus du data_streaming ça devient du data processing non?

## Quickstart

Pour commencer nous allons mettre en place une plateforme flink en standalone et lancer les exemples fournis par flink. J'aime bien voir que ça marche avant d'utiliser. En générale quand je bloque à cette étape je n'ai plus confiance dans le produit et j'abandonne. Le considérant soit trop compliqué soit trop peu fiable. C'est mon défaut et je l'assume. 

### Télechargement et installation de flink et de ses dépendances

Il s'agit de :

* flink - 
A l'heure ou j'écris ces lignes la dernière version de flink est celle-ci http://www.apache.org/dyn/closer.lua/flink/flink-1.3.1/flink-1.3.1-bin-hadoop27-scala_2.11.tgz trouvé sur la page : https://flink.apache.org/downloads.html
* java 1.8 : http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
* eventuellement scala 2.11.x
* Ils conseillent intelliJ en IDE mais ce n'est pas necessaire pour le quickstart
* maven : https://maven.apache.org/download.cgi (j'ai pris la 3.5)
* netcat (sudo apt-get install netcat depuis debian, yum install netcat depuis redhat)

Il suffit de les détarer/dezipper et d'ajouter le rep bin de chacun de ces outils dans son PATH et ça fonctionne.

### Lancement de flink

source : https://ci.apache.org/projects/flink/flink-docs-release-1.3/quickstart/setup_quickstart.html

* si flink est dans votre PATH : ````sh start-local.sh ````
  * sinon aller dans le repertoire flink et taper : ````sh  ./bin/start-local.sh ````

* verifier qu'il est accessible via http://localhost:8081

* Lancer une socket en ecoute sur le port 9000 ```sh nc -lk 9000```

* lancer un autre terminal


### Construction du quickstart

source : https://ci.apache.org/projects/flink/flink-docs-release-1.3/quickstart/java_api_quickstart.html

* construction du projet depuis un archetype maven

```sh
mvn archetype:generate                               \
      -DarchetypeGroupId=org.apache.flink              \
      -DarchetypeArtifactId=flink-quickstart-java      \
      -DarchetypeVersion=1.3.0

```

  groupId : link.apprensemble.quickstart
	archetypId : quickstart
	version : 

* aller dans le rep quickstart et builder le projet

```sh
mvn clean install -Pbuild-jar
```

### Lancement quickstart

Etrangement ça semble tellement evident que rien n'est marqué à ce sujet...

Considerons flink dans votre PATH.

depuis le repertoire target de votre projet quickstart taper :

```sh
flink run -j quickstart-1.0-SNAPSHOT.jar -c link.apprensemble.quickstart.SocketTextStreamWordCount localhost 9000
```

Vous devriez voir un nouveau job sur la console flink (http://localhost:8081)

Retour au premier terminal et taper quelques mots puis entrer : bonjour bonjour ça flink?

dans la partie taskmanager->votre task->stdout : vous devriez voir la liste des mots tapés.

Il ya 2 progs d'exemples fournis je vous laisse regarder la doc vous saurez les lancer il suffit de remplacer SocketTextStreamWordCount par un autre nom d'exemple.

```sh
flink run -j quickstart-1.0-SNAPSHOT.jar -c link.apprensemble.quickstart.WordCount
```

Il y a également 2 template pour commencer a faire vos propre stream ou batch. C'est la dessus que nous nous appuyerons pour la suite.

C'est tout pour aujourd'hui.


## RAF

* Permettre a flink de parser les messages du nodeMCU
* Ajout d'elasticsearch + kibana

## resources

* https://tgrall.github.io/blog/2016/10/17/getting-started-with-apache-flink-and-mapr-streams/

* https://mapr.com/resources/launching-mapr-cluster-google-compute-engine/assets/launching_mapr_cluster_on_gce_4.pdf

* https://mapr.com/ebooks/intro-to-apache-flink/chapter-2-streaming-first-architecture.html#stream-first_architecture

* https://flink.apache.org/introduction.html

* https://ci.apache.org/projects/flink/flink-docs-release-1.3/quickstart/setup_quickstart.html

* https://www.elastic.co/blog/building-real-time-dashboard-applications-with-apache-flink-elasticsearch-and-kibana
