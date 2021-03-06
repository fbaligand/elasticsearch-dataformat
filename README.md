Elasticsearch Data Format Plugin
========================

## Overview

Elasticsearch Data Format Plugin provides a feature to allow you to download a response of a search result as several formats other than JSON.
The supported formats are CSV, Excel, JSON(Bulk), JSON(Object List) and GeoJSON.

## Version

[Versions in Maven Repository](https://repo1.maven.org/maven2/org/codelibs/elasticsearch-dataformat/)

### Issues/Questions

Please file an [issue](https://github.com/codelibs/elasticsearch-dataformat/issues "issue").

## Installation

    $ $ES_HOME/bin/elasticsearch-plugin install org.codelibs:elasticsearch-dataformat:7.6.0

## Supported Output Formats

This plugin allows you to download data as a format you want.
If the query dsl contains "from" parameter, the query is processed as search query.
If not, it's as scan query(all data are stored.).

### CSV

    $ curl -o /tmp/data.csv -XGET "localhost:9200/{index}/{type}/_data?format=csv&source=..."

| Request Parameter | Type    | Description |
|:------------------|:-------:|:------------|
| append.header     | boolean | Append column headers if true |
| fields_name       | string  | choose the fields to dump (comma separate format) |
| source            | string  | [Query DSL](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/query-dsl.html) |
| csv.separator     | string  | Separate character in CSV |
| csv.quote         | string  | Quote character in CSV|
| csv.escape        | string  | Escape character in CSV |
| csv.nullString    | string  | String if a value is null |
| csv.encoding      | string  | Encoding for CSV |

### Excel

    $ curl -o /tmp/data.xls -XGET "localhost:9200/{index}/{type}/_data?format=xls&source=..."

| Request Parameter | Type    | Description |
|:------------------|:-------:|:------------|
| append.header     | boolean | Append column headers if true |
| fields_name       | string  | choose the fields to dump (comma separate format) |
| source            | string  | [Query DSL](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/query-dsl.html) |

### Excel 2007

    $ curl -o /tmp/data.xlsx -XGET "localhost:9200/{index}/{type}/_data?format=xlsx&source=..."

| Request Parameter | Type    | Description |
|:------------------|:-------:|:------------|
| append.header     | boolean | Append column headers if true |
| fields_name       | string  | choose the fields to dump (comma separate format) |
| source            | string  | [Query DSL](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/query-dsl.html) |

### JSON (Elasticsearch Bulk format)

    $ curl -o /tmp/data.json -XGET "localhost:9200/{index}/{type}/_data?format=json&source=..."

| Request Parameter | Type    | Description |
|:------------------|:-------:|:------------|
| source            | string  | [Query DSL](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/query-dsl.html) |
| bulk.index        | string  | Index name in Bulk file |
| bulk.type         | string  | Type name in Bulk file |

### JSON (Object List format)

    $ curl -o /tmp/data.json -XGET "localhost:9200/{index}/{type}/_data?format=jsonlist&source=..."

| Request Parameter |  Type  | Description                                                  |
| :---------------- | :----: | :----------------------------------------------------------- |
| source            | string | [Query DSL](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/query-dsl.html) |

### GeoJSON (Open GIS standard)

    $ curl -o /tmp/data.json -XGET "localhost:9200/{index}/{type}/_data?format=geojson&source=..."

| Request Parameter        |  Type   | Description                                                  |
| :----------------------- | :----:  | :----------------------------------------------------------- |
| source                   | string  | [Query DSL](http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/query-dsl.html) |
| geometry.lon_field       | string  | Longitude field for coordinates (Support Geometry type "Point") |
| geometry.lat_field       | string  | Latitude field for coordinates (Support Geometry type "Point") |
| geometry.alt_field       | string  | Altitude field for coordinates (Support Geometry type "Point") |
| geometry.coord_field     | string  | Coordinates field. Support all Geometry types (see [GeoJSON Example](https://en.wikipedia.org/wiki/GeoJSON)).<br/>If set, overwrite `geometry.lon_field`, `geometry.lat_field` and `geometry.alt_field` |
| geometry.type_field      | string  | Geometry type field (see [GeoJSON Example](https://en.wikipedia.org/wiki/GeoJSON))<br/>Only used if `geometry.coord_field` param is set |
| keep_geometry_info       | boolean | Keep or not the original geometry fields in final GeoJSON properties (default: false) |
| exclude_fields           | string  | Exclude fields in final geojson properties (comma separate format) |

**NB**: Field name can use basic style like `a` or JSONpath style like `a.b.c[2].d`
