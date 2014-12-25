---
layout: default
title: Accueil
---

<div class="container">
<div class="span-10 append-1">

<h2>Construire des Changelogs</h2>
<ul>
<li><a href="databasechangelog.html">Fichiers Changelog</a>
<ul>
    <li><a href="xml_format.html">Format XML</a></li>
    <li><a href="yaml_format.html">Format YAML</a></li>
    <li><a href="json_format.html">Format JSON</a></li>
    <li><a href="sql_format.html">Format SQL</a></li>
    <li><a href="other_formats.html">Autres formats</a></li>
</ul></li>
<li><a href="changeset.html">Changesets</a></li>
<li><a href="changes/index.html">Commandes relatives aux modifications/refactorisations</a></li>
<li><a href="include.html">Inclure/imbriquer des changelogs</a></li>
<li><a href="preconditions.html">Préconditions</a></li>
<li><a href="contexts.html">Contextes</a></li>
<li><a href="changelog_parameters.html">Paramètres des Changelogs</a></li>
<li><a href="generating_changelogs.html">Génération des Changelogs</a></li>
<li><a href="existing_project.html">Introduire Liquibase dans un projet existant</a></li>
</ul>

<h2>Commandes Liquibase</h2>
<ul>
<li><a href="update.html">Update</a></li>
<li><a href="rollback.html">Rollback</a></li>
<li><a href="diff.html">Diff</a></li>
<li><a href="sql_output.html">Sorties SQL</a></li>
<li><a href="dbdoc.html">DBDoc</a></li>
</ul>

<h2>Exécuter Liquibase</h2>
<ul>
<li><a href="running.html">Aperçu</a></li>
<li><a href="command_line.html">Ligne de commandes</a></li>
<li><a href="ant/index.html">Ant</a></li>
<li><a href="maven/index.html">Maven</a></li>
<li><a href="spring.html">Spring</a></li>
<li><a href="servlet_listener.html">Servlet Listener</a></li>
<li><a href="cdi.html">Environnement CDI</a></li>
</ul>

<h2>Développer des extensions</h2>
<ul>
<li><a href="sdk/index.html">SDK Liquibase</a></li>
</ul>
</div>

<div class="span-13 last">
<h2>Concepts principaux</h2>

<h3>Fichier Changelog</h3>
<p>
Les développeurs enregistrent les modifications de la base de données dans des fichiers textes sur leurs machines de développement et les appliquent
à leurs bases de données locales. Les fichiers changelogs (ou journaux de modifications) peuvent être imbriqués à l''envie pour permettre une meilleure gestion. 
<a href="databasechangelog.html">[en savoir plus]</a>
</p>

<h3>Change Set</h3>
<p>
Les Change Sets (ou ensembles de modifications) sont identifiés de manière unique grâce aux attributs "author" et "id" ainsi que grâce à l''emplacement du fichier changelog. Ils sont l''unité de base dont Liquibase trace l''exécution. Quand Liquibase s''exécute, il interroge la table DATABASECHANGELOG pour voir les changesets qui sont indiqués comme ayant déjà été exécutés puis exécute toutes les changesets du fichier changelog qui n''ont pas encore été exécutés.
 <a href="databasechangelog.html">[en savoir plus]</a>
</p>

<h3>Changes</h3>
<p>
Chanque changeset contient généralement une modification qui décrit les modifications ou refactorisations à appliquer à la base de données. Liquibase prend en charge à la fois des modifications descriptives qui génèrent du SQL pour les bases de données prises en charge et du SQL brut.
Généralement, il ne devrait y avoir q''un seul ensemble de modification par changeset pour éviter des erreurs que des instructions dont le commit échoue ne laissent la base de données dans un état inattendu.
 <a href="changes/index.html">[en savoir plus]</a>
</p>

<h3>Préconditions</h3>
<p>
Des préconditions peuvent être appliquées soit à un changelog dans son intégralité, soit à des changes sets particuliers. Si une précondition échoue, Liquibase arrête son exécution.
 <a href="preconditions.html">[en savoir plus]</a>
</p>

<h3>Contextes</h3>
<p>
Des contextes peuvent être appliqués à des ensembles de modification pour contrôler ceux qui sont exécutés dans des environnements différents. Par exemple, certains ensembles de modifications peuvent être marqués "production" et d''autres "test". Si aucun contexte n''est indiqué, les ensembles de modifications seront exécutés quel que soit le contexte d''exécution.
 <a href="contexts.html">[en savoir plus]</a>
</p>

</div>

</div>
