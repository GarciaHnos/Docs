# Glosario

Términos que aparecen en el relevamiento y en el código de planta. Si falta uno, agregalo en un PR.

## Sistemas y productos

**Integra**  
ERP / sistema de gestión de la planta. La mayoría de los programas leen datos de Integra o graban ahí vía webservice (horas, pallets, accesos, stock).

**Qlik**  
Herramienta de indicadores / BI. El slideshow de planta mezcla tableros de Qlik con otras fuentes.

**Shologix**  
Sistema de indicadores de piso de planta. El slideshow también lo consume.

**Bizerba**  
Equipos de etiquetado. El programa de etiquetas lee registros (SQL Server) asociados a esas básculas/etiquetadoras y los persiste en Integra.

## Planta y hardware

**PLC**  
Controlador lógico programable. En mozzarella, conteo de hormas y stock de silos el software habla con un PLC (lectura o escritura periódica).

**Reloj biométrico**  
Terminal de marcación en red. Horas sueldos y control de accesos leen esas marcaciones y las envían a Integra.

**Horma**  
Unidad de queso en línea. El conteo de hormas blandos lee un PLC que cuenta piezas y graba el resultado en Integra.

**Tina**  
Equipo de elaboración. El programa de tinas lee datos del equipo y los envía a Integra vía webservice.

**Pallet / final de línea**  
Cierre de línea de yogurt, UAT o quesos: se leen pallets o cajas (CSV, SQL Server o Integra) y se registran en Integra.

**Silo**  
Almacenamiento a granel. El programa de stock lee el volumen desde PLC.

**RS232**  
Puerto serie. La balanza de termoformados lee el equipo por RS232 y graba en Integra vía webservice.

## Software y flujo de trabajo

**ws / webservice**  
API SOAP/HTTP hacia Integra. “Llama a ws” en el relevamiento significa persistir o consultar Integra sin escribir en su base en forma directa.

**feature / develop / main**  
Ramas del [Git Flow](../enfoque-metodologico/git/gitFlow/gitFlow.md). Una funcionalidad vive en `feature/<id-jira>` y entra a `develop` por Pull Request.

**Jira**  
Gestor de tickets. El ID del ticket va en el nombre de la rama y en el mensaje de commit.

**MkDocs**  
Generador de este sitio a partir de Markdown. El deploy lo hace GitHub Actions hacia GitHub Pages.
