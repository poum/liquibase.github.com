---
layout: default
title: Démarrage rapide avec Liquibase
---
## Étape 1: Créer un fichier Changelog: ##

Le [fichier de changelog de la base de données](documentation/fr/databasechangelog.html) est l'endroit où toutes les modifications de la base de données sont listées. Il est au format XML, donc commençons avec un fichier XML vide:

{% highlight xml %}
<?xml version="1.0" encoding="UTF-8"?>

<databaseChangeLog
  xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog
         http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.1.xsd">

</databaseChangeLog>
{% endhighlight %}

## Étape 2: Ajouter un ChangeSet ##

Chaque [ensemble de modifications](documentation/fr/changeset.html) est identifié de manière unique par un attribut "id" et un attribut "author". Ces deux marqueurs, associés au nom et au paquet du fichier changelog identifient de manière unique la modification. Si on s'était limité au seul "id" à indiquer, il aurait été trop facile de le dupliquer accidentellement, notamment quand on doit gérer plusieurs développeurs et branches de code. Inclure un attribut "author" minimise les risques de doublons. 

Pensez à chaque change set comme une modification atomique que vous voulez appliquer à votre base de données. Il est habituellement préférable de n'inclure qu'une seule modification dans votre change set, mais il est autorisé et il peut faire sene d'en mettre davantage si vous insérez plusieurs lignes qui doivent être ajoutées comme une unique transaction. Liquibase tentera d'exécuter chaque ensemble de modification comme une unique transaction mais plusieurs bases de données vont finaliser silencieusement et reprendre les transactions pour certaines commandes (create table, drop table, etc.)

{% highlight xml %}
<?xml version="1.0" encoding="UTF-8"?>

<databaseChangeLog
  xmlns="http://www.liquibase.org/xml/ns/dbchangelog"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog
         http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.1.xsd">

    <changeSet id="1" author="bob">
        <createTable tableName="department">
            <column name="id" type="int">
                <constraints primaryKey="true" nullable="false"/>
            </column>
            <column name="name" type="varchar(50)">
                <constraints nullable="false"/>
            </column>
            <column name="active" type="boolean" defaultValueBoolean="true"/>
        </createTable>
    </changeSet>

</databaseChangeLog>
{% endhighlight %}

## Étape 3: Exécuter le ChangeSet ##

Il y a de nombreuses manières d'exécuter votre journal de modifications dont [la ligne de commandes](documentation/fr/command_line.html), [Ant](documentation/fr/ant/index.html), [Maven](documentation/fr/maven/index.html), [Spring](documentation/fr/spring.html), un [servlet listener](documentation/fr/servlet_listener.html) et un [environnement CDI](documentation/fr/cdi.html).

Voici un exemple pour mysql via jdbc:

{% highlight bat %}
liquibase --driver=com.mysql.jdbc.Driver \
     --classpath=/path/to/classes \
     --changeLogFile=com/example/db.changelog.xml \
     --url="jdbc:mysql://localhost/example" \
     --username=user \
     --password=asdf \
     migrate
{% endhighlight %}

Il a beaucoup plus de bases de données prises en charge par liquibase. Pour en avoir la liste et quel pilote jdbc, quelle URL, quel chemin d'accès, etc. utiliser avec, voir la section [bases de données](databases.html).

## Étape 4: Contrôler votre base de données ##

Vous verrez que votre base de données contient désormais une table appelée "department". Deux autres tables ont également été créees: 'databasechangelog" et "databasechangeloglock". La table "databasechangelog" contient une liste de toutes les instructions qui ont été exécutées dans la base de données. La table databasechangeloglock est utilisée pour s'assurer que deux machines ne tentent pas de modifier la base de données en même temps.

## Étapes suivantes ##

* Ce guide de démarrage rapide est conçu pour vous aider à démarrer avec Liquibase. Pour une description complète de tout ce qu'il peut faire, voir [le manuel Liquibase](documentation/fr/index.html), lisez [les meilleures pratiques](bestpractices_fr.html) et visitez les [forums](community/fr/index.html). 
* Si vous avez un projet déjà existant et que vous voulez également y ajouter Liquibase, visitez la page [projet existant](documentation/fr/existing_project.html).
* Si vous êtes intéressé par un support commercial, des formations ou une prestation de consultant, voyez [datical.com](http://www.datical.com/liquibase/).

