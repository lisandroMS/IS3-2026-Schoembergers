Título: ADR-002 Incorporación de Circuit Breaker para el manejo de errores en APIs externas

Estado: Propuesto

Fecha: 17/06/2026

Decisores: Equipo de desarrollo

Relacionado: project.md, módulo Certificados
//////////////////////////////////////////////////////////////////////////////
Contexto

    El sistema puede requerir integración con servicios externos, como plataformas de correo electrónico, sistemas de videoconferencia o servicios de autenticación.

    Cuando una API externa presenta fallos, tiempos de respuesta elevados o indisponibilidad temporal, las solicitudes realizadas por el sistema pueden quedar bloqueadas o generar errores en cascada que afecten a otros módulos.

    Se necesita una solución que permita aislar estos fallos y mantener la disponibilidad general de la aplicación aun cuando los servicios externos experimenten problemas.
//////////////////////////////////////////////////////////////////////////////
Decisión

    Se incorpora un componente de tipo Circuit Breaker para gestionar las llamadas a APIs externas.

    El Circuit Breaker monitoreará las respuestas de cada servicio externo y, al detectar una cantidad determinada de errores consecutivos, interrumpirá temporalmente las solicitudes hacia dicho servicio.

    Durante ese período, el sistema devolverá respuestas controladas y registrará los errores para su posterior análisis.

Alcance

    Incluye:

        • Integraciones con APIs externas.
        • Monitoreo de errores y tiempos de respuesta.
        • Bloqueo temporal de llamadas a servicios inestables.

    No incluye:

        • Servicios internos del sistema.
        • Accesos a la base de datos.
        • Comunicación entre módulos propios.

//////////////////////////////////////////////////////////////////////////////
Alternativas consideradas

    • Opción A: Manejo básico mediante bloques try/catch

        Pros:

        * Implementación sencilla.
        * No requiere componentes adicionales.

        Contras:

        * No evita llamadas repetidas a servicios caídos.
        * Puede generar degradación general del sistema.

    • Opción B: Incorporar Circuit Breaker

        Pros:

        * Evita errores en cascada.
        * Mejora la resiliencia de la aplicación.
        * Reduce tiempos de espera innecesarios.

        Contras:

        * Agrega complejidad arquitectónica.
        * Requiere configuración y monitoreo.

    • Opción C: Reintentos automáticos ilimitados

        Pros:

        * Puede recuperar errores temporales.

        Contras:

        * Incrementa la carga sobre servicios ya degradados.
        * Puede empeorar la situación durante una caída.

//////////////////////////////////////////////////////////////////////////////
Consecuencias
    Beneficios esperados

    * Mayor estabilidad ante fallos externos.
    * Menor impacto sobre la experiencia del usuario.
    * Mejor monitoreo de integraciones.

    Costos o riesgos que se aceptan

    * Incorporación de lógica adicional de configuración.
    * Posibles rechazos temporales de solicitudes mientras el circuito permanece abierto.

    Impacto en operación y equipo

    * Necesidad de definir umbrales de error.
    * Monitoreo periódico de las integraciones externas.

//////////////////////////////////////////////////////////////////////////////

Plan de implementación

    1. Incorporar una librería de Circuit Breaker (por ejemplo, Opossum para Node.js).
    2. Encapsular todas las llamadas a APIs externas.
    3. Configurar umbrales de apertura y cierre del circuito.
    4. Registrar eventos de fallo y recuperación.
    5. Realizar pruebas simulando indisponibilidad de servicios externos.

Dependencias

    * Node.js.
    * Librería Circuit Breaker.
    * Sistema de logging.

Métrica de éxito

    * Reducción de errores en cascada provocados por servicios externos.
    * Disminución de tiempos de espera durante caídas de APIs.
    * Recuperación automática una vez restablecido el servicio externo.

//////////////////////////////////////////////////////////////////////////////

Triggers de revisión

    * Incorporación de una plataforma de integración diferente.
    * Cambios significativos en la cantidad de servicios externos utilizados.
    * Evidencia de que la estrategia no mejora la disponibilidad del sistema.

    Fecha sugerida de revisión: 12/07/2026