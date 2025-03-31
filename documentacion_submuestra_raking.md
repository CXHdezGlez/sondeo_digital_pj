
# Documentación Técnica del Proceso de Submuestreo y Raking

## 1. Objetivo del proceso

Obtener una submuestra representativa de una base de datos nacional, garantizando:

- El cumplimiento estricto de las proporciones poblacionales por estado (según la lista nominal del INE).
- La representación de todos los grupos de edad y sexo, ajustada mediante técnica de post-stratification (raking).

## 2. Base de trabajo

Archivo original: `SD_PROC.xlsx`

> Se eliminaron previamente los registros con la categoría "Prefiero no decirlo" en la variable sexo.

## 3. Extracción de la submuestra por estado

Tamaño objetivo: **1,200 casos**

Pasos:

1. Se asignan casos a cada estado con base en su proporción en la lista nominal.
2. Se seleccionan aleatoriamente los casos requeridos por estado.
3. Se calcula el **peso de expansión por estado** como:

```python
df_sub['peso_estado'] = proporcion_poblacional_estado / proporcion_muestral_estado
```

## 4. Ajuste por Edad y Sexo (Raking)

Se aplicó un ajuste cruzado por las proporciones poblacionales de edad y sexo:

```plaintext
Rango de edad       Hombre     Mujer
18 a 24 años        50.12%     49.88%
25 a 34 años        50.10%     49.90%
35 a 44 años        49.23%     50.77%
45 a 54 años        48.26%     51.74%
55 a 64 años        46.91%     53.09%
65+                 45.31%     54.69%
```

Código de ajuste:

```python
# Crear variable cruzada edad + sexo
df_sub['edad_sexo'] = df_sub['Edad'] + " | " + df_sub['Sexo']

# Proporciones cruzadas
edad_sexo_pob = {
  '18 a 24 años | Hombre': 0.1514 * 0.5012,
  ...
  '65 años en adelante | Mujer':  0.1392 * 0.5469,
}

# Ajuste por celda
prop_muestra = df_sub['edad_sexo'].value_counts(normalize=True).to_dict()
ajuste_dict = {
  celda: edad_sexo_pob[celda] / prop_muestra[celda] for celda in edad_sexo_pob if celda in prop_muestra
}

df_sub['ajuste_edad_sexo'] = df_sub['edad_sexo'].map(ajuste_dict)
df_sub['peso_raking'] = df_sub['peso_estado'] * df_sub['ajuste_edad_sexo']
```

## 5. Validación gráfica

Gráfico final de distribución ponderada por edad y sexo:

![Distribución Edad-Sexo Raking](grafico_edad_sexo_raking.png)

## 6. Resultado final

Archivos exportados:

- [`submuestra_1200_estado_raking.xlsx`](sandbox:/mnt/data/submuestra_1200_estado_raking.xlsx)
- [`grafico_edad_sexo_raking.png`](sandbox:/mnt/data/grafico_edad_sexo_raking.png)

Variables clave:

- `peso_estado`: para análisis con ajuste por estado.
- `peso_raking`: para análisis ajustado por estado + edad + sexo.
