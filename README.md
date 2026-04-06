# 📊 Sistema de Monitoreo con Prometheus y Grafana

Este proyecto muestra cómo configurar un sistema básico de monitoreo utilizando **Prometheus**, **Grafana** y **Node Exporter** con **Docker Compose**.

El objetivo es recolectar métricas del sistema y visualizarlas en dashboards interactivos.

---

## 🚀 Tecnologías utilizadas

* Docker & Docker Compose
* Prometheus (recolección de métricas)
* Grafana (visualización de datos)
* Node Exporter (métricas del sistema)

---

## 📁 Estructura del proyecto

```
.
├── docker-compose.yml
├── prometheus.yml
└── README.md
```

---

## ⚙️ Configuración del proyecto

### 1. Crear `docker-compose.yml`

```yaml
version: '3.8'

services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    ports:
      - "9090:9090"

  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    environment:
      - GF_SECURITY_ADMIN_USER=admin
      - GF_SECURITY_ADMIN_PASSWORD=admin
    ports:
      - "3000:3000"

  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    ports:
      - "9100:9100"
```

---

### 2. Crear `prometheus.yml`

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node-exporter'
    static_configs:
      - targets: ['node-exporter:9100']
```

---

## ▶️ Ejecución del proyecto

Ejecuta el siguiente comando en la terminal:

```bash
docker-compose up -d
```

---

## ✅ Verificación

Comprueba que los contenedores estén corriendo:

```bash
docker ps
```

---

## 🌐 Acceso a los servicios

* Prometheus → http://localhost:9090
* Grafana → http://localhost:3000
* Node Exporter → http://localhost:9100

---

## 🔐 Credenciales de Grafana

* Usuario: `admin`
* Contraseña: `admin`

---

## 📊 Configuración de Grafana

1. Accede a Grafana
2. Ve a **Connections → Data Sources**
3. Agrega una nueva fuente de datos:

   * Tipo: **Prometheus**
   * URL: `http://prometheus:9090`
4. Guarda y prueba la conexión

---

## 📈 Creación de Dashboard

1. Crear un nuevo dashboard
2. Añadir un panel
3. Usar consultas como:

### CPU

```
node_cpu_seconds_total
```

### Memoria

```
node_memory_Active_bytes
```

---

## 🧠 Funcionamiento del sistema

* **Node Exporter** expone métricas del sistema
* **Prometheus** recolecta métricas cada 15 segundos
* **Grafana** permite visualizar las métricas en dashboards

---

## 🎯 Resultado

Se obtiene un sistema de monitoreo funcional que permite:

* Visualizar uso de CPU
* Monitorear memoria
* Analizar métricas en tiempo real

---

## 🔥 Posibles mejoras

* Añadir dashboards preconfigurados
* Implementar alertas con Alertmanager
* Agregar persistencia de datos
* Monitorear aplicaciones (APIs, bases de datos)

---

## 📌 Uso en CV

Este proyecto demuestra habilidades en:

* Contenerización con Docker
* Monitoreo de sistemas
* Visualización de datos
* Integración de herramientas DevOps

Ejemplo:

> Implementé un sistema de monitoreo con Prometheus y Grafana usando Docker Compose, recolectando y visualizando métricas del sistema en tiempo real.

---

## 📄 Licencia

Proyecto de uso educativo.
