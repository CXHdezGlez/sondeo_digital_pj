
# Submuestra Nacional con Ajuste de Raking

Este repositorio contiene la documentación técnica, scripts y base de datos correspondientes a la extracción y ajuste de una submuestra nacional ponderada por:

- **Estado** (según la Lista Nominal del INE)
- **Edad y Sexo** (ajustada mediante técnica de *raking*)

## Contenido

- `submuestra_1200_estado_raking.xlsx`: base de datos final con 1,200 casos y campos de ponderación
- `grafico_edad_sexo_raking.png`: validación gráfica del ajuste por edad y sexo
- `documentacion_submuestra_raking.md`: documentación técnica completa
- `documentacion_submuestra_raking.html`: versión HTML para incrustar o publicar
- `README.md`: este archivo

## Uso sugerido

En SPSS, STATA o Python:
- Aplicar el campo `peso_raking` como ponderador
- Usar `peso_estado` solo si se desea analizar por entidad federativa sin controlar por edad y sexo

## Créditos

Este trabajo fue generado en conjunto con un sistema de asistencia IA especializado en análisis de datos y SPSS v27.
