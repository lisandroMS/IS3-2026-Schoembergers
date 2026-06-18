Título: ADR-003 Uso de Docker para contenerización del sistema
Estado: Aceptado
Fecha: 2026-06-17
Decisores: Equipo de desarrollo
Relacionado: docker-compose.yml, backend/, frontend/

## Contexto

El sistema de gestión de eventos académicos debe poder ejecutarse en distintos entornos (desarrollo, pruebas y producción). Se requiere asegurar consistencia en la ejecución del backend y frontend, evitando problemas de dependencias y configuraciones locales.

## Decisión

Se decide utilizar Docker para contenerizar los servicios del sistema, junto con Docker Compose para la orquestación de múltiples contenedores (backend y frontend).

## Alternativas consideradas

* Instalación manual en cada entorno

  * Pros: simple inicialmente
  * Contras: inconsistencia entre entornos, difícil mantenimiento

* Máquinas virtuales

  * Pros: aislamiento completo
  * Contras: mayor consumo de recursos

* Docker

  * Pros: portabilidad, reproducibilidad, facilidad de despliegue
  * Contras: curva de aprendizaje inicial

## Consecuencias

### Beneficios

* Entornos consistentes
* Fácil despliegue
* Simplificación del onboarding de nuevos desarrolladores

### Costos o riesgos

* Necesidad de aprender Docker
* Posibles problemas de configuración inicial

### Impacto

* Mejora la organización del proyecto
* Facilita futuras integraciones y despliegues

## Plan de implementación

* Crear Dockerfile para backend
* Configurar docker-compose.yml
* Definir servicios y puertos
* Validar ejecución del sistema

## Triggers de revisión

* Cambios en la arquitectura (microservicios)
* Problemas de rendimiento en contenedores
* Revisión sugerida: 6 meses
