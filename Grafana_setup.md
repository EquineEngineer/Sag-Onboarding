# Grafana setup
- [Grafana setup](#grafana-setup)
- [Install necessary dependencies](#install-necessary-dependencies)
- [How to install Grafana](#how-to-install-grafana)
- [How to setup Grafana](#how-to-setup-grafana)
  - [Monaco editor](#monaco-editor)
  - [How to setup data sources](#how-to-setup-data-sources)
  - [Use case](#use-case)
- [Wrap up](#wrap-up)

# Install necessary dependencies
```bash
sudo apt update && sudo apt install unzip
```

# How to install Grafana

1. Clone the Grafana [repository](https://github.com/Dataskop/SmartCommunities)

```bash
git clone https://github.com/Dataskop/SmartCommunities.git
```

2. Download Grafana binary

```bash
wget https://dl.grafana.com/enterprise/release/grafana-enterprise-9.3.6.linux-amd64.tar.gz
tar -zxvf grafana-enterprise-9.3.6.linux-amd64.tar.gz
```

> To install other versions of Grafana, select an appropriate version on the [Grafana website](https://grafana.com/grafana/download) and download a **standalone binary**

3. Copy downloaded binary to the Grafana repository

```bash
cp -r grafana-9.3.6/bin/ SmartCommunities/grafana-9.3.6_E_DB1/
```

4. Navigate to the Grafana directory and run the server

```bash
cd SmartCommunities/grafana-9.3.6_E_DB1/
./bin/grafana-server
```

5. Login

  Open up your browser under `localhost:3000` and login with default credentials `admin` `admin`. You can skip "new passwords" step

# How to setup Grafana 
The Grafana repository has a lot of branches, but for now you just need a new local branch (e.g. `imc`)

## Monaco editor
At the moment of writing this branch is pretty old, so we need to add one thing - an editor. Some branches have it, such as `develop`, but for `imc` you have to add it manually

 1. Navigate to the `grafana-9.3.6_E_DB1/public/lib`
 ```bash
 cd grafana-9.3.6_E_DB1/public/lib
 ``` 
 2. Download the monaco editor
 ```bash
 wget "https://docs.google.com/uc?export=download&id=1nfxchDda2NOgK5bq-O9oWgE3hb1SbOBX" -O monaco.zip
 unzip monaco.zip
 ```
 > [!NOTE]
 > In case you don't have access to the file please contact Egor
 
 3. Restart the server if it's running

## How to setup data sources

For now, we have only one data source (API). To add it you need to install the neccasary [plugin](http://localhost:3000/plugins/marcusolsson-json-datasource). Once it's done, navigate to the data sources menu

<img src="https://github.com/bobokrut/Sag-Onboarding/assets/45918782/77c768cb-f05b-41e4-bf38-1e96055f87f9" width=75% height=75%>

Click `Add data source` button and select `JSON API` data source

<img src="https://github.com/bobokrut/Sag-Onboarding/assets/45918782/86edfebe-1999-4dc8-9f62-ad90abe9fc29" width=75% height=75%>

Choose a name, specify `https://data.iiss.at/dataskop/fiwarenosec/v2/entities` as a url, and leave everything else default. You can test if everything works fine by clicking `Explore`, selecting needed data source and specifying some query (e.g. `$.0`). You should get a json response

<img src="https://github.com/bobokrut/Sag-Onboarding/assets/45918782/a620d580-b867-4a62-80c3-1bec949e55d6" width=75% height=75%>

This plugin uses a `JSONPaht` as a selector. See [docs]((https://goessner.net/articles/JsonPath/))

## Use case

To demonstarate our use case I created a dashboard that can be imported to the Grafana. To import it, go to [http://localhost:3000/dashboard/import](http://localhost:3000/dashboard/import) and paste the json

<details>
  <summary>Dashboard file</summary>
  
  ```json
{
  "annotations": {
    "list": [
      {
        "builtIn": 1,
        "datasource": {
          "type": "grafana",
          "uid": "-- Grafana --"
        },
        "enable": true,
        "hide": true,
        "iconColor": "rgba(0, 211, 255, 1)",
        "name": "Annotations & Alerts",
        "target": {
          "limit": 100,
          "matchAny": false,
          "tags": [],
          "type": "dashboard"
        },
        "type": "dashboard"
      }
    ]
  },
  "description": "Just a sample dashboard to try things out",
  "editable": true,
  "fiscalYearStartMonth": 0,
  "graphTooltip": 0,
  "id": 2,
  "links": [],
  "liveNow": false,
  "panels": [
    {
      "datasource": {
        "type": "marcusolsson-json-datasource",
        "uid": "qAa5U2kIk"
      },
      "fieldConfig": {
        "defaults": {
          "color": {
            "mode": "thresholds"
          },
          "custom": {
            "hideFrom": {
              "legend": false,
              "tooltip": false,
              "viz": false
            }
          },
          "mappings": [],
          "thresholds": {
            "mode": "absolute",
            "steps": [
              {
                "color": "green",
                "value": null
              }
            ]
          }
        },
        "overrides": []
      },
      "gridPos": {
        "h": 10,
        "w": 24,
        "x": 0,
        "y": 0
      },
      "id": 4,
      "options": {
        "basemap": {
          "config": {
            "showLabels": true,
            "theme": "auto"
          },
          "name": "Layer 0",
          "opacity": 1,
          "type": "carto"
        },
        "controls": {
          "mouseWheelZoom": true,
          "showAttribution": true,
          "showDebug": false,
          "showMeasure": false,
          "showScale": false,
          "showZoom": true
        },
        "layers": [
          {
            "config": {
              "showLegend": true,
              "style": {
                "color": {
                  "fixed": "yellow"
                },
                "opacity": 0.5,
                "rotation": {
                  "fixed": 0,
                  "max": 360,
                  "min": -360,
                  "mode": "mod"
                },
                "size": {
                  "fixed": 5,
                  "max": 3,
                  "min": 2
                },
                "symbol": {
                  "fixed": "img/icons/marker/circle.svg",
                  "mode": "fixed"
                },
                "text": {
                  "field": "name",
                  "fixed": "",
                  "mode": "fixed"
                },
                "textConfig": {
                  "fontSize": 12,
                  "offsetX": 0,
                  "offsetY": 0,
                  "textAlign": "left",
                  "textBaseline": "bottom"
                }
              }
            },
            "filterData": {
              "id": "byRefId",
              "options": "A"
            },
            "location": {
              "mode": "auto"
            },
            "name": "POI",
            "tooltip": true,
            "type": "markers"
          }
        ],
        "tooltip": {
          "mode": "details"
        },
        "view": {
          "allLayers": true,
          "id": "coords",
          "lastOnly": false,
          "lat": 41.38278,
          "layer": "Layer 1",
          "lon": 2.17694,
          "padding": 10,
          "zoom": 11
        }
      },
      "pluginVersion": "9.3.6",
      "targets": [
        {
          "cacheDurationSeconds": 300,
          "datasource": {
            "type": "marcusolsson-json-datasource",
            "uid": "qAa5U2kIk"
          },
          "fields": [
            {
              "jsonPath": "$[*].address.value.addressRegion",
              "name": "region"
            },
            {
              "jsonPath": "$[*].address.value.addressCountry",
              "language": "jsonpath",
              "name": "country"
            },
            {
              "jsonPath": "$[*].name.value",
              "language": "jsonpath",
              "name": "name"
            },
            {
              "jsonPath": "$[*].location.value.coordinates[1]",
              "language": "jsonpath",
              "name": "lat"
            },
            {
              "jsonPath": "$[*].location.value.coordinates[0]",
              "language": "jsonpath",
              "name": "lon"
            },
            {
              "jsonPath": "$[*].description.value",
              "language": "jsonpath",
              "name": "description"
            }
          ],
          "method": "GET",
          "params": [
            [
              "type",
              "PointOfInterest"
            ]
          ],
          "queryParams": "",
          "refId": "A",
          "urlPath": ""
        }
      ],
      "title": "Test map",
      "transformations": [
        {
          "id": "calculateField",
          "options": {
            "alias": "address",
            "mode": "reduceRow",
            "reduce": {
              "include": [
                "region",
                "country"
              ],
              "reducer": "allValues"
            }
          }
        },
        {
          "id": "organize",
          "options": {
            "excludeByName": {
              "country": true,
              "region": true
            },
            "indexByName": {
              "address": 1,
              "country": 6,
              "description": 2,
              "lat": 3,
              "lon": 4,
              "name": 0,
              "region": 5
            },
            "renameByName": {}
          }
        }
      ],
      "transparent": true,
      "type": "geomap"
    }
  ],
  "schemaVersion": 37,
  "style": "dark",
  "tags": [],
  "templating": {
    "list": []
  },
  "time": {
    "from": "now-6h",
    "to": "now"
  },
  "timepicker": {},
  "timezone": "",
  "title": "IMC",
  "uid": "BcN3KjAVx",
  "version": 3,
  "weekStart": ""
}
  ```
</details>

After it's done, you should see this

<img src="https://github.com/bobokrut/Sag-Onboarding/assets/45918782/0c574d16-f7af-45af-88b7-737e7df12142" width=75% height=75%>

To futher explore it, press `e` on your keyboard or select `edit` in the dropdown menu (`Test map` above the map). This visualisation should be understandable but in case of the difficulties please contact Egor

# Wrap up
As a small demo you can watch this video just to get the general idea on how to work with Grafana. Pay attenchion on how something can be done and not what can be done this exmaple is not relative to us

[![Video](https://img.youtube.com/vi/EGgtJUjky8w/maxresdefault.jpg)](https://youtu.be/EGgtJUjky8w?si=3BD6cH5Q5Xp9S7DH&t=175)
