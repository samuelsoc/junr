<!-- README.md is generated from README.Rmd. Please edit that file -->
junr
====

[![Travis-CI Build Status](https://travis-ci.org/FvD/junr.svg?branch=master)](https://travis-ci.org/FvD/junr) [![Coverage Status](https://img.shields.io/codecov/c/github/FvD/junr/master.svg)](https://codecov.io/github/FvD/junr?branch=master) [![CRAN\_Status\_Badge](http://www.r-pkg.org/badges/version/junr)](http://cran.r-project.org/package=junr)

Access Junar API data in R
--------------------------

The Junar API is the basis for a number of Open Data initiatives in Latin America and the USA. The `junr` package is a wrapper to make it easier to access data made public through the Junar API. Some examples of implementations are: [the City of Pasadena](http://data.cityofpasadena.net/home/), and [the City of San Jose](http://data.sanjoseca.gov/home/). Others are listed on the [Junar website](http://junar.com/?lang=en).

### Installation

    install.packages("devtools")
    devtools::install_github("FvD/junr")

Accede Datos del API de Junar en R
----------------------------------

El API de Junar es la base para varias iniciativas de Datos Abiertos en Latino América y los EEUU. El paquete `junr` facilita el acceso a estos datos des R. El objetivo es fomentar el uso de los datos disponibles haciendo el acceso lo mas fácil. Algunos ejemplos de implementaciones son: [el Portal de Datos Abiertos del Gobierno de Costa Rica](http://datosabiertos.presidencia.go.cr/home), [Chile Transparente](http://infodatos.opendata.junar.com/home/?lang=es) y la [Ciudad de Córdoba (Argentina)](http://cdcordoba.opendata.junar.com/home/?lang=en) entre otros.

### Instalación

Para instalar este paquete desde Github es necesario tener el paquete `devtools` instalado:

``` r
    install.packages("devtools")
    devtools::install_github("FvD/junr")
```

Por favor tome en cuenta que este paquete esta bajo desarrollo activo. Para actualizar la versión instalada es necesario repetir los pasos arriba.

### Uso

Como ejemplo vamos a usar los [datos de la casa presidencial de Costa Rica](http://datosabiertos.presidencia.go.cr/home). Lo primero es ir al sitio correspondiente para encontrar el URL base (`base_url`) y obtener un *API Key* para el API de Junar en [la página de Datos Abiertos Costa Rica](http://datosabiertos.presidencia.go.cr/developers/).

``` r
    library(junr)
    url_base <- "http://api.datosabiertos.presidencia.go.cr/api/v2/datastreams/"
    api_key <- "El API Key que obtuviste de la pagina"
```

Miremos primero cuales datos hay disponibles en este URL:

``` r
    get_index(url_base, api_key)
```

Este indice es la lista completa con todos los meta-datos incluidos como un `data frame` en R.

Para tener solo una lista de los GUID la instrucción es:

``` r
    list_guid(url_base, api_key)
```

Y solo un listado de los títulos:

``` r
    list_titles(url_base, api_key)
```

Estas dos anteriores ayudan para tener una sobrevista rápida de los datos que hay disponibles.

Obviamente, si conoces el GUID de interés lo puedes usar directamente para obtener los datos. Por ejemplo para los datos de la presidencia Costarricense:

    guid_datos <- "COMPR-PUBLI-DEL-MINIS"
    datos_compras <- get_data(url_base, api_key, guid_datos)
    View(datos_compras)

Con `View(datos_compras)` podrás comprobar que los datos han sido bajado desde la plataforma Junar y han sido convertidos a una hoja de datos (*EN: data frame*) en R.

### Determinar la cantidad de datos disponibles

En las plataformas que corren en Junar se encuentran muchos datos que no son mas que tablas (datos ya trabajados y resumidos). Por eso es útil poder ver de una vez cuantos filas hay detrás de cada GUID en el URL disponible.

En `junr` lo puedes hacer rápidamente usando la función `get_dimensions` para obtener una tabla con todos los GUID y las dimensiones de los datos:

``` r
   get_dimensions(url_base, api_key)
```

Plan de desarrollo
------------------

Esta es una versión preliminar y aprecio cualquier comentario. Si tienes ideas sobre funcionalidad que puede ser útil incluir en este paquete o si encuentras bichos raros (*EN: bugs*) abre un incidente aquí en Github. En mi lista de que-haceres esta por lo menos lo siguiente:

-   \[X\] Determinar la disponibilidad de datos detrás de un url\_base
-   \[X\] Convertir datos de divisas a números (en el caso de Costa Rica valores son representados como TEXT y requieren conversión para análisis numérico)

Si gustas me puedes seguirme en Twitter [@fransvandunne](<https://www.twitter.com/fransvandunne>), donde anuncio cualquier cambio en el paquete.
