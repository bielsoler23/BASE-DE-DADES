## 1.2.3 Consultes sobre una taula amb funcions

1. Llista totes les columnes de la taula empleats.
```sql
SELECT * FROM empleats;
```
2. Llista els cognoms de tots els empleats.
```sql
SELECT cognom
	FROM empleats;
```
3. Llista els cognoms dels empleats eliminant els cognoms que estiguin repetits.
```sql
SELECT DISTINCT cognoms
	FROM empleats;
```
4. Llista el nom i els cognoms de tots els empleats.
```sql
SELECT nom, cognoms
	FROM empleats;
```
5. Mostra els cognoms i nom dels empleats concatenats amb una coma i un
espai en blanc.
```sql
SELECT CONCAT(cognoms, ", ", nom) AS nom_complet
	FROM empleats;
```
6. Volem una columna on estigui tot en majúscules i l’altre tot en minúscules. Anomena les columnes com a "nom_majuscules" i "nom_minuscules" respectivament.
```sql
SELECT UPPER(nom) AS nom_majuscules, LOWER(nom) AS nom_minuscules
	FROM empleats;
```
7. Mostra les 6 primeres lletres dels cognoms dels empleats
```sql
SELECT LEFT(nom, 6) AS primeres_6_lletres
	FROM empleats;
```
8. Quins són els empleats que tenen la longitud del cognoms major a 6? (Mostra els cognoms i la longitud)
```sql
SELECT cognoms, LENGTH(cognoms)
	FROM empleats
WHERE LENGTH(cognoms) > 6;
```
9. Substitueix totes les 'a' dels cognoms dels empleats per 'e'. Ordena pel nou valor dels cognoms
```sql
SELECT REPLACE(REPLACE(cognoms, "a", "e"), "A", "E") AS nomsE
	FROM empleats
ORDER BY cognoms;
```
10. Mostra tots els empleats que tenen en la segona posició dels cognoms una 'a'. (Sense utilitzar l’operador LIKE, ni REGEXP)
```sql
SELECT SUBSTRING(LOWER(TRIM(cognoms)),2,1) = "a"
	FROM empleats;
```
11. Per cada empleat mostra el codi d’empleat, cognom i el salari amb un augment del 15% expressat com un número enter, etiqueta la columna amb el nom "nou_salari".
```sql
SELECT empleat_id, cognoms, salari,
  FLOOR(salari * 1.15) AS nou_salari
FROM empleats;
```
12. Partint de la consulta anterior, afegeix una nova columna que mostri la diferencia salarial entre el nou salari i l’antic. Etiqueta la columna com a "increment"
```sql
SELECT empleat_id, cognoms, 
  FLOOR(salari * 1.15) AS nou_salari,
  FLOOR(salari * 1.15) - salari AS increment
FROM empleats;
```
13. Fes una consulta on mostri el cognom de l’empleat en majúscules i la longitud del cognom dels empleats on el seu cognom comenci per J, A o M. Ordena els resultats per cognom d’empleat.
```sql
SELECT UPPER(cognoms), LENGTH(cognoms)
	FROM empleats
WHERE cognoms LIKE "J%" OR cognoms LIKE "A%" OR cognoms LIKE "M%"
ORDER BY cognoms;
```
14. Fes una consulta on mostri el codi, nom i cognoms dels empleats que van ser contractats un dilluns o un divendres.
```sql

```
15. Mostra l’import de comissió dels empleats. Etiqueta la columna com a "import_comissio" i arrodoneix el valor a 2 decimals. Si un empleat no té assignada comissió fes el que calgui per tal que el resultat de l’operació surti zero en comptes de NULL. Mostra també el cognom i el salari en Ptes despreciant els decimals (truncar)
```sql

```
16. Utilitzant alguna de les funcions de dates, obté el nom, cognom i data de contractació dels empleats contractats durant el 1997.
```sql

```
17. Utilitzant alguna de les funcions de data, mostra tots els empleats que van ser contractats entre els mesos de juny i novembre, independentment de l’any.
```sql

```
18. El nostre departament de recursos humans s’aborreix molt i per justificar el seu sou està elaborant tot d’estadístiques extranyes. Ara volen saber quins empleats varen ser contractats en un dia parell.
```sql

```
19. Mostra el cognom, la data de contractació i el dia de la setmana en el que va començar l’empleat a treballar. Etiqueta la columna com a dia. Ordena els resultats per dia de la setmana.
```sql

```
20. Mostra el codi d’empleat, cognoms i la data de contractació en format AAAAMM. El dia no ens interessa ara en el nostre estudi estadístic. Ordena per aquest nou format de data.
```sql

```
21. Per cada empleat, mostra el cognom, la data de contractació i el número de mesos entre el dia d’avui i la data de contractació. Etiqueta la columna com a "mesos_treballats" i arrodoneix sense decimals. Ordena el resultat segons els mesos treballats de més a menys.
```sql

```
22. Mostra el nom, cognom i anys d’antiguitat dels empleats que tenen una antiguitat superior o igual a 20 anys a l’empresa.
```sql

```
23. Crea una consulta per mostrar el cognom i salari de tots els empleats que guanyen més de 10.000 a l’any. Dona format al camp salari per a que tingui 15 caràcters de longitud, omplint per l’esquerra amb $. Etiqueta la columna com a salari.
```sql

```
24. Mostra el cognom, salari i percentatge de comissió dels empleats. Afegeix una nova columna en que si un empleat no té assignada comissió, posi "SenseComissió". Etiqueta la columna amb nom "no_comissio"
```sql

```
25. Mostra el cognom, salari i utilitzant la funció CASE, mostra el següent en
funció del valor del salari
  - Si el salari està entre 0 i 3000 -> "Mig"
  - Si el salari està entre 12000 i 24000 -> "Alt"
  - Qualsevol altre valor posa "Altres"
  - Anomena la columna com a "poder_adquisitiu" i ordena per salari de menor a major
