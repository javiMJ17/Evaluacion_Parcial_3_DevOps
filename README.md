# Evaluación Parcial 3 - Ingeniería DevOps

## Orquestación de microservicios en Amazon ECS y monitoreo mediante CloudWatch

### Integrantes

- Javier Castro
- Benjamin Aravena

### Información académica
- Asignatura: Ingeniería DevOps (DOY0101)
- Sección: 801D
- Docente: Guillermo Villacura
- Fecha: 27/11/2026

## Descripción del proyecto

Este proyecto tiene como objetivo implementar una arquitectura de microservicios en Amazon Web Services (AWS), utilizando Amazon ECS con Fargate para la orquestación de contenedores y Amazon CloudWatch para el monitoreo de recursos, tráfico y disponibilidad de los servicios.

## Tecnologías utilizadas

- AWS Academy Learner Lab
- Amazon ECS
- AWS Fargate
- ECS Service Connect
- AWS Cloud Map
- Amazon CloudWatch
- Container Insights
- CloudWatch Logs Insights
- Docker Hub
- PowerShell
- GitHub

## Arquitectura de microservicios

| Microservicio | Puerto | Función |
|---|---|---|
| Frontend | 5000 | Interfaz de usuario |
| Backend1 | 5001 | Consulta de publicaciones |
| Backend2 | 5002 | Consulta de usuarios |

Los microservicios se desplegaron en el clúster doy0101-ecs y se comunicaron mediante Service Connect utilizando el espacio de nombres microservices-demo.

## Seguridad

Se configuró un grupo de seguridad con las siguientes reglas de entrada:

| Puerto | Protocolo | Origen |
|---|---|---|
| 5000 | TCP | 0.0.0.0/0 |
| 5001-5002 | TCP | 172.31.0.0/16 |

Esta configuración permite el acceso público al frontend y restringe el acceso a los backends a la red interna de la VPC.

## Monitoreo y observabilidad

Se implementó el dashboard doy0101-microservicios-Castro en Amazon CloudWatch, compuesto por ocho widgets:

1. CPU y memoria.
2. Tareas deseadas y en ejecución.
3. Tráfico de red.
4. Peticiones recibidas.
5. Latencia de respuesta.
6. Códigos HTTP.
7. Comunicación entre frontend y backends.
8. Conexiones activas y nuevas.

También se utilizó CloudWatch Logs Insights para consultar y analizar los registros de los tres microservicios.

## Pruebas realizadas

- Verificación del funcionamiento de los tres microservicios.
- Consulta de publicaciones y usuarios desde el navegador.
- Generación de tráfico mediante PowerShell.
- Monitoreo de las métricas en tiempo real.
- Simulación de caída controlada de backend2.
- Verificación de la recuperación del servicio.
- Análisis de errores mediante CloudWatch Logs Insights.

## Resultados obtenidos

Durante las pruebas se comprobó el funcionamiento de los tres microservicios y su comunicación interna.

En la simulación de caída de backend2, el servicio backend1 continuó funcionando correctamente, mientras que las solicitudes de usuarios presentaron errores HTTP 502.

Mediante CloudWatch Logs Insights se identificaron 294 respuestas HTTP 502 asociadas a la consulta de usuarios. Posteriormente se restauró backend2 y se verificó la recuperación del sistema.

Las métricas HTTP 4XX y 5XX de destino no pudieron verificarse directamente en el dashboard.

## Limpieza de recursos

Al finalizar la actividad se detuvieron los microservicios y se eliminaron los servicios ECS, el clúster, el dashboard, los grupos de registros de la aplicación y el grupo de seguridad.

La eliminación del espacio de nombres de AWS Cloud Map no pudo completarse debido a una restricción de permisos de AWS Academy Learner Lab.

## Documentación y evidencias

El informe de evaluación reúne el procedimiento realizado, las capturas de pantalla, las respuestas conceptuales y el análisis de las métricas obtenidas.
