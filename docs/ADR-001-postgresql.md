Título:ADR-001 Selección de PostgreSQL como motor de base de datos
Estado: Aceptado 
Fecha: 17/06/2026
Decisores: Equipo de desarrollo 
Relacionado: project.md

//////////////////////////////////////////////////////////////////////////////
Contexto: 
El sistema de gestión de eventos académicos requiere almacenar información de usuarios, eventos, inscripciones y certificados de manera persistente y consistente. Los datos presentan múltiples relaciones entre entidades y deben soportar operaciones transaccionales, como el registro de inscripciones y la actualización de cupos disponibles. Además, el documento del proyecto establece la necesidad de utilizar una base de datos relacional compartida entre todos los módulos del sistema. Era necesario seleccionar un motor de base de datos que garantizara integridad de datos, soporte para relaciones complejas y compatibilidad con el ORM Prisma.
//////////////////////////////////////////////////////////////////////////////
Decisión 
Se adopta PostgreSQL como motor de base de datos del sistema.
Alcance Incluye:
    • Persistencia de usuarios.
    • Persistencia de eventos.
    • Persistencia de inscripciones.
    • Persistencia de certificados.
No incluye:
    • Estrategias de caché.
    • Replicación.
    • Almacenamiento de archivos.
//////////////////////////////////////////////////////////////////////////////
Alternativas consideradas 
Opción A: PostgreSQL 
Pros:
    • Base de datos relacional robusta y madura.
    • Excelente soporte para integridad referencial.
    • Compatibilidad nativa con Prisma.
    • Software libre y ampliamente utilizado. 
      Contras:
    • Requiere administración y mantenimiento.
    • Mayor complejidad que soluciones NoSQL para casos simples.
Opción B: MySQL 
Pros:
    • Amplia adopción en aplicaciones web.
    • Buen rendimiento general. 
Contras:
    • Menor alineación con las recomendaciones del equipo.
    • Algunas funcionalidades avanzadas menos completas que PostgreSQL.
Opción C: MongoDB 
Pros:
    • Flexibilidad de esquema.
    • Facilidad para almacenar documentos. 
Contras:
    • Las relaciones entre entidades del dominio son más complejas de gestionar.
    • Menor adecuación para garantizar integridad referencial.
//////////////////////////////////////////////////////////////////////////////
Consecuencias 
Beneficios esperados
    • Consistencia de datos entre módulos.
    • Gestión eficiente de relaciones entre entidades.
    • Compatibilidad completa con Prisma.
Costos o riesgos que se aceptan
    • Necesidad de administrar migraciones.
    • Dependencia de un motor relacional específico.
Impacto en operación y equipo
    • Todos los desarrolladores utilizan el mismo esquema de datos.
    • Se simplifica el mantenimiento y la integración entre módulos.
//////////////////////////////////////////////////////////////////////////////
Plan de implementación
    1. Instalar PostgreSQL.
    2. Configurar la conexión desde Prisma.
    3. Definir el esquema de datos.
    4. Crear migraciones iniciales.
    5. Integrar los repositorios de acceso a datos.
Dependencias
    • Prisma ORM.
    • Entorno Docker del proyecto.
Métrica de éxito
    • Todos los módulos almacenan información correctamente en PostgreSQL.
    • Las migraciones se ejecutan sin errores en cualquier entorno.
//////////////////////////////////////////////////////////////////////////////
Triggers de revisión
    • Problemas de escalabilidad no cubiertos por PostgreSQL.
    • Cambio tecnológico definido por el proyecto.
Fecha sugerida de revisión: 14/06/2027
