Développer un module GeoNature Monitorings (Atelier du 25 Mai 2023)
===================================================================

| `Dépot et installation (github PnX-SI) <https://github.com/PnX-SI/gn_module_monitoring>`_
| `Créer un sous module (github PnX-SI) <https://github.com/PnX-SI/gn_module_monitoring/blob/master/docs/sous_module.rst>`_


Le concept
----------

| Un sous-module monitoring est constitué de 2 format de fichiers pincipaux : le JSON et le SQL.

    * JSON permet de créer la structure, le fonctionnement et l'articulation du module de suivi.
    * SQL permet de créer les vues dans votre base de données GéoNature afin de rappatrier les données dans la synthèse ou de définir un export au sein du sous module.


Au sein du module Monitorings le terme ``site`` correspond à des entités géographiques.

La structure globale d'un sous-module
-------------------------------------

Génarale
~~~~~~~~

| **Différents fichiers sont à construire pour réaliser votre sous-module :**
| `Les 3 premier fichiers listés ci-dessous sont obligatoires pour le bon fonctionnement de votre module. Les autres ont un caractère plus ou moins facultatif en fonction de vos besoins..`

    .. image:: /_static/gn_monitoring/arbo_module.png
        :align: center

    * ``config.json`` `Fichier de configuration du module qui définit l'arbre d'enchainement des formulaires et d'autres spécificités liés à la donnée.`
    * ``module.json`` `Fichier de configuration du module qui définit certains affichages (nom, description, couleur, export(s) disponible(s),...)`
    * ``site.json`` `Définit le formulaire de description des géométries (Point, LineString ou  Polygon). Jusqu'à présents, il n'est pas possible de définirs différentes géométries dans module de suivi (Exemple : Point ET Polygon impossible).`
    * ``group_site.json`` `Définit le formulaire de regroupement des géométries.`
    * ``visit.json`` `Définit le formulaire du passage sur le lieu de la géométrie.`
    * ``observation.json`` `Définit le formulaire de description des espèces observées lors de la visite.`
    * ``observation_detail.json`` `Définit le formulaire de description  des détails des observations`
    * ``nomenclature.json`` `Fichier permettant de définir et d'ajouter à la base de données des nomenclatures spécifiques au sous-module.`
    * ``synthese.sql`` `Définit la vue des données présentent dans le sous-module pour la synchronisation avec la synthèse.`
    * ``img.jpg`` `Image qui servira de vignette du sous-module sur la page d'accueil du module Monitorings. Le format paysage est à privilégier.`


Les exports
~~~~~~~~~~~
De manière avancée, il est possible de définir des exports spécifique à chaque module, à l'intérieur des modules en suivant l'arborescence illustrée.


    .. image:: /_static/gn_monitoring/arbo_module_avancé.png
        :align: center



La configuration des fichiers
-----------------------------

Entrons un peu plus dans les détails de chaque fichier.


config.json
~~~~~~~~~~~
* Dans ce fichier, ``tree`` définit les relations entre les objets, à l'image d'un arbre de cheminement.

.. code-block:: json

    {
        "tree": {
            "module": {
                "site": {
                    "visit": {
                        "observation": {
                            "observation_detail": null
                        }
                    }
                }
            }
        }
    }


L'exemple ci-dessus signifie que :

- En allant dans le module, vous pourrez consulter et décrire vos différents `sites`. 
- En entrant dans un `site`, il vous sera possible de consulter et de décrire des `visites`.
- En entrant dans une `visite`, il vous sera possible de consulter et de décrire des `observations`.
- En entrant dans une `observation`, il vous sera possible de consulter et de décrire des `observations plus en détails`.


Voici ci-dessous un autre exemple. 

.. code-block:: json

    {
        "tree": {
            "module": {
                "sites_group": {
                    "site": {
                        "visit": {
                            "observation": null
                        }
                    }
                },
                "site": {
                    "visit": {
                        "observation": null
                    }
                }
            }
        }
    }

Dans cet exemple, les groupes de sites (``Prospect zone``) et les sites (``Quadrats``) sont consultables et définissables dès l'entrée dans le module, sous la forme de deux onglets. A 


.. image:: /_static/gn_monitoring/zone_group.png




module.json
~~~~~~~~~~~


site.json
~~~~~~~~~


group_site.json
~~~~~~~~~~~~~~~


visit.json
~~~~~~~~~~


observation.json
~~~~~~~~~~~~~~~~


observation_detail.json
~~~~~~~~~~~~~~~~~~~~~~~


nomenclature.json
~~~~~~~~~~~~~~~~~


synthese.sql
~~~~~~~~~~~~
