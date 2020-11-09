https://www.postgresql.org/docs/11/routine-vacuuming.html#VACUUM-FOR-STATISTICS  
Bra att köra kontinuerligt.

 ```sql
 VACUUM;
 VACUUM FULL;
```
 FULL frigör mer utrymme men
 - tar längre tid och
 - sätter exklusivt lås på tabellen den verkar på (går ej att komma åt på något sätt).

 ```sql
ANALYZE;
 ```
 Updatera statistik (query planner bygger på statistiken).  
 Autovacuum daemon initierar automatiskt ANALYZE.
  - The daemon schedules ANALYZE strictly as a function of the number of rows inserted or updated; it has no knowledge of whether that will lead to meaningful statistical changes.
  - frequent updates of statistics are more useful for heavily-updated tables than for seldom-updated ones