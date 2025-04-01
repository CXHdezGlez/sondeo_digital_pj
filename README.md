
# Submuestra nacional con ajuste de Raking

Este repositorio contiene la documentación técnica, scripts y base de datos correspondientes a la extracción y ajuste de una submuestra nacional ponderada por:

- **Estado** (según la Lista Nominal del INE)
- **Edad y Sexo** (ajustada mediante técnica de *raking*)

## Contenido

- `submuestra_1200_estado_raking.xlsx`: base de datos final con 1,200 casos y campos de ponderación
- `documentacion_submuestra_raking.md`: documentación técnica completa
- `Informe_Sondeo_Ejecutivo.md`: versión ejecutiva del sondeo, con los principales hallazgos
- `Informe_Sondeo_Tecnico.md`: versión técnica del sondeo, con los detalles de los distintos análisis realizados
- `README.md`: este archivo

## Uso sugerido

En SPSS, STATA o Python:
- Aplicar el campo `peso_raking` como ponderador
- Usar `peso_estado` solo si se desea analizar por entidad federativa sin controlar por edad y sexo

## Créditos

Carlos Hernández - Analista de Datos.