```sql

```
26. Llista el codi dels departaments dels empleats que apareixen a la taula empleats.
```sql

```
27. Partint de la consulta anterior elimina els codis de departament repetits.
```sql

```
28. Calcula el nombre d'empleats que **no tenen** comissió assignada.
```sql

```
    
## 1.2.4 Consultes sobre una taula utilitzant agrupaments

1. Quants empleats van ser contractats l'any passat.
```sql
SELECT count(*) AS quants
	FROM empleats
WHERE YEAR(data_contractacio) = YEAR(curdate()) - 1;
```
2. Quin és el treballador (nº d’anys no el nom del treballador) amb més anys d'antiguitat.
```sql
SELECT MAX(timestampdiff(YEAR,data_contractacio, curdate())) AS anys_antiguitat
	FROM empleats;
-- ORDER BY anys_antiguitat DESC
-- LIMIT 1;
```
3. Quin és el treballador(nº d’anys no el nom del treballador) amb menys anys d'antiguitat.
```sql
SELECT MIN(timestampdiff(YEAR,data_contractacio, curdate())) AS anys_antiguitat
	FROM empleats;
-- ORDER BY anys_antiguitat ASC
-- LIMIT 1;

```
4. Quin és el salari mig de l'empresa
```sql
SELECT AVG(salari) AS salari_mig
	FROM empleats;
```
5. Mostra el salari més alt i el més baix dels empleats. Anomena les columnes com a "salari_max" i "salari_min" respectivament.
```sql
SELECT MAX(salari) AS salari_max, MIN(salari) AS salari_min
    FROM empleats;
```
6. Mostra la mitjana dels salaris i el número d’empleats que tenim. Arrodoneix la mitjana al número enter més pròxim i anomena les columnes com a salari_mig i num_empleats respectivament.
```sql
SELECT ROUND(AVG(salari),0) AS salari_mig, COUNT(*) AS num_empleats
	FROM empleats;
```
7. Mostra, per cada tipus de treball, la mitjana dels salaris. Ordena la informació per tipus de treball.
```sql
SELECT feina_codi, AVG(salari)
	FROM empleats
GROUP BY feina_codi;
```
8. Quants empleats tenim assignats a cada tipus de treball? Ordena la informació per número d’empleats.
```sql
SELECT COUNT(*) AS quantitat, feina_codi
	FROM empleats
GROUP BY feina_codi
ORDER BY quantitat;
```
9. Quants empleats tenim assignats a cada departament? Mostra el  codi de departament i el número d’empleats que té. Ordena la informació per número d’empleats.
```sql
SELECT departament_id, COUNT(*) AS quantitat
	FROM empleats
GROUP BY departament_id
ORDER BY quantitat;
```
10. Partint de la consulta anterior, volem saber també quants empleats no tenen departament assignat. Mostra el text "No assignat" com a identificador del departament.
```sql
SELECT ifnull(departament_id,"No assignat") AS departament_id, COUNT(*) AS quantitat
	FROM empleats
GROUP BY departament_id
ORDER BY quantitat;
```
11. Quants directors (caps) diferents tenim? Anomena la columna com a "numero_de_directors"
```sql
SELECT DISTINCT count(id_cap) AS numero_directors 
	FROM empleats;
```
12. Fes una consulta per calcular la diferència que hi  ha entre el salari màxim i el mínim dels empleats. Anomena la columna com a "diferencia".
```sql
SELECT MAX(salari) AS salari_max, MIN(salari) AS salari_min, MAX(salari) - MIN(salari) AS diferencia
    FROM empleats;
```
13. Mostra, per cada cap, el número identificador de l’empleat (com a cap) i el salari de l’empleat pitjor pagat per a aquest cap. Exclou els empleats  que no tinguin assignat cap.
```sql
SELECT id_cap, MIN(salari)
	FROM empleats
WHERE id_cap IS NOT NULL
GROUP BY id_cap;
```
14. Partint de la consulta anterior, exclou també aquells caps en què el salari mínim sigui inferior o igual a 6.000.
```sql
SELECT id_cap, MIN(salari) AS min_salari
	FROM empleats
WHERE id_cap IS NOT NULL
GROUP BY id_cap
HAVING min_salari > 6000;
```
15. Obté el número d’empleats contractats per cada any. Ordena la informació per any.
```sql
SELECT YEAR(data_contractacio) AS any, COUNT(*) AS quantitat
	FROM empleats
GROUP BY any;
```
16. Mostra els codis de departament que tenen 3 o més empleats. Mostra només el codi del departament.
```sql
SELECT departament_id
	FROM empleats
WHERE departament_id IS NOT NULL
GROUP BY departament_id
HAVING COUNT(*) >= 3;
```
17. Mostra el nombre d'empleats que cobren més de 9.000 euros.
```sql
SELECT COUNT(*)
	FROM empleats
WHERE salari > 9000;
```

