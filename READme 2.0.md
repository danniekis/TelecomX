# TelecomX_LATAM
Challenge TelecomX_LATAM - Alura LATAM

## Objetivo del Análisis

El objetivo de este análisis es comprender y divulgar las causas por las cuales la empresa TelecomX está experimentando una alta tasa de evasión de clientes. Esta evasión representa pérdidas monetarias para la empresa, al dejar de recibir ingresos por servicios que ya no se prestan.

## 1. Limpieza y Procesamiento de Datos

Se utilizaron las librerías `pandas` y `numpy` para trabajar con los datos. A continuación se detallan los pasos realizados:

### Importación de los Datos

- Se usó la función `pd.read_json()` para leer los datos desde un archivo JSON.

### Procesamiento y Normalización

1. Se identificaron columnas con objetos JSON anidados.
2. Se creó un nuevo DataFrame `df_json` para normalizar dichas columnas usando `pd.json_normalize()`.
3. Las columnas normalizadas se integraron al DataFrame principal.
4. Se eliminaron las columnas JSON originales.
5. Se reemplazaron valores nulos o vacíos en la columna `Charges.Total` con 0.
6. Se convirtió el tipo de dato de `Charges.Total` a `float`.
7. Se transformaron las columnas tipo string a minúsculas.
8. Se codificaron valores `"yes"` y `"no"` como `1` y `0`.
9. Se creó una nueva columna `Cuentas diarias` dividiendo el valor mensual entre 30.

## 2. Análisis Exploratorio de Datos (EDA)

### Proporción de Clientes

- Total de clientes: **7,267**
- Clientes activos: **5,398** (74.3%)
- Clientes que se dieron de baja: **1,869** (25.7%)

### Evasión por Género

- Mujeres: 50.2%
- Hombres: 49.7%
- Conclusión: El género no es un factor relevante en la evasión.

### Evasión por Medio de Pago

- Bank Transfer (automatic): 13.8%
- Credit Card (automatic): 12.4%
- Electronic Check: 57.3%
- Mailed Check: 16.4%

**Conclusión:** El método **Electronic Check** está fuertemente asociado a la evasión.

### Evasión por Tipo de Contrato

- Two Year: 2.56%
- One Year: 8.88%
- Month-to-Month: 88.55%

**Conclusión:** Los contratos mensuales presentan la mayor evasión.

### Tiempo de Contrato

- La mayoría de cancelaciones ocurre en los primeros meses del contrato.

### Gasto Total

- Usuarios con bajo gasto son los que más cancelan.
- Los clientes que permanecen muestran una distribución más amplia del gasto.

## 3. Conclusiones Principales

- La tasa de evasión general es **alta (25.7%)**.
- El género no incide significativamente en la cancelación.
- Los medios de pago automáticos tienen menor evasión.
- Los contratos de tipo "Month-to-Month" son los más riesgosos.
- La evasión temprana es una señal de problemas en la experiencia inicial del cliente.
- Los clientes con menor gasto tienden más a cancelar.

## 4. Recomendaciones Estratégicas

### Contratos a Largo Plazo

- Promover contratos de 1 y 2 años con descuentos por fidelidad.

### Incentivos para Métodos de Pago Seguros

- Promocionar Bank Transfer y Credit Card con beneficios adicionales.

### Programa de Retención Temprana

- Acompañar a los clientes durante los primeros meses con buen soporte y seguimiento.

### Estudio de Clientes con Bajo Gasto

- Implementar encuestas de salida para entender las causas del abandono en este segmento.

## 5. Instrucciones para Ejecutar el Proyecto

1. Clona este repositorio:
   ```bash
   git clone https://github.com/tu_usuario/TelecomX_LATAM.git
