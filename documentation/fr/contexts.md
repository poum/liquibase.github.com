---
layout: default
title: Contextes
---

# Contextes #

Les "Contextes" dans Liquibase sont des étiquettes que vous pouvez ajouter aux changeSets pour déterminer lesquels seront exécutés pour toute exécution de migration particulière. N'importe quelle chaîne de caractères peut être utilisée comme nom de contexte et elles sont contrôlées sans tenir compte de la casse.

Quand vous exécutez le migrateur via l'une des méthodes disponibles, vous pouvez lui passer une série de contextes à exécuter. Seuls les changeSets marqués avec les contextes qui auront été passés seront exécutés.

Si vous n'affectez pas de contexte à un changeSet, il sera exécuté tout le temps, quels que soient les contextes que vous aurez passés au migrateur.

Si vous n'indiquez pas de contexte quand vous exécutez le migrateur, TOUS les contextes seront exécutés.

Voici un exemple de change set utilisant l'attribut contexte:
{% highlight xml %}
   <changeSet id="2" author="bob" context="test">
        <insert tableName="news">
            <column name="id" value="1"/>
            <column name="title" value="Liquibase 0.8 Released"/>
        </insert>
        <insert tableName="news">
            <column name="id" value="2"/>
            <column name="title" value="Liquibase 0.9 Released"/>
        </insert>
    </changeSet>
{% endhighlight %}

## Syntaxe des contextes ##

Les contextes peuvent être indiqués en utilisant AND, OR, ! et des parenthèses. Sans parenthèses, l'ordre des opérations sont "!" puis "AND" puis "OR".

__Exemples:__

 * context="!test"
 * context="v1.0 or map"
 * context="v1.0 or map"
 * context="!qa and !master"

 Utiliser une "," pour séparer des contextes fonctionne comme une opération OR mais avec la précédence la plus élevée.

 __Exemples:__

  * "test, qa" est identique à "test OR qa"
  * "test, qa and master" est identique à "(test) OR (qa and master)

__Disponibilité:__

* le séparateur "," est disponible pour toutes les versions de Liquibase
* "AND, OR, !, parenthèses" ajoutés dans la 3.2.0


## Utiliser des contextes pour des données de test ##

Si vous gérez vos données de test avec Liquibase, le meilleur moyen de les inclure est de le faire en même temps que vos autres changeSets mais en les marquant avec contexte "test". De cette façon, quand vous voulez que vos données de test soient insérées, vous pouvez exécuter le migrateur avec le contexte "test". Quand vient le moment de migrer votre base de données de production, n'incluez pas le contexte "test" et vos données de test ne seront pas incluses. Si vous avez plusieurs environnements de test ou plusieurs ensembles de données de test, marquez les simplement avec différents contextes tels que "min-test", "integration-test", etc.

Utiliser des contextes pour contrôler des données de test est mieux que de les avoir dan un arbre de changelog séparé car des refactorisations ultérieures et des modifications seront appliquées aux données de test existantes comme elles seront appliquées aux données de production. Si vous avez un ensemble de données de test qui ont été crées et simplement ajoutées après que la base de données a été configurée, vous devrez continuellement mettre à jour manuellement vos scripts de données de test pour les garder synchronisés avec le schéma actuel de base de données.

## Utiliser des contextes pour des change logs multi bases de données ##

Vous pouvez utiliser des contextes pour contrôler quels change sets seront appliqués à quelles bases de données, mais la meilleure option est d'utiliser l'étiquette "dbms" come étiquette du changeSet.
