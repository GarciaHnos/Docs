# Primer día en el Sector IT

Esta página es el punto de partida. El resto del sitio (Git, convenciones, programas de planta) se lee después de completar esta lista.

## Antes de codear

Pedí estos accesos a quien te asignaron como referente. Sin ellos no vas a poder clonar repos ni ver sistemas de planta.

| Acceso | Para qué | Cómo se pide |
| ------ | -------- | ------------ |
| Usuario de red / correo | Mail, calendario, archivos internos | Referente de IT |
| GitHub org `GarciaHnos` | Código y este sitio de docs | Invitación a la organización |
| Jira | Tickets; el ID va en el nombre de la rama `feature/<id-jira>` | Referente de IT |
| Integra | ERP de planta; casi todos los programas graban o leen de acá | Referente de sistemas / planta |
| Red de planta / VPN | Relojes biométricos, PLC, SQL Server de línea | Referente de IT |

Los responsables por dominio están en [Contactos](contactos.md). Términos de planta (lote, PLC, Bizerba, Shologix) están en el [Glosario](glosario.md).

## Entorno de trabajo

1. Instalá Git y configurá usuario, correo y autenticación. Guía: [Configuración inicial](../enfoque-metodologico/git/configInicial/configInicial.md).
2. Cloná este repositorio (`GarciaHnos/Docs`) y recorré el sitio en local con MkDocs. Guía: [Previsualización](../contribucion/mkDocs/Previsualización/previsualizacion.md).
3. Leé el [flujo Git](../enfoque-metodologico/git/gitFlow/gitFlow.md): las features salen de `develop` y el PR va **hacia** `develop`, no al revés.
4. Revisá [nomenclatura](../enfoque-metodologico/nomeclatura/nomenclatura.md), [SOLID](../enfoque-metodologico/principiosSOLID/principios_solid.md) y [Clean Code](../enfoque-metodologico/clean-code/cleancode.md) antes del primer PR.

## Qué hay en este sitio

- **Onboarding** — esta guía, glosario y contactos.
- **Enfoque metodológico** — Git, nombres, SOLID, Clean Code y Clean Architecture.
- **Proyectos** — [relevamiento](../proyectos/relevamientoProgramas/relevamientoProgramas.md) y una página por programa de planta.
- **Contribución** — cómo editar MkDocs y Markdown.
- **DevOps** — cómo se publica este sitio.

## Primera semana (sugerida)

1. Día 1: accesos, clone de Docs, leer glosario y relevamiento.
2. Día 2: levantar MkDocs en local y un PR de prueba (typo o una corrección chica).
3. Día 3–5: el referente te asigna un sistema. Abrí su página en Proyectos y el repo si existe. Anotá lo que falte (accesos, dependencias) y actualizá la página.

!!! tip "Si algo de esta guía no coincide con la práctica actual"
    Corregilo en un PR. Este sitio es la fuente de onboarding; si está desactualizado, el próximo ingreso vuelve a tropezar.
