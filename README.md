# WHOA Alfabeta

Este servicio utiliza el Terminology Kit de WHOA y Alfa Beta para realizar búsquedas semánticas dentro del Terminology Kit, devolviendo los códigos Alfa Beta. Si se ingresa un código válido de Alfa Beta, se omite la búsqueda en el Terminology Kit, a menos que se indique en el cuerpo de la solicitud que se desea obtener el nombre correspondiente en SNOMED CT (variable `"incluirsnomedct"=true`).

## Cómo ejecutar el servicio

Para iniciar el servicio, ejecute el siguiente comando. Previamente modificar las variables de entorno.

```sh
docker-compose up -d
```

# Importación de datos

Importar los archivos de alfabeta de la siguiente forma:

```sh
curl --location --request POST 'http://localhost:4000/procesar' --form 'file=@"alfabeta.zip"'
```

O desde la página web: `http://localhost:4000`.

# Búsqueda

- Busqueda por terminos:

```sh
curl --location --request POST 'http://localhost:4000/api/search' \
--header 'Content-Type: application/json' \
--data-raw '{
    "termino": "ANUSOL"
}'
```

- Busqueda por código:

```sh
curl --location --request POST 'http://localhost:4000/api/search' \
--header 'Content-Type: application/json' \
--data-raw '{
    "termino": "00671"
}'
```

- Popular con el concepto snomed:

```sh
curl --location --request POST 'http://localhost:4000/api/search' \
--header 'Content-Type: application/json' \
--data-raw '{
    "termino": "ANUSOL",
    "incluirsnomedct": true
}'
```
