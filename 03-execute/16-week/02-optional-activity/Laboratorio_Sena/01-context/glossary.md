# Glosario

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Términos del dominio SENA

| Término | Definición | Contexto |
|---------|------------|----------|
| **Ficha** | Grupo de aprendices matriculados en un programa de formación específico. Identificada por un código numérico único (ej: `2879723`). Una ficha tiene una jornada asignada, un nivel de formación y una fecha de inicio y fin. | SENA |
| **Jornada** | Franja horaria institucional en la que se desarrollan las actividades de formación. Las jornadas definidas son: Diurna (6:00–14:00), Tarde (14:00–22:00) y Nocturna (18:00–22:00). | SENA |
| **Horario** | Asignación temporal que define cuándo, dónde y con qué instructor se desarrolla una competencia o resultado de aprendizaje para una ficha específica. Un horario incluye: ficha, instructor, ambiente, fecha/hora de inicio y fin. | Dominio |
| **Instructor** | Profesional vinculado al SENA (contratista o planta) encargado de impartir formación a una o varias fichas. Puede tener disponibilidad parcial y especializaciones por área de conocimiento. | SENA |
| **Aprendiz** | Persona matriculada en un programa de formación del SENA dentro de una ficha activa. Consume horarios de forma pasiva (consulta, no gestiona). | SENA |
| **Ambiente** | Espacio físico o virtual donde se desarrolla la formación: aula, laboratorio, taller, sala de sistemas o plataforma virtual (Teams, Territorium). Tiene capacidad máxima y disponibilidad horaria. | SENA |
| **Competencia** | Unidad de formación que agrupa un conjunto de resultados de aprendizaje. Define el bloque temático que un instructor desarrolla con una ficha. | SENA |
| **Resultado de Aprendizaje (RA)** | Logro específico y medible que el aprendiz debe alcanzar al finalizar una competencia. Los RA son la unidad mínima de planificación de horarios. | SENA |
| **Coordinador** | Funcionario de planta del SENA responsable de gestionar los horarios de una o varias fichas, asignar instructores y resolver conflictos de agenda. | SENA |
| **Disponibilidad** | Ventana de tiempo en la que un instructor o un ambiente puede ser asignado a una actividad formativa sin generar conflicto con otra asignación. | Dominio |
| **Conflicto de horario** | Situación en la que un instructor o un ambiente está asignado a dos o más actividades en el mismo bloque de tiempo. El sistema debe detectar y prevenir estos conflictos. | Dominio |
| **Bloque** | Unidad mínima de tiempo de una sesión formativa. Generalmente de 1 hora, agrupable en bloques de 2 o 4 horas consecutivas. | Dominio |
| **Iteración** | Ciclo de desarrollo del proyecto (equivalente a un sprint). Cada iteración produce un incremento documentado y revisado del sistema. | Proyecto |
| **ADR** | Architecture Decision Record. Documento que registra una decisión arquitectónica importante: contexto, opciones evaluadas, decisión tomada y consecuencias. | Proyecto |
| **ADSO** | Análisis y Desarrollo de Software. Programa de formación tecnológica del SENA al que pertenece el equipo que desarrolla este sistema. | SENA |
| **Territorium** | Plataforma virtual utilizada por el SENA para el seguimiento de actividades, evidencias y comunicación entre instructores y aprendices. | SENA |
| **LMS** | Learning Management System. Sistema de gestión de aprendizaje. En el contexto SENA, puede referirse a Territorium u otras plataformas de apoyo. | Tecnología |
| **Microservicio** | Componente de software independiente y desplegable que encapsula una responsabilidad de negocio específica dentro del sistema (ej: `horarios-service`, `usuarios-service`). | Arquitectura |
| **JWT** | JSON Web Token. Mecanismo estándar para autenticación y autorización sin estado entre el cliente y los microservicios del sistema. | Tecnología |
| **API Gateway** | Punto de entrada único al sistema que enruta las peticiones a los microservicios correspondientes, aplica autenticación y controla el tráfico. | Arquitectura |

---

## Acrónimos frecuentes

| Acrónimo | Significado |
|----------|-------------|
| RF | Requisito Funcional |
| RNF | Requisito No Funcional |
| HU | Historia de Usuario |
| ADR | Architecture Decision Record |
| RA | Resultado de Aprendizaje |
| PR | Pull Request |
| CI/CD | Continuous Integration / Continuous Deployment |
| ER | Entidad-Relación (modelo de base de datos) |
| CRUD | Create, Read, Update, Delete |
| SLA | Service Level Agreement |
