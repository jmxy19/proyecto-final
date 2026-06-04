# Proyecto Final — Arquitecto Cloud
**Sistemas Operativos 750001C | Semestre 1 – 2026**
**Universidad del Valle**

---

## Equipo

|     Nombre     |   Código  |             Rol           |
|----------------|-----------|---------------------------|
| Jhostin Mapura | 202560787 | Virtualización            |
| Miguel Riascos | 202560706 | Docker                    |
| Mateo Carbajal | 202560786 | Kubernetes                |
| Juan Castillo  | 202560755 | Sitio Web + Documentación |

**Grupo asignado:** Grupo 4  
**Distribución gráfica:** [Kubuntu 24.04.4 desktop]  
**Distribución consola:** [Ubuntu 24.04.4 live server]  
**Imagen Docker base:** [lubuntu 24.04.4 desktop]

---

## Componente 1: Virtualización con Linux

**Distribuciones instaladas:** VM Gráfica + VM Consola  
**Herramienta:** VirtualBox / VMware

### Evidencias
- Captura instalación VM gráfica
- Captura particionamiento (lsblk)
- Captura configuración de red
- Captura prueba SSH funcional

### Comandos principales
```bash
ip a                          # Ver interfaces de red
lsblk                         # Ver particiones
ssh usuario@ip_vm_consola     # Conectar por SSH
```

---

## Componente 2: Contenedores Docker

**Servicios implementados:**
- Frontend: Nginx sirviendo HTML estático (puerto 80)
- Backend: Python HTTP (puerto 5000)

### Estructura de archivos
```
docker/
├── frontend/
│   ├── Dockerfile.frontend
│   └── index.html
├── backend/
│   ├── Dockerfile.backend
│   └── server.py
└── docker-compose.yml
```

### Evidencias
- Captura `docker compose up -d`
- Captura navegador accediendo al frontend
- Captura `curl http://localhost:5000`

### Comandos principales
```bash
docker compose up -d
docker ps
docker images
curl http://localhost
curl http://localhost:5000
```
---

## Componente 3: Orquestación con Kubernetes

**Herramienta:** Minikube

### Manifiestos
- `deployment.yaml` — Nginx con 2 réplicas
- `service.yaml` — NodePort en puerto 30080

### Evidencias
- Captura `kubectl get pods`
- Captura `kubectl get svc`
- Captura acceso desde navegador
- Captura escalado a 3 réplicas

### Comandos principales
```bash
minikube start
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl get pods
kubectl scale deployment nginx --replicas=3
minikube service nginx --url
```

---

## Componente 4: Sitio Web de Documentación

**URL del sitio:** [https://...]  
**Video YouTube:** [https://youtu.be/...]

### Secciones del sitio
- Home: introducción y objetivos
- Equipo: integrantes con fotos y roles
- Componentes: descripción, capturas y comandos de cada uno
- Conclusiones: aprendizajes, dificultades y recomendaciones

---

## Diagrama de Arquitectura

> Insertar imagen del diagrama (draw.io / Miro / Lucidchart)

---

## Conclusiones

1. [Aprendizaje principal]: durante el desarrollo de este proyecto aprendimos a poner en práctica varias tecnologías, entre ellas, la virtualización y la forma en que se pueden interconectar las máquinas virtuales de Linux (Kubuntu y Ubuntu server) configurando las redes y el acceso remoto mediante SSH, de igual manera con Docker entendimos como empaquetar servicios en contenedores facilitando el despliegue y la administración en backend y frontend, por otro lado, mediante kubernets y minikube conocimos conceptos básicos de orquestación de contenedores incluyendo el uso de pods, deployments, services y escalado de replicas,  todo esto en conjunto nos ayudó a tener una idea de como se implementan y administran servicios en entornos Cloud.
   
2. [Dificultad encontrada y cómo se resolvió]: en cada parte del proyecto se encontraron varias dificultades:

      •	Virtualización con Linux: al momento de hacer la conexión entre el entorno grafico y el servidor se presentaron     muchos problemas ya que en el VirtualBox no se estaban configurando las maquinas virtuales de forma correcta,       lo   cual hacía que no apareciera la ip para hacer la conexión entre las máquinas, para solucionar el problema      se         activo el adaptador puente y promiscuos mode en permitir todo para que se pudieran ver entre sí,         otro problema fue   que al intentar hacer la conexión se ejecutaron muchos comando de actualización y               reinstalación de SSH lo cual      hizo que se corrompieran algunos archivos y cuando se ejecutaba “sudo             systemctl status ssh” salía un error por falta de archivos, para solucionar fue necesario eliminar y                reconfigurar las VMs desde cero.
    
    •	Contenedores Docker: para los contenedores fue un poco mas fácil ya que solo se usaba el entorno grafico y los principales errores eran por una mala configuración en los archivos “Dockerfile.backend”, ”Dockerfile.frontend” y “docker-compose.yml” que no permitían crear e iniciar los contenedores, para solucionar estos errores simplemente fue poner la versión correcta en FROM que era: “FROM ubuntu:24.04”, y escribir bien el nombre del archivo “docker-compose.yml” que se había guardado con otro nombre.
    
    •	Orquestación con Kubernets: en esta parte los errores que salían era porque se estaba intentando iniciar el minikube  sin haberlo descargado, para solucionar se ejecutaron comandos como: “curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64” y “sudo install minikube-linux-amd64 /usr/local/bin/minikube”, después de esto salia un error porque era necesario agregar el usuario al grupo Docker con “sudo usermod -aG docker $USER” y durante la instalación ocurrió otro problema por falta de almacenamiento en el /root asi que fue necesario reinstalar la MV dándole mas espacio.
     
3. [Recomendación para futuros proyectos]: se recomienda ser muy cuidadoso al momento de hacer las configuraciones desde el virtual box para que al momento de ejecutar la maquina virtual no salga ningún error, otra cosa es asegurarse de dar un buen espacio de almacenamiento para poder descargar todos los archivos sin necesidad de borrar otras cosas y en la parte de dockers y orquestación asegurarse de que los archivos forntend y backend tienen la sintaxis correcta para evitar errores.
---

*Proyecto desarrollado para la asignatura Sistemas Operativos 750001C — Semestre 3, 2026*
