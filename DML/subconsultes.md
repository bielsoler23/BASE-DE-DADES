## SUBCONSULTES
[bdd](https://github.com/bielsoler23/BASE-DE-DADES/tree/main/.sql/bbdd_rrhh.sql) per fer els exercicis

1. Obtenir el id_empleat, nom i salari dels empleats que tenen el mateix salari que l'empleat ‘Pat Fay’.
```sql
SELECT empleat_id, nom, salari
  FROM empleats
WHERE salari = (SELECT salari FROM empleats WHERE nom = 'Pat' AND cognoms = 'Fay');
```

2. Obtenir el id_empleat, nom i salari dels empleats que tenen un salari superior al de l'empleat ‘Pat Fay’.
```sql
SELECT empleat_id, nom, salari
  FROM empleats
WHERE salari > (SELECT salari FROM empleats WHERE nom = "Pat" AND cognoms = "Fay");
```

3. Obtenir el id_empleat, cognoms i codi departament dels empleats que treballen en el mateix departament que l'empleat ‘Pat Fay’.
```sql
SELECT empleat_id, cognoms, departament_id
  FROM empleats
WHERE departament_id = (SELECT departament_id FROM empleats WHERE nom = "Pat" AND cognoms = "Fay");
```

4. Obté el id_empleat, nom i salari dels empleats que guanyen més del departament de ‘Vendes’.
```sql
SELECT empleat_id, nom, salari
  FROM empleats
WHERE salari > (SELECT MAX(salari) FROM empleats WHERE departament_id = (SELECT departament_id FROM departaments WHERE nom = 'Vendes'));
```

5. Obté el id_empleat, nom i salari dels empleats que guanyen menys del departament de ‘Vendes’.
```sql
SELECT empleat_id, nom, salari
  FROM empleats
WHERE salari > (SELECT MIN(salari) FROM empleats WHERE departament_id = (SELECT departament_id FROM departaments WHERE nom = 'Vendes'));
```

6. Obté el id_empleat, nom i salari dels empleats del departament de ‘Compres’ que guanyen més que la mitjana d’aquest departament.
```sql
SELECT empleat_id, nom, salari
  FROM empleats
WHERE salari > (SELECT AVG(salari) FROM empleats WHERE departament_id = (SELECT departament_id FROM departaments WHERE nom = 'Compres'));
```

7. Obté el nom, cognom i data de contractació dels empleats que van ser contractats després de l'empleat ‘Pat Fay’. Ordena per data de contractació.
```sql
SELECT nom, cognoms, data_contractacio
  FROM empleats
WHERE data_contractacio > (SELECT data_contractacio FROM empleats WHERE nom = "Pat" AND cognoms = "Fay");
```

8. Volem saber els cognoms, salari i codi de departament dels empleats que guanyen més que la mitjana dels salaris del departament ‘Compres’. Exlou els que siguin d’aquest departament.
```sql
SELECT e.cognoms, e.salari, e.departament_id
FROM empleats e
WHERE e.salari > (
    SELECT AVG(salari)
    FROM empleats
    WHERE departament_id = (SELECT departament_id FROM departaments WHERE nom = "Compres")
)
AND e.departament_id != (SELECT departament_id FROM departaments WHERE nom = "Compres");
```

9. Partint de la consulta anterior, volem saber també el nom del departament dels empleats. Ordena per salari.
```sql
SELECT e.cognoms, e.salari, e.departament_id, d.nom AS departament
FROM empleats e
JOIN departaments d ON e.departament_id = d.departament_id
WHERE e.salari > (
    SELECT AVG(salari)
    FROM empleats
    WHERE departament_id = (SELECT departament_id FROM departaments WHERE nom = 'Compres')
)
AND e.departament_id != (SELECT departament_id FROM departaments WHERE nom = 'Compres')
ORDER BY e.salari;
```

10. Volem saber el codi, nom i cognom del jefe de l'empleat 103. Utilitza l'operador IN.
```sql
SELECT empleat_id, nom, cognoms
FROM empleats
WHERE empleat_id IN (
    SELECT id_cap
      FROM empleats
    WHERE empleat_id = 103
);
```

11. Quins departaments no tenim empleats? Mostra el codi i nom de departament. Utilitza l'operador NOT IN.
```sql
SELECT departament_id, nom
  FROM departaments
WHERE departament_id NOT IN (
  SELECT DISTINCT departament_id
    FROM empleats
  WHERE departament_id IS NOT NULL
);
```

12. Quins empleats (nom/cognom/nom_departament)  pertanyen als mateixos departaments situats a Seattle.
```sql
SELECT nom, cognoms, 
    (SELECT nom FROM departaments WHERE departament_id = empleats.departament_id) AS nom_departament
FROM empleats
WHERE departament_id IN (
    SELECT departament_id 
    FROM departaments
    WHERE localitzacio_id IN (
        SELECT localitzacio_id 
        FROM localitzacions
        WHERE ciutat = 'Seattle'
    )
);
```

13. Crea una llista dels empleats mostrant l’inicial del nom juntament amb el cognom separat per un punt (‘.’), el salari, el nom del departament de cada empleat que guanyi més de la mitjana del seu propi departament.
```sql
SELECT 
    CONCAT(LEFT(nom, 1), '.', cognoms) AS nom_cognom, 
    salari, 
    (SELECT nom FROM departaments WHERE departament_id = empleats.departament_id) AS nom_departament
FROM empleats
WHERE salari > (
  SELECT AVG(salari) 
    FROM empleats AS e 
  WHERE e.departament_id = empleats.departament_id
);
```

14. Quins empleats només han estat assignats a un sol treball? Mostra el codi empleat, nom, cognom i ordena per codi empleat.  
```sql
SELECT empleat_id, nom, cognoms
FROM empleats
WHERE (
  SELECT COUNT(*) 
    FROM historial_feines 
  WHERE historial_feines.empleat_id = empleats.empleat_id
) = 1
ORDER BY empleat_id;
```

15. Obté per cada departament, el salari màxim. Descarta els empleats que no tenen assignat cap departament.
```sql
SELECT departament_id AS id, nom, (SELECT MAX(salari) 
                                      FROM empleats e 
                                    WHERE e.departament_id = d.departament_id) AS salari_maxim
  FROM departaments d
WHERE departament_id IN (SELECT DISTINCT departament_id FROM empleats WHERE departament_id IS NOT NULL);
```

16.  Dels empleats que no treballen a cap departament indica quins són els que guanyen més? (nom,cognoms i salari).
```sql

```
17.  Volem saber quins empleats guanyen més de cada departament. Mostra el codi empleat, nom, codi de departament, nom departament i salari. Utilitza l’operador IN.
```sql

```

18. Volem saber el nom, cognoms i salari dels empleats que guanyen més QUE ALGUN dels empleats del departament  de ‘Vendes’. 
```sql

```

19. Volem saber el nom, cognoms i salari dels empleats que guanyen més QUE TOTS els empleats del departament de ‘Vendes’.
```sql

```

20. Quants empleats tenim del departament de ‘IT’ que van ser contractats bans que QUE ALGUN empleat del departament de ‘Vendes’? Mostra els cognoms i la data de contractació.
```sql

```
21. Quants empleats tenim del departament de ‘IT’ que van ser contractats abans que TOTS els empleats del departament de ‘Vendes’? Mostra els cognoms i la data de contractació.
```sql

```

22. Utilitzant l’operador EXISTS. Volem saber els departaments que tenen assignats empleats.
```sql

```

23. Mostra el resultat de la consulta tal i com es mostra a continuació:
- Crea una llista de noms dels empleats per Id de departaments
- Crea una llista de noms de departaments
- Crea una llista de noms de ciutats

```sql

```

24. Crea una llista que inclogui els cost de salaris de cada feina dins de cada departament. A la mateixa llista, mostra el cost de salaris per ciutat.
```sql

```

25. Dels empleats que han tingut 3 feines quins d’aquests estan treballant actualment al departament de Vendes.
```sql

```

26. Mostra els empleats(nom,cognoms,salari,nom_departament) que cobrin més que el doble de la mitjan del departament ‘Vendes’.
```sql

```

27. Partint de la consulta anterior exclou els empleats del departament de ‘Vendes’.
```sql

```

28. Mostra els departaments (identificador i nom) a on tots els empleats tinguin un salari més alt que la mitjana de tots els empleats amb salari superior a 2.000.
```sql

```

