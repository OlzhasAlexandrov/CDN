---

copyright:
  years: 2017
lastupdated: "2017-11-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}  

# Conteneur Mapping  
La collection `SoftLayer_Container_Network_CdnMarketplace_Configuration_Mapping` contient les attributs utilisés par nos API de mappage. Chaque API de mappage renvoie une collection de ce type.

Classe `SoftLayer_Container_Network_CdnMarketplace_Configuration_Mapping` :

* `vendorName` : Nom d'un fournisseur IBM Cloud CDN valide.
* `uniqueId` : Identificateur à 10 chiffres généré par le système et unique à chaque mappage. Il est généré lors de la création d'un mappage.
* `domain` : Nom du CDN principal. Il est également appelé `hostname`.
* `protocol` : Protocole utilisé pour configurer les services. Il peut être HTTP, HTTPS ou une combinaison des deux, HTTP_AND_HTTPS.
* `originType` : Type de l'hôte d'origine, actuellement 'HOST_SERVER' ou 'OBJECT_STORAGE'.
* `originHost` : Adresse du serveur d'origine (le nom d'hôte ou l'adresse IPv4 du serveur d'origine), qui correspond au noeud final où le contenu doit être extrait ou au nom du compartiment où le contenu est stocké. Elle doit contenir moins de 511 caractères.
* `httpPort` :  Numéro du port utilisé pour le protocole HTTP. Akamai possède certaines limitations au niveau des numéros de ports pour les ports HTTP et HTTPS. Consultez la [FAQ](faq.html#are-there-any-restrictions-on-what-http-and-https-port-numbers-are-allowed-for-akamai-) pour connaître les numéros de ports autorisés.
* `httpsPort` :  Numéro du port utilisé pour le protocole HTTPS. Akamai possède certaines limitations au niveau des numéros de ports pour les ports HTTP et HTTPS. Consultez la [FAQ](faq.html#are-there-any-restrictions-on-what-http-and-https-port-numbers-are-allowed-for-akamai-) pour connaître les numéros de ports autorisés.
* `cname` : Enregistrement du nom canonique qui sert d'alias au nom d'hôte. Il peut être fourni par l'utilisateur ou généré par le système. S'il est fourni par l'utilisateur, il doit comprendre moins de 64 caractères alphanumériques et doit être unique. S'il n'est pas fourni, il sera généré lors de la création du mappage.
* `respectHeaders` : Valeur booléenne qui, si définie sur 'true', entraîne le remplacement des paramètres TTL du CDN par les paramètres TTL du serveur d'origine.
* `header` : Spécifie les informations relatives aux en-têtes d'hôte utilisés par le serveur d'origine
* `status` : Statut du mappage. Le statut peut être CNAME_CONFIGURATION, SSL_CONFIGURATION, RUNNING, STOPPED, DELETED ou ERROR.
* `bucketName` : Nom de compartiment de votre stockage d'objet S3.
* `fileExtension` : Extensions de fichier pouvant être mises en cache.
* `path` : Chemin d'accès à votre stockage d'objet S3. Il se trouve généralement sous l'URL du conteneur d'objets ou dans la section API de votre service.
* `cacheKeyQueryRule` : Les options suivantes sont disponibles pour configurer le comportement de la clé de cache : 
  * `include-all` : Inclure tous les arguments de requête. **Valeur par défaut**
  * `ignore-all` : Ignorer tous les arguments de requête
  * `ignore: space separated query-args` : Ignore ces arguments de requête spécifiques. Par exemple, "ignore: query1 query2"
  * `include: space separated query-args` : Inclut ces arguments de requête spécifiques. Par exemple, "include: query1 query2"

Il est important de faire une remarque particulière pour `uniqueId` qui est généré lors de la création d'un mappage et qui est utilisé en tant que paramètre pour les appels d'API suivants.

Par exemple, cet appel vers `listDomainMappingByUniqueid`  
```php  
$cdnMapping = $client->listDomainMappingByUniqueid(d'750352919747xxx');  
```

renverra un objet similaire à celui-ci :

```php  
[0] => SoftLayer_Container_Network_CdnMarketplace_Configuration_Mapping Object
                (
                    [vendorName] => akamai
                    [uniqueId] => 750352919747xxx
                    [domain] => test.testingcdn.net
                    [protocol] => HTTP_AND_HTTPS
                    [originType] => HOST_SERVER
                    [originHost] => test.testingcdn.net
                    [httpPort] => 80
                    [httpsPort] => 443
                    [cname] => test.cdnedge.bluemix.net
                    [performanceConfiguration] =>
                    [certificateType] =>
                    [respectHeaders] => 1
                    [header] =>
                    [status] => RUNNING
                    [bucketName] =>
                    [fileExtension] =>
                    [path] => /
                    [cacheKeyQueryRule] => include-all
                )
```