## 1.2.5 Consultes multitaula (JOINs)

1. Calcula el nombre d' empleats que treballen en cadascun dels departaments. El resultat d' aquesta consulta també ha d' incloure aquells departaments que no tenen cap empleat associat.
```sql
SELECT d.nom, COUNT(e.empleat_id) AS quantitat
	FROM empleats e
	RIGHT JOIN departaments d ON e.departament_id = d.departament_id
GROUP BY d.departament_id;
```
2. ----Retorna un llistat amb els empleats i les dades dels departaments on treballa cadascú.
```sql

```
3. Retorna un llistat amb els empleats i les dades dels departaments on treballa cadascú. Ordena el resultat, en primer lloc pel nom del departament (en ordre alfabètic) i en segon lloc pels cognoms i el nom dels empleats.
```sql
SELECT d.departament_id, d.nom
	FROM departaments AS d
    INNER JOIN empleats AS e ON e.departament_id = d.departament_id;
```
4. Retorna un llistat amb el codi i el nom del departament, només d' aquells departaments que tenen empleats.
```sql

```
5. Retorna un llistat amb el codi, el nom del departament i el valor del pressupost actual de què disposa, només d' aquells departaments que tenen empleats. El valor del pressupost actual el pot calcular restant al valor del pressupost inicial (columna pressupost) el valor de les despeses que ha generat (columna despeses).
```sql

```
6. Retorna el nom del departament on treballa l' empleat que té el nif 38382980M.
```sql

```
7. Retorna el nom del departament on treballa l'empleat Pepe Ruiz Santana.
```sql

```
8. Retorna un llistat amb les dades dels empleats que treballen al departament d' R + D. Ordena el resultat alfabèticament.
```sql

```
9. Retorna un llistat amb les dades dels empleats que treballen al departament de Sistemes, Comptabilitat o R + D. Ordena el resultat alfabèticament.
```sql

```
10. Retorna una llista amb el nom dels empleats que tenen els departaments que **no** tenen un pressupost entre 100000 i 200000 euros.
```sql

```
11. Retorna un llistat amb el nom dels departaments on hi ha algun empleat el segon cognom del qual sigui NULL. Tingui en compte que no ha de mostrar noms de departaments que estiguin repetits.
```sql

```
12. Mostra el nombre d'empleats que hi ha a cada departament. Has de retornar dues columnes, una amb el nom del departament i una altra amb el nombre d'empleats que té assignats.
```sql

```
----
1. Retorna un llistat amb **tots els empleats** juntament amb les dades dels departaments on treballen. Aquest llistat també ha d' incloure els empleats que no tenen cap departament associat.
2. Retorna un llistat on només apareguin aquells empleats que no tenen cap departament associat.
3. Retorna un llistat on només apareguin aquells departaments que no tenen cap empleat associat.
4. Retorna un llistat amb tots els empleats juntament amb les dades dels departaments on treballen. El llistat ha d' incloure els empleats que no tenen cap departament associat i els departaments que no tenen cap empleat associat. Ordeni el llistat alfabèticament pel nom del departament.
5. Retorna un llistat amb els empleats que no tenen cap departament associat i els departaments que no tenen cap empleat associat. Ordeni el llistat alfabèticament pel nom del departament.


