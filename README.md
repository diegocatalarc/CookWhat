# ¿Qué cocino hoy?

App para quitarle a mi mamá la carga diaria de decidir qué cocinar.
Abre la app y el plato del día ya está decidido, según sus gustos.

- Brief del producto: [docs/brief.md](docs/brief.md)
- Tablero de tareas: [TASKS.md](TASKS.md)
- Equipo (roles): [.claude/agents/](.claude/agents/)

## Acuerdo de trabajo con el stakeholder

- **Ningún rol toma decisiones solo.** Antes de cada decisión (tecnología,
  diseño, alcance, librerías) se presentan opciones con pros y contras y una
  recomendación, y Diego decide.
- **Antes de empezar cada tarea** se explica qué se va a hacer y se espera su
  aprobación. **Al terminarla** se muestra el resultado antes de integrarlo.
- Las explicaciones van en lenguaje simple, sin jerga.

## Cómo trabajamos

Trabajamos como un equipo real. Cada etapa la lleva un rol y el stakeholder
(Diego) aprueba antes de pasar a la siguiente:

1. **Product Owner** → brief y alcance del MVP ✅
2. **Diseñador UX** → flujos y prototipo de pantallas
3. **Tech Lead** → tecnología, arquitectura y división en tareas
4. **Desarrollador** → implementación, una tarea por rama
5. **QA** → pruebas y revisión antes de integrar
6. **Prueba con la usuaria** → mamá usa la app y medimos
