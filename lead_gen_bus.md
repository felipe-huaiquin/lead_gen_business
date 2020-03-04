## Lead Gen Business.

1. Consulta que devuelve los ingresos totales para marzo de 2012.
```
SELECT MONTHNAME(charged_datetime) AS month, SUM(amount) AS total_month
FROM billing
WHERE charged_datetime LIKE '%2012-03%';
```
2. Consulta que obtiene todos los ingresos provenientes del cliente con id 2.
```
SELECT client_id, SUM(amount) AS total_charged
FROM billing
WHERE client_id = 2;
```
3. Consulta que devuelve todos los sitios que posee el cliente con un id 10.
```
SELECT clients.client_id, sites.domain_name
FROM clients
JOIN sites ON sites.client_id = clients.client_id
WHERE clients.client_id = 10;
```
4. Consulta que devuelve el número total de sitios creados por mes y por año para el cliente 1 y luego, para el cliente 20.
#Cliente 1.
```
SELECT clients.client_id, COUNT(sites.domain_name) AS site_quantity, MONTH(sites.created_datetime) AS month, YEAR(sites.created_datetime) AS year
FROM clients
JOIN sites ON sites.client_id = clients.client_id
WHERE clients.client_id = 1
GROUP BY MONTH(sites.created_datetime), YEAR(sites.created_datetime)
```
#Cliente 20.
```
SELECT clients.client_id, COUNT(sites.domain_name) AS site_quantity, MONTHNAME(sites.created_datetime) AS month, YEAR(sites.created_datetime) AS year
FROM clients
JOIN sites ON sites.client_id = clients.client_id
WHERE clients.client_id = 1
GROUP BY MONTH(sites.created_datetime), YEAR(sites.created_datetime)
```
5. Consulta que devuelve el total de leads por sitio entre el 1 de enero y 15 de febrero 2015.
```
SELECT sites.domain_name, COUNT(leads.leads_id) AS number_leads
FROM sites
JOIN leads ON leads.site_id = sites.site_id
WHERE leads.registered_datetime > '2011-01-01' AND leads.registered_datetime < '2011-02-15'
GROUP BY leads.site_id
```
6. Consulta que devuelve una lista con los nombres de todos los clientes y su correspondiente cantidad de leads durante el año 2011.
```
SELECT CONCAT(clients.first_name," ",clients.last_name) AS client_name, COUNT(leads.leads_id) AS total_leads
FROM clients
JOIN sites ON sites.client_id = clients.client_id
JOIN leads ON leads.site_id = sites.site_id
WHERE YEAR(leads.registered_datetime) = 2011
GROUP BY clients.client_id;
```
7. Consulta que devuelve una lista con los nombres de todos los clientes y su correspondiente cantidad de leads entre los meses de enero y junio del 2011.
```
SELECT CONCAT(clients.first_name," ",clients.last_name) AS client_name, COUNT(leads.leads_id) AS monthly_leads, MONTHNAME(leads.registered_datetime) AS month_leads
FROM clients
JOIN sites ON sites.client_id = clients.client_id
JOIN leads ON leads.site_id = sites.site_id
WHERE MONTH(leads.registered_datetime) BETWEEN 1 AND 6 AND YEAR(leads.registered_datetime) = 2011
GROUP BY clients.client_id, MONTH(leads.registered_datetime);
```
8. Consulta que devuelve una lista con los nombres de todos los clientes y su correspondiente cantidad de leads durante el año 2011. Esta lista contiene el nombre del cliente, el dominio del sitio web, el número de lead de ese sitio web, y la fecha de ese lead.
```

```
