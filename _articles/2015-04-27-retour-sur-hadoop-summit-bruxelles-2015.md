---
ID: 388
post_title: Retour sur Hadoop Summit Bruxelles 2015
author: Arnaud Cogoluègnes
post_date: 2015-04-27 14:30:00
post_excerpt: |
  <p><a href="http://2015.hadoopsummit.org/brussels/">Hadoop Summit</a> est LA conférence Hadoop en Europe à ne pas rater et Zenika y était. Avec plus de 1300 participants et jusqu'à 7 sessions en parallèle, les amateurs de big data sont sûrs de ne pas s'ennuyer. Nous vous proposons un retour sur les sessions que nous avons suivies lors de cet événement exceptionnel.</p> <p><img src="/public/2015-04-hadoop-summit-bruxelles/hadoop_summit_logo.png" alt="Hadoop Summit 2015" title="Hadoop Summit 2015" /></p>
layout: post
permalink: >
  http://blog.zenika-offres.com/retour-sur-hadoop-summit-bruxelles-2015/
published: true
slide_template:
  - default
---
<a href="http://2015.hadoopsummit.org/brussels/">Hadoop Summit</a> est LA conférence Hadoop en Europe à ne pas rater et Zenika y était. Avec plus de 1300 participants et jusqu'à 7 sessions en parallèle, les amateurs de big data sont sûrs de ne pas s'ennuyer. Nous vous proposons un retour sur les sessions que nous avons suivies lors de cet événement exceptionnel.

NB : les slides des présentations seront disponibles sur <a href="http://fr.slideshare.net/Hadoop_Summit">Slideshare</a>
<h3>Keynote du 15 avril 2015</h3>
<strong>Par Rob Bearden (Hortonworks), Mike Gualtieri (Forrester Research), T.K. "Ranga" Rengarajan (Microsoft), Arun Murthy (Hortonworks), Irfan Khan (SAP), John Iley (Formula One Racing)</strong>

Lors de cette keynote, les différents intervenants ont insisté sur l'importance des données et la carte à jouer que les technologies Hadoop ont dans le traitement et la gouvernance de ces immenses volumes de données. Plusieurs retours d'expérience ont été présentés, et pas seulement chez les "grands" du web.

<strong>A retenir :</strong> Hadoop et son écosystème sont en passe de devenir "mainstream", car ils sont maintenant beaucoup plus accessibles. A noter aussi, la création de la plateforme Hadoop commune ODP (Open Data Platform), qui sera le socle commun des distributions Hadoop de Hortonworks et de Pivotal.
<h3>Apache Tez - Present and future</h3>
<strong>Par Jeff Zhang (Hortonworks), Rajesh Balamohan (Hortonworks)</strong>

Tez est un moteur d'exécution distribué ; pour faire simple, une version 2 de MapReduce sur Hadoop. Plus puissant, flexible et surtout plus rapide que MapReduce, il tourne déjà sous le capot de Hive et de Pig. Avec Tez, des traitements complexes comme des jointures ou des tris s'exécutent beaucoup plus rapidement qu'en MapReduce traditionnel. Les raisons : moins d'IO réseau et sur HDFS, moins de jobs générés. Pour certains traitements, les traitements sont 100 fois plus rapide qu'en MapReduce. Tez est en cours de développement, mais ces API sont stables et les équipes de développement continuent de l'améliorer.

<strong>A retenir :</strong> Tez devient le moteur d'exécution pour de plus en plus d'outils (Hive, Pig, Cascading). Même si MapReduce n'est pas amené à disparaître immédiatement, il est clair que nous sommes maintenant dans une deuxième génération d'outils (Tez, Spark, Flink).
<h3>Hive now Sparks</h3>
<strong>Par Xuefu Zhang (Cloudera), Rui Li (Intel)</strong>

Voir les <a href="http://fr.slideshare.net/Hadoop_Summit/hive-now-sparks">slides</a>

Après MapReduce et Tez, Hive peut maintenant fonctionner sous Spark ! Cette initiative est récente, mais donne de bons résultats d'après ses créateurs. L'idée est donc de combiner Hive et Spark pour avoir du SQL exécuté parrallélement sur Hadoop. Les intervenants ont présenté des benchmarks entre MapReduce, Tez et Spark. MapReduce est bien sûr bien plus lent, tandis que Tez et Spark sont très proches. Tez sur Hive a encore une petite longueur d'avance sur certains types de requêtes, car il dispose d'optimisations pas encore implémentées dans Hive sur Spark.

<strong>A retenir :</strong> Encore une tentative de SQL sur Hadoop, avec deux poids lourds de l'écosystème, Hive et Spark. Des débuts prometteurs, à suivre.
<h3>The missing piece in Big Data Security: HDFS Encryption at Rest</h3>
<strong>Par Charles Lamb (Cloudera), Andrew Wang (Cloudera)</strong>

