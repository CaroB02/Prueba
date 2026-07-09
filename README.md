# Prueba
## 🤖 Pipeline CI/CD Automatizado (GitHub Actions & AWS ECS)

Para cumplir con los estándares DevOps de la asignatura, el repositorio cuenta con un pipeline de Integración y Despliegue Continuo (CI/CD) completamente automatizado mediante **GitHub Actions**. El flujo se gatilla de forma inmediata tras cada evento `git push` en la rama principal (`main`).

### 🚀 Flujo de Trabajo (Workflow)
El pipeline ejecuta de manera secuencial tres etapas críticas dentro de la infraestructura de nube:

1. **Build (Compilación):** Descarga el código fuente del repositorio, inicializa el entorno Docker y compila la imagen optimizada de la aplicación utilizando el `Dockerfile`.
2. **Push (Empuje):** Realiza el proceso de autenticación segura en la plataforma de AWS, se conecta al registro privado y sube la imagen generada hacia **Amazon ECR (Elastic Container Registry)** bajo la etiqueta `latest`.
3. **Deploy (Despliegue):** Notifica al clúster de **AWS ECS (Elastic Container Service)**, actualizando la definición de tarea (Task Definition) activa. AWS Fargate se encarga de realizar un despliegue controlado descargando la nueva imagen, garantizando la autorecuperación y disponibilidad del servicio sin tiempos de caída.

### 🔐 Gestión Segura de Credenciales (Secrets)
Para mitigar riesgos de seguridad y evitar la exposición de llaves de acceso públicas en el código (cumpliendo con las normativas de Innovatech Chile), las credenciales dinámicas de AWS Academy se inyectan en tiempo de ejecución de manera cifrada a través de **GitHub Secrets**:
* `AWS_ACCESS_KEY_ID`
* `AWS_SECRET_ACCESS_KEY`
* `AWS_SESSION_TOKEN`
