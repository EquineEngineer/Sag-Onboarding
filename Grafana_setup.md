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

  Open up your browser under `localhost:3000` and login with default credentials `admin` `admin`
