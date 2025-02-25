# Aplicación de integración WHOA - Alfa Beta

Este servicio utiliza el Terminology Kit de WHOA y las bases de Alfa Beta para realizar búsquedas semánticas dentro del Terminology Kit, permitiendo devolver los resultados incluyendo los códigos Alfa Beta. 
Si se ingresa un código válido de Alfa Beta se omitirá la búsqueda en el Terminology Kit, a menos que se indique en el cuerpo de la solicitud que se desea obtener el nombre del producto según se estableció en SNOMED CT (variable `"incluirsnomedct"=true`). En caso de ingresar un código que no esta incluído en Alfa Beta se lo buscará en el Terminology Kit de WHOA.

## Cómo ejecutar el servicio

Para iniciar el servicio, ejecute el siguiente comando. **Previamente modificar las variables de entorno (archivo .env). Aquí se deberá incluir la API Key de WHOA,al igual que el entorno al cual conectarse (Sandbox o Live).**

```sh
docker-compose up -d
```

# Importación de datos

Importar los archivos de Alfa Beta de la siguiente forma:

```sh
curl --location --request POST 'http://localhost:4000/procesar' --form 'file=@"alfabeta.zip"'
```

O desde la página web: `http://localhost:4000` (el puerto se puede establecer en el archivo .env).

**El archivo ZIP a importar debe ser el mismo que se recibió/descargo de Alfa Beta, sin cambio alguno. La importación de datos insertará los nuevos registros o bien reemplazará los datos de aquellos que tengan modificaciones, por lo que el proceso será el mismo indistintamente si el archivo contiene toda la base de datos de Alfa Beta o solamente actualizaciones.**


# Búsqueda

- Búsqueda por término sin usar Alfa Beta, únicamente el Terminology Kit (ejemplo):

```sh
curl --location --request POST 'http://localhost:4000/api/search' \
--header 'Content-Type: application/json' \
--data-raw '{
    "termino": "ANUSOL"
}'
```

- Búsqueda por código Alfa Beta sin usar el Terminology Kit (ejemplo):

```sh
curl --location --request POST 'http://localhost:4000/api/search' \
--header 'Content-Type: application/json' \
--data-raw '{
    "termino": "00671"
}'
```

- Búsqueda por código Alfa Beta incluyendo el Terminology Kit (ejemplo):

```sh
curl --location --request POST 'http://localhost:4000/api/search' \
--header 'Content-Type: application/json' \
--data-raw '{
    "termino": "00671",
    "incluirsnomedct": true
}'
```