Les 2 ingénieurs de Cloudera ont présenté une solution d'encryptage au niveau HDFS. Cette solution est transparente pour les applications, elle demande par contre l'installation de serveurs supplémentaires pour notamment gérer la distribution de clés de cryptage. L'idée est que seule l'application puisse vraiment lire et écrire les fichiers et pas l'administrateur du serveur de clés, ni l'administrateur HDFS. L'encryptage a un impact sur les performances, mais tout à fait acceptable (7,5 % en lecture, négligeable en écriture). Ces tests ont été effectués avec des processeurs Intel qui disposent de l'extension AES-NI (à noter que Intel est le principal investisseur dans Cloudera).

<strong>A retenir :</strong> la sécurité dans Hadoop est un sujet récurrent. Peut-être un signe de maturité de ces technologies.
<h3>Architecting a scalable Hadoop platform: top 10 considerations for success</h3>
<strong>Par Sumeet Singh (Yahoo)</strong>

Fort de son expérience Hadoop chez Yahoo (qui dispose de clusters Hadoop de plusieurs milliers de noeuds), Sumeet Singh cite les éléments clés pour réussir avec Hadoop. Citons notamment le choix de l'infrastructure (cloud ou chez soi), le réseau (il a particulièrement insisté sur ce point qui est souvent omis), la sécurité (encore), la gouvernance et l'intégration avec les autres systèmes (notamment pour les partenariats avec des entreprises qui fournissent des données à Yahoo). Il en a aussi profité pour tordre le cou à certains mythes ("debunking myths"), comme le fameux "Hadoop is dead".

<strong>A retenir :</strong> Yahoo nous fait profiter de son expérience sur Hadoop. C'est tout à son intérêt, étant un des gros sponsors du projet.
<h3>Guideline for productive full stack engineers</h3>
<strong>Par Rafal Wojdyla (Spotify)</strong>

Spotify maintient un cluster d'environ 1300 noeuds. L'intervenant est administrateur du cluster, il insiste sur l'importance de l'automatisation (avec des outils comme Ambari ou Cloudera Manager). Coté développement, Spotify a commencé avec Hadoop Streaming pour pouvoir développer en Python. Cette solution s'est révélée finalement loin d'être parfaite (lenteur et fiabilité) et ils sont ensuite passés à du Java avec Apache Crunch et Cascading, ainsi que Pig et Hive. Les frameworks type API (Crunch, Cascading) se sont avérés un meilleur choix que Hadoop Crunching. En plein engouement autour de Spark, Spotify avoue l'avoir black-listé pour l'instant, suite à des résultats décevants sur des jeux de données importants (environ 1 To de données en shuffling).

<strong>A retenir :</strong> un retour intéressant d'une société qui a remporté un grand succès grâce à Hadoop.
<h3>Implementing the Lambda architecture efficiently with Apache Spark</h3>
<strong>Par Michael Hausenblas (MapR)</strong>

Avec un titre pareil, impossible de rater le call for papers d'une conférence Big Data ! L'intervenant revient sur l'architecture Lambda (un livre, des couches, des technologies) et la possibilité de l'implémenter avec Spark (pour la couche batch) et Spark Streaming (pour la couche speed).

<strong>A retenir :</strong> une session un peu pépère, puisqu'une rapide recherche sur l'architecture Lambda et un tutorial sur Spark ferait aussi bien que le contenu de la présentation. On attend mieux d'une société comme MapR. On risque cependant d'appliquer les techniques de l'architecture Lambda dans les années à venir.
<h3>ORC 2015: Faster, better, smaller</h3>
<strong>Par Gopal Vijayaraghavan (Hortonworks)</strong>

ORC signifie "Optimized Row Columnar", il s'agit d'un format de fichiers utilisé principalement dans Hive. Les formats orientés colonnes comme Parquet ou ORC sont particulièrement adaptés lorsque que l'on souhaite ne lire qu'une partie des champs d'un jeu de données. C'est aussi via ORC que des fonctionnalités avancées de Hive (update, transactions) sont implémentées. Facebook a par exemple économisé 1400 serveurs de stockage en passant des données sous ORC (optimisation de stockage et de compression). Spotify a diminué l'utilisation CPU d'un facteur de 32 et fait 16 fois moins d'IO en lecture en étant passé de Avro à ORC. ORC n'est pas une balle d'argent, mais est simplement plus adapté à certains cas d'usage, il n'est par exemple pas adapté des structures organisées en arbres.

