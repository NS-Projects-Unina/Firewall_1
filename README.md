Per prima cosa, accedi alla cartella "Progetto" ed esegui il seguente script:  

# per costruire la configurazione della rete e inserire automaticamente le regole nelle tabelle dei firewall  

./config.sh  

Accedi a uno dei due container Docker (cliente1 o host1) per testare le regole. Puoi utilizzare i comandi nel file comandi_utilizzati. 
docker exec -it cliente1 bash  


## Esegui uno degli attacchi presenti nel file comandi_utilizzati  


### Test delle Regole  

Per testare le regole, puoi utilizzare il comando seguente prima e dopo l'applicazione delle regole per registrare il traffico:  

docker exec --privileged -t firewall1 iptables -A FORWARD -j NFLOG --nflog-prefix="FORWARD Log pre-regola:"  

Dopo aver applicato le regole:  

docker exec --privileged -t firewall1 iptables -A FORWARD -j NFLOG --nflog-prefix="FORWARD Log post-regola:"  


Puoi visualizzare i risultati seguendo il percorso /var/log/ulog nel firewall testato, aprendo il file syslogemu.log.  


In caso di problemi con il log, puoi riavviare il demone ulog nel firewall con il comando:  

service ulogd2 restart  

Il file di log può essere utilizzato per analizzare il traffico che passa attraverso la rete, eventualmente per scopi futuri.  


#### Pulizia della Configurazione  

Per ripulire la configurazione e rimuovere le modifiche fatte, esegui il seguente script:  

./pulizia.sh  

Questo comando rimuoverà tutte le configurazioni e le regole applicate, riportando il sistema allo stato iniziale.
