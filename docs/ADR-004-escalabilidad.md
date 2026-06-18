Título: ADR-004 Estrategia de escalabilidad para el módulo de inscripciones
Estado: Aceptado
Fecha: 2026-06-17
Decisores: Equipo de desarrollo
Relacionado: specs/inscripciones, backend/

## Contexto

El sistema permite la inscripción de participantes a eventos académicos. En escenarios de alta demanda (por ejemplo, apertura de inscripciones), múltiples usuarios pueden intentar registrarse simultáneamente, lo que puede generar problemas de rendimiento, inconsistencias en cupos y sobrecarga del servidor.

## Decisión

Se decide implementar una estrategia de desacoplamiento del módulo de inscripciones, permitiendo su futura escalabilidad mediante el uso de procesamiento asincrónico y control de concurrencia.

## Alternativas consideradas

* Procesamiento síncrono tradicional

  * Pros: simple implementación
  * Contras: no escala bien ante alta concurrencia

* Uso de colas de mensajes (RabbitMQ, Kafka)

  * Pros: alta escalabilidad, desacoplamiento
  * Contras: mayor complejidad

* Separación del módulo como servicio independiente

  * Pros: escalabilidad horizontal
  * Contras: mayor complejidad arquitectónica

## Consecuencias

### Beneficios

* Mejor manejo de alta concurrencia
* Reducción de errores en inscripciones
* Posibilidad de escalar el módulo de forma independiente

### Costos o riesgos

* Mayor complejidad en implementación futura
* Necesidad de monitoreo adicional

### Impacto

* Mejora la robustez del sistema
* Permite crecimiento del sistema sin rediseño completo

## Plan de implementación

* Identificar endpoints críticos de inscripción
* Incorporar control de concurrencia
* Evaluar integración con cola de mensajes
* Implementar logs y monitoreo

## Métrica de éxito

* Reducción de errores en inscripciones simultáneas
* Mejora en tiempos de respuesta bajo carga

## Triggers de revisión

* Incremento significativo de usuarios
* Problemas de rendimiento detectados
* Revisión sugerida: 3 meses