<strong>A retenir :</strong> ORC fait partie de l'initiative Stinger, tout comme Tez. L'idée est de faire passer le temps de réponse de Hive en dessous de la seconde. Les améliorations annoncées sont impressionnantes et l'équipe Hortonworks touche au but. ORC est pour l'instant défini directement dans Hive, mais il va devenir un projet Apache "top-level" dans les mois qui viennent. ORC deviendra plus facile à intégrer dans d'autres outils.
<h3>Docker based Hadoop provisioning</h3>
<strong>Par Jan
os Matyas (SequenceIQ)</strong>

Janos présente Cloudbreak, "Hadoop as a service API". L'idée est de pouvoir déployer des clusters Hadoop avec le moins de configuration possible, à partir de blueprint. Cloudbreak est basé sur des technologies Hadoop classiques (Ambari), mais aussi des outils très en vogue dans le monde DevOps : Docker (container), Swarm (clustering pour Docker) et Consul (DNS, service discovery, serveur de configuration). Un outil très jeune, basée sur des technos... jeunes. Mais la valeur n'attend pas le nombre des années comme dit l'autre.

<strong>A retenir :</strong> Le produit de cette startup qu'Hortonworks vient de racheter se propose de rendre le déploiement de clusters Hadoop aussi simple qu'un click. A suivre.
<h3>Real insights, Real-time : bridging batch and real-time systems for anomaly detection</h3>
<strong>Par <a href="https://twitter.com/costinl">Costin Leau</a> (Elastic)</strong>

Costin nous présente une solution utilisant des composants tels que Elasticsearch, Hadoop et Spark pour détecter les données pertinentes dans les énormes flux de données à traiter. Le challenge consiste à écarter le bruit et détecter ce qui n'est pas commun pour analyser le plus finement possible les anomalies. L'architecture proposée se base sur l'utilisation d'Elastic+Spark+Hadoop permettant à la fois des analyses en temps réel (idéal pour prévenir les fraudes avant qu'elles n'arrivent) et en mode batch.

<strong>A retenir :</strong> Spark remplace Storm dans une <a href="https://speakerdeck.com/elasticsearch/real-time-analytics-and-anomalies-detection-using-elasticsearch-hadoop-and-storm">ancienne présentation</a> de Costin, est-ce un message ?
<h3>Protecting Enterprise Data in Hadoop</h3>
<strong>Par <a href="https://twitter.com/owen_omalley">Owen O'Malley</a> (Hortonworks)</strong>

Owen rappelle les règles de base de la sécurité d'un cluster Hadoop :
<ul>
	<li>sur un petit cluster, un firewall est suffisant pour commencer
<ul>
	<li>Knox fournit une gateway http</li>
</ul>
</li>
	<li>se reposer sur les utilisateurs du cluster et leurs permissions
<ul>
	<li>il faut éviter les répertoires avec des droits en 777 !</li>
	<li>il faut minimiser l'espace des utilisateurs</li>
	<li>il faut utiliser les ACLs etc.</li>
	<li>à lire : <a href="http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html">HDFS Permissions Guide</a></li>
</ul>
</li>
	<li>utiliser HDFS encryption</li>
</ul>
Anecdote : le cluster de Facebook n'est pas protégé ! C'est certainement la raison pour laquelle, dans Hive (qui vient de FB), la sécurité fut longtemps absente ou presque (sur d'anciennes versions, on peut s'accorder soit-même tous les droits!)

<strong>A retenir :</strong> souvent pour de mauvaises raisons, on voit des clusters ouverts à tout vent, car c'est plus simple à gérer, il est donc important de rappeler des règles simples à mettre en oeuvre pour sécuriser les données d'un cluster.
<h3>Building scalable event detection pipelines with Apache Kafka</h3>
<strong>Par <a href="https://twitter.com/jeffholoman">Jeff Holoman</a> (Cloudera)</strong>

Présentation d'une architecture basée sur Kafka pour la détection d'événements. Une introduction à ce genre de traitement est disponible sur le <a href="http://blog.cloudera.com/blog/2014/11/flafka-apache-flume-meets-apache-kafka-for-event-processing/">blog de Cloudera</a>

