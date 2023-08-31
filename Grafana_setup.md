# Grafana setup

- [Install necessary dependencies](#install-necessary-dependencies)
- [How to setup Grafana](#how-to-setup-grafana)
  - [How to setup data sources](#how-to-setup-data-sources)
- [How to fix some errors](#how-to-fix-some-errors)
  - [Dashboard problems](#dashboard-problems)
    - [Panel not found](#panel-not-found)
    - [Can't load/edit dashboard JSON](#cant-loadedit-dashboard-json)

# Install necessary dependencies
```bash
sudo apt update && sudo apt install unzip zip npm
sudo npm install -g yarn node@19
```

# How to setup Grafana

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

## How to setup data sources
For now, to set up currently existing data sources you need to install several plugins. With a running Grafana server go to these urls and click `install`:
- [http://localhost:3000/plugins/marcusolsson-json-datasource](http://localhost:3000/plugins/marcusolsson-json-datasource)
- [http://localhost:3000/plugins/yesoreyeram-infinity-datasource](http://localhost:3000/plugins/yesoreyeram-infinity-datasource)

<details>
 <summary>Configuring other existing data sources</summary>

 To configure other existing data sources, go the data sources tab
<img src="https://github.com/bobokrut/Sag-Onboarding/assets/45918782/77c768cb-f05b-41e4-bf38-1e96055f87f9" width=75% height=75%>

Some data sources requires plugins (probably all of configured by Dataskope team). If you see a data source with a default icon, you need to install a plugin
<details>
 <summary>Example</summary>
 <img src="https://github.com/bobokrut/Sag-Onboarding/assets/45918782/aa7b725a-9e52-46c6-84a8-479a9a02411b" width=75% height=75%>
</details>

Unfortunately, there is no way to install the missing plugin with a click of a button. The easiest way to do it is to remember the name of the plugin

<img src="https://github.com/bobokrut/Sag-Onboarding/assets/45918782/34c94df1-e1d5-462d-bc5c-86be1776225f" width=75% height=75%>

Then go to `Plugins` tab

<img src="https://github.com/bobokrut/Sag-Onboarding/assets/45918782/e371c4bd-9bd2-4055-980f-4b8529f012c9" width=75% height=75%>

Search for the plugin by the name. Full name of the plugin is displayed as a link

<img src="https://github.com/bobokrut/Sag-Onboarding/assets/45918782/a8678012-eb33-401d-85b3-7527823b5e12" width=75% height=75%>

Finally install it

<img src="https://github.com/bobokrut/Sag-Onboarding/assets/45918782/6feb8dd9-1165-4aa2-a515-37bb81a5b9a4" width=75% height=75%>

</details>


# How to fix some errors

## Dashboard problems

### Panel not found

You might face this error message if open a dashboard for the first time
> [!NOTE]
> The name of the plugin might be different, in this case it is `smartcomm-multiplelinechart-panel`

<img src="https://github.com/bobokrut/Sag-Onboarding/assets/45918782/83899e5f-c21a-4097-8b0b-eb12192bf896" width=75% height=75%>

Dataskope team develops their own plugins, and in order to fix this issue you will need to build their plugins/panel manually. 
<details>
 
 <summary>Solution</summary>
 
 1. In the `SmartCommunities` repo navigate to `grafana-9.3.6_E_DB1/data/plugins/`
```bash
cd grafana-9.3.6_E_DB1/data/plugins/
```
2. Go to the directory with the same name as the in the error message (in this case it is `smartcomm-multiplelinechart-panel`
```bash
cd smartcomm-multiplelinechart-panel
```
3. Install and build everything
```bash
yarn install && yarn dev --no-watch
```
> [!NOTE]
> You might see some errors during build. You can ignore them unless you can build the plugin (`error Command failed with exit code 1.` might be also fine

4. Verify that everything works
Restart the server. Then go to the dashboard and if error is gone then you are good to go. If not, please contact Egor

</details>

### Can't load/edit dashboard JSON
<details>
 
 <summary>Solution</summary>
 
 If loading of the json file takes forever you might nned to add monaco editor to the current branch. 
 1. Verify that monaco editor is missing
     1. Navigate to the `public/lib/`
     ```bash
     cd public/lib/
     ```
     2. List directories
     ```bash
     ls
     ```
     If you don't see `monaco` directory then procced to the next step. If it's there then you have a different problem🤷
 
 2. Download the monaco editor
 You can the `monaco` editor from the other branches (e.g. `feature_extremeValues`), however you download it from my google drive as a `zip` file and unzip it. (you need to be in the `public/lib/` directory)
 
 ```bash
 wget "https://docs.google.com/uc?export=download&id=1nfxchDda2NOgK5bq-O9oWgE3hb1SbOBX" -O monaco.zip
 unzip monaco.zip
 ```
 > [!NOTE]
 > In case you don't have access to the file please contact Egor
 
 3. Restart the server

</details>