## 1.2.6 Subconsultes

### 1.2.6.1 Amb operadors bàsics de comparació

1. Retorna un llistat amb tots els empleats que té el departament de Sistemes. (Sense utilitzar INNER JOIN).
2. Retorna el nom del departament amb major pressupost i la quantitat que té assignada.
3. Retorna el nom del departament amb menor pressupost i la quantitat que té assignada.

### 1.2.6.2 Subconsultes amb ALL i ANY

1. Retorna el nom del departament amb major pressupost i la quantitat que té assignada. Sense fer ús de MAX, ORDER BY ni LIMIT.
2. Retorna el nom del departament amb menor pressupost i la quantitat que té assignada. Sense fer ús de MIN, ORDER BY ni LIMIT.
3. Retorna els noms dels departaments que tenen empleats associats. (Utilitzant ALL o ANY).
4. Retorna els noms dels departaments que no tenen empleats associats. (Utilitzant ALL o ANY).

### 1.2.6.3 Subconsultes amb IN i NOT IN

1. Retorna els noms dels departaments que tenen empleats associats. (Utilitzant IN o NOT IN).
2. Retorna els noms dels departaments que no tenen empleats associats. (Utilitzant IN o NOT IN).

### 1.2.6.4 Subconsultes amb EXISTS i NOT EXISTS

1. Retorna els noms dels departaments que tenen empleats associats. (Utilitzant EXISTS o NOT EXISTS).
2. Retorna els noms dels departaments que tenen empleats associats. (Utilitzant EXISTS o NOT EXISTS).
