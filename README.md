# Servidor de producció per a una empresa mitjana
## Posada a punt:
El meu servidor disposará d'un Docker Compose, amb lo qual, es facilitará l'ús i posada a punt de diferents serveis.
He disposat un servdor amb els següents recursos:
## DNS
Per a oferir un servei DNS combinat amb Docker Compose, he decidit utilitzar el BIND9, i he trobat coses bastant interessants.
Se'ns planteja el següent problema: com oferim un servei DNS dins un servidor amb Docker? S'ha d'instal·lar DNS a cada contenidor?
Després d'investigar una mica, he treobat el següent enllaç el qual exposa la manera més correcta de fer-ho (pel meu criteri) https://medium.com/@thiago.nobayashi/running-a-dns-server-in-docker-61cc2003e899.
He instal·lat BIND9 al mateix nivell que Docker, d'aquesta manera es pot enllaçar el domini al servidor sense haver de donar servei desde un contenidor.

;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     empresa.com. root.empresa.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      empresa.com.
@       IN      A       172.16.133.129

empresa.com.    IN      A       172.16.133.129
empresa.com.    IN      NS      empresa.com.

(he afegit db.empresa al named.conf.local per a poder especificar que s'utilitzará aquest arxiu com a predeterminat)

###Per a poder usar el servidor DNS, només cal engegar el servidor i donará servei automàticament

## OpenLDAP

Per a poder utilitzar un servidor OpenLDAP, he utilitzat una imatge anomenada "osixia/openldap"

## Zend Server
## Documentació PHP
