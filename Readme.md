Konfiguration

Environment Variables

- DATEF Date Format eg. Y-m-d
- DB_HOST_NAME 
- DB_USER_NAME
- DB_PASSWORD
- DB_NAME
- default_currency_iso4217
- default_currency_name
- default_currency_symbol
- site_url



#Setup 
- Mysql Installieren
 `docker run -d -e MYSQL_ROOT_PASSWORD=<my pass> -e MYSQL_DATABASE=suitecrm --name mysqlserver mysql:5.7`
Box installieren
- `docker run -d -p 80:80 --link mysqlserver bertschi/suitecrm`
