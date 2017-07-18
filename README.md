# data_streaming
Infra de streaming des messages venant du nodemcu

## Choix technique

J'en suis à l'étude des solutions. Je n'y connais rien mais je pense me diriger vers mapR + Flink pour deux raisons :
1. J'avais vu une présentation de Tugdual Grall alias tgrall dans une session big data et ça m'a plu. C'est d'ailleurs suite à sa présentation que j'ai acheté le NodeMCU.
1. C'est conseillé pour l'IOT et c'est le but de ce projet, je pourrais certainement plus facilement trouver des exemples ou ressources sur le sujet.

NB : Depuis je suis convaincu d'utiliser flink mais au niveau de MapR, pas encore. Je vais commencer par utiliser flink en standalone puis sans doute avec elasticsearch et kibana mais bon ce n'est plus du data_streaming ça devient du data processing non?

## resources

* https://tgrall.github.io/blog/2016/10/17/getting-started-with-apache-flink-and-mapr-streams/

* https://mapr.com/resources/launching-mapr-cluster-google-compute-engine/assets/launching_mapr_cluster_on_gce_4.pdf

* https://mapr.com/ebooks/intro-to-apache-flink/chapter-2-streaming-first-architecture.html#stream-first_architecture

* https://flink.apache.org/introduction.html

* https://ci.apache.org/projects/flink/flink-docs-release-1.3/quickstart/setup_quickstart.html

* https://www.elastic.co/blog/building-real-time-dashboard-applications-with-apache-flink-elasticsearch-and-kibana