<strong>A retenir :</strong>
<ul>
	<li>pour la sérialisation des données, préférez <a title="Avro" href="Avro">Avro</a>(http://avro.apache.org/) à JSON</li>
	<li>pour Kafka, développez une lib de producer/consumer qui évite aux développeurs de réinventer la roue</li>
	<li>utilisez Flume pour l'ingestion des données (dans HBase ou HDFS)</li>
</ul>
<h3>Beyond the tweeting toaster : IoT streaming analytics with Apache Storm, Kafka and Arduino</h3>
<strong>Par <a href="https://twitter.com/ptgoetz">P.Taylor Goetz</a> (Hortonworks)</strong>

Voir les <a href="https://speakerdeck.com/ptgoetz/beyond-the-tweeting-toaster-iot-analytics-with-apache-storm-kafka-and-arduino-1">slides</a>

Constat : il y aura 26 milliards d'objets connectés d'ici 2020 et les capteurs s(er)ont partout : téléphones, voitures, bracelets, ... Il n'y pas de limite aux cas d'utilisation ! Le speaker présente un exemple d'architecture de traitement de données venant de capteurs basée sur Kafka et Storm (pour la couche analyse).

<strong>A retenir :</strong> l'IoT est un sujet majeur des années à venir et les chaînes de traitement des données venant de ces objets restent à définir, même si on perçoit que Kafka (ou tout autre système de queues), Storm (ou tout autre système de traitement massivement parallèle) et HDFS (ou tout autre stockage de masse) sont les éléments incontournables de ce futur.
<h3>Real-time stream processing with Apache Flink</h3>
Par Marton Balassi (Data Artisans) et Gyula Fora (SICS) Voir les <a href="http://fr.slideshare.net/GyulaFra/flink-streaming-hadoopsummit">slides</a>

Présentation d'<a href="https://flink.apache.org/">Apache Flink</a> un moteur de traitement de données, que l'on peut placer comme concurrent à Storm ou Spark.

A retenir : malgré son manque de visiblité vis-à-vis de ses principaux concurrents, Flink est à suivre !
<h3>Driving enterprise data governance for big data systems through Apache Falcon</h3>
<strong>Par Srikanth Sundarrajan et Naresh Agarwal (InMobi)</strong>

Ce talk présentait les concepts du projet <a href="http://falcon.apache.org/">Apache Falcon</a>. Il s'agit d'un framework dédié à l'orchestration des traitements des données dans des clusters Hadoop : il permet à ses utilisateurs de définir les actions à réaliser sur leurs données (mouvement des données, traitements, ...). Ce framework repose notamment sur Oozie pour la partie scheduling et HCatalog pour les metadata.

<strong>A retenir :</strong> si ce genre de framework s'avère indispensable dans une entreprise pour la gouvernance des données, il devra s'équiper de clients haut niveau pour s'adresser au plus grand nombre.
<h3>How (the Internet of) Things are turning the Internet upside down</h3>
Par <a href="https://twitter.com/ted_dunning">Ted Dunning</a> (MapR) Voir les <a href="http://fr.slideshare.net/tdunning/how-the-internet-of-things-is-turning-the-internet-upside-down">slides</a>

Ted Dunning évoque le fait que l'IoT change l'architecture d'Internet : nous passons d'un monde où les données allaient des serveurs (peu nombreux) vers des clients (nombreux) à un monde où les objets (très nombreux) envoient leurs données vers des serveurs. De plus, suite à cette acquisition de données, il est alors nécessaire de stocker et d'analyser ces données qui sont essentiellement des time series. Ted évoque la solution <a href="http://opentsdb.net/">OpenTSDB</a>, base de données reposant sur HBase dédiée à la gestion de time series. OpenTSDB offre une API et des outils de base pour insérer et lire des données typées time series et qui se définissent par le tuple (nom de la métrique, timestamp, valeur, ensemble de paires clé/valeur décrivant la time serie à laquelle appartient la valeur). Une communauté existe et fournit des <a href="http://opentsdb.net/docs/build/html/resources.html#clients">clients plus évolués</a> pour OpenTSDB.

<strong>A retenir :</strong>
<ul>
	<li>une belle histoire sur le partage des données de navigation aux XIXème siècle</li>
	<li>OpenTSDB : gardons un oeil dessus...</li>
</ul>
<h3>Security needs in Hadoop's current and future - How Apache Ranger can help ?</h3>
<strong>Par Balaji Ganesan et Don Bosco Durai (Hortonworks)</strong>

Présentation d'Apache Ranger, un projet encore en incubation. Il se veut le point central de la gestion de la sécurité (autorisation, audit) d'un cluster Hadoop. Au travers de plugins, il peut gérer la séc
urité de HDFS, Hive, HBase, ...

<strong>A retenir :</strong> l'initiative est intéressante et mérite d'être suivie (cela mériterait peut-être d'être intégré à Ambari)
<h3>Conclusion</h3>
Le nombre de participants à cette conférence et le niveau des interventions montrent la bonne santé des technologies Hadoop. Outre la couverture de sujets techniques et d'outils de traitement de données (par exemple Spark, Flink), on notera l'attention portée aux sujets de la gouvernance des données et de la sécurité.

<em>Article co-écrit par Bruno Bonnin et Arnaud Cogoluègnes</em>.