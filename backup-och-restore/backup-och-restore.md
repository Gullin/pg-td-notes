***[INNEHÅLL](../_content.md)***


# Backup & Restore

## EXPORT
```
pg_dump
pg_dumpall
```


## IMPORT
pg_restore måste användas om delar har exporteras genom pg_dump och växel -Fc

Kräver att databas är skapad innan, -d [databas]  
Importeras utan källans ägare och rättigheter, medför att inte roller och använder behöver finns i destinationsdatabas

SQL:
 > ```sql
 > CREATE DATABASE [databasnamn] TEMPLATE template0;
 > ```

SHELL:
 > ```properties
 > creatdb -T template0 [databasnamn]
 > ```


Mall template0 ska användas som en av de två nativa mallarna (template0 och template1).  
template0 ska innehålla template1 som den såg ut vid initial installation, ska inte ändras. Däremot kan template1 ändras.  
template1 används som standard om inget annat anges.

```properties
pg_restore --no-owner --no-privileges -d geodata_dev -h localhost -U postgres -W X:\PGBackup\Dump\geodata_2020-11-04.backup
```

Med loggfil (fungerar inte)

```properties
pg_restore --no-owner --no-privileges -d geodata_dev -h localhost -U postgres -W X:\PGBackup\Dump\geodata_2020-11-04.backup >> c:\temp\pg_restore.log
```