***[INNEHÅLL](../_content.md)***


# Prestanda och Underhåll

https://www.postgresql.org/docs/11/routine-vacuuming.html#VACUUM-FOR-STATISTICS  

Bra att köra kontinuerligt.

## VACUUM  

SQL:
> ```sql
> VACUUM;
> VACUUM FULL;
> ```

FULL frigör mer utrymme men
- tar längre tid och
- sätter exklusivt lås på tabellen den verkar på (går ej att komma åt på något sätt).

Kör vaccum från shell (om i pathen, utan sökväg)  
SHELL:
> ```propteries
> vacuumdb
> ```
från shell körs vacuum enklare för flera databaser.

## autovaccum

https://www.postgresql.org/docs/11/runtime-config-autovacuum.html  
PostgreSQL kör automatisk vacuum med analyze genom inställningar i `postgresql.config` under installationens datakatalog.  
`autovacuum = on`  
och  
`track_counts = on`

*ändrade konfigurationsparametrar behöver läsas in på nytt genom ex.*
- *pgAdmin >> Tools >> Reload Configuration*
- *\bin\pg_ctl.exe relod*
- *SELECT pg_reload_conf();*
- *service postgresql restart*

*Ingen av alternativen påverkar databasen under drift.*

## ANALYZE

SQL:
> ```sql
> ANALYZE;
> ```
 Updatera statistik (query planner bygger på statistiken).  
 Autovacuum daemon initierar automatiskt ANALYZE.
  - The daemon schedules ANALYZE strictly as a function of the number of rows inserted or updated; it has no knowledge of whether that will lead to meaningful statistical changes.
  - frequent updates of statistics are more useful for heavily-updated tables than for seldom-updated ones

  Insamlad statistik lagras i tabellen `pg_statistic`.