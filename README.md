# Proyecto - Vendedores - Machine-Learning

**Rol:** Felipe Morales • **Fecha:** Sept/2025 • **Stack:** Excel, Python, R.

## 1) Problema de negocio
El proyecto consiste en que a partir de un archivo Excel debemos crear múltiples archivos Excel en 
base a un criterio de filtrado.
Específicamente, tenemos un archivo Excel con ventas de múltiples vendedores, y debemos  crear un 
archivo Excel para cada vendedor con su respectiva información. 
Primero veremos cómo sería en Excel, y luego, eficientar este proceso en Python y R.

## 2) Datos
Fuente(s), tamaño, periodo, link o script de descarga (`data/4_datos.xlsx`), notas de calidad/ética.

## 3) Metodología
ETL (SQL/Python), features, modelo/medidas, visualizaciones, supuestos.

## 4) Resultados
- Tiempo en procesamiento de datos y exportación segmentada reducida considerablemente por un sistema de automatización, entregando diferentes archivos excel filtrado por vendedores.
- Alrededor de 100 archivos Excel obtenidos en 1 segundo.

## 5) Summary - Proyecto: Automatización de Archivos excel por vendedor

import pandas as pd
import os

ruta_base = "/content"
archivo_ventas = os.path.join(ruta_base, "4_Datos.xlsx")
ventas = pd.read_excel(archivo_ventas, sheet_name="datos")
vendedores = ventas["Vendedor"].unique()

for v in vendedores:
    ventas_filtradas = ventas[ventas["Vendedor"] == v]
    nombre_archivo = v.replace(" ","_") + ".xlsx"
    ruta_salida= os.path.join(ruta_base, nombre_archivo)
    ventas_filtradas.to_excel(ruta_salida, index=False)
__________________________________________________________________

## 6) Paso a paso

[proyecto_1_paso_a_paso.py](https://github.com/user-attachments/files/22583604/proyecto_1_paso_a_paso.py)

## Carga de librerías

import pandas as pd
import os

## Lectura de archivos Excel

# Ruta del archivo
ruta_base = "/content"

# Nombre del archivo en su respectiva ruta
archivo_excel = os.path.join(ruta_base, "4_Datos.xlsx")

# Cargamos los datos a Python
datos = pd.read_excel(archivo_excel, sheet_name="datos_resumen")

# Mostramos los datos
print(datos)

## Procesamiento de datos

# Filtramos los datos para Luis
datos[datos["Vendedor"] == "Luis"]

# Almacenamos los datos filtrados para Luis
datos_luis = datos[datos["Vendedor"] == "Luis"]
print(datos_luis)

# Almacenamos los datos filtrados para Ana
datos_ana = datos[datos["Vendedor"] == "Ana"]
print(datos_ana)

# Revisamos la columna "Producto" para la data de Ana
print(datos_ana["Total Venta"])

## Exportación a Excel

# Definimos la ruta de salida
ruta_salida_ana = os.path.join(ruta_base, "datos_ana.xlsx")

# Exportamos el archivo en su respectiva ruta
datos_ana.to_excel(ruta_salida_ana, index=False)

# ------------------
# REVISIÓN COMPLETA DEL PROYECTO
# Dividir el Excel por vendedor
# ------------------

# Definimos la ruta donde leeremos y guardaremos archivos Excel
ruta_base = "/content"

# Creamos la ruta del archivo Excel
archivo_ventas = os.path.join(ruta_base, "4_Datos.xlsx")

# Cargamos el archivo Excel en Python
ventas = pd.read_excel(archivo_ventas, sheet_name="datos")

# Obtenemos los vendedores únicos
vendedores = ventas['Vendedor'].unique()


for v in vendedores:

    # Filtramos por el vendedor del ciclo
    ventas_filtradas = ventas[ventas['Vendedor'] == v]

    # Creamos el nombre del archivo utilizando el nombre del vendedor sin espacios
    nombre_archivo = v.replace(" ", "_") + ".xlsx"

    # Creamos la ruta de salida (carpeta + nombre archivo)
    ruta_salida = os.path.join(ruta_base, nombre_archivo)

    # Exportamos el archivo en su respectiva ruta
    ventas_filtradas.to_excel(ruta_salida, index=False)
