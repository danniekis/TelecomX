# =====================================================
# TELECOM X - CHALLENGE 2: Alura LATAM
# Análisis de clientes que abandonan la empresa (Churn)
# =====================================================

# 1. LIBRERÍAS
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

# Configuración estética
sns.set(style='whitegrid', palette='muted')
plt.rcParams['figure.figsize'] = (10, 6)

# 2. EXTRACCIÓN DE LOS DATOS
url = 'https://raw.githubusercontent.com/alura-cursos/challenge2-data-science-LATAM/refs/heads/main/TelecomX_Data.json'
df = pd.read_json(url)

# 3. TRANSFORMACIÓN DE LOS DATOS

# Eliminación de espacios vacíos como NaN y limpieza inicial
df.replace(" ", np.nan, inplace=True)
df.dropna(inplace=True)

# Conversión de columnas numéricas
df['Charges.Monthly'] = pd.to_numeric(df['Charges.Monthly'], errors='coerce')
df['Charges.Total'] = pd.to_numeric(df['Charges.Total'], errors='coerce')
df['SeniorCitizen'] = df['SeniorCitizen'].astype(int)

# Mapeo de variables categóricas
df['Churn'] = df['Churn'].map({'Yes': 1, 'No': 0})

# Transformación a minúsculas
df.columns = [col.lower() for col in df.columns]
df = df.applymap(lambda x: x.lower() if isinstance(x, str) else x)

# Reemplazo de 'yes' y 'no' por 1 y 0
df.replace({'yes': 1, 'no': 0}, inplace=True)

# Cálculo de cuentas diarias
df['cuentas_diarias'] = df['charges.monthly'] / 30

# 4. ANÁLISIS EXPLORATORIO

# Porcentaje de churners
total_clientes = len(df)
churn_rate = df['churn'].mean() * 100
print(f"Total de clientes: {total_clientes}")
print(f"Tasa de abandono (Churn): {churn_rate:.2f}%")

# Churn por tipo de contrato
sns.countplot(data=df, x='contract', hue='churn')
plt.title("Churn por tipo de contrato")
plt.xlabel("Tipo de contrato")
plt.ylabel("Cantidad")
plt.xticks(rotation=30)
plt.tight_layout()
plt.show()

# Churn por forma de pago
sns.countplot(data=df, x='paymentmethod', hue='churn')
plt.title("Churn por forma de pago")
plt.xlabel("Forma de pago")
plt.ylabel("Cantidad")
plt.xticks(rotation=30)
plt.tight_layout()
plt.show()

# Churn por tenure (meses)
sns.histplot(data=df, x='tenure', bins=30, hue='churn', multiple='stack')
plt.title("Distribución del tiempo de contrato")
plt.xlabel("Meses de permanencia")
plt.ylabel("Cantidad")
plt.tight_layout()
plt.show()

# Gasto total vs churn
sns.histplot(data=df, x='charges.total', bins=30, hue='churn', multiple='stack')
plt.title("Distribución del gasto total")
plt.xlabel("Gasto total")
plt.ylabel("Cantidad")
plt.tight_layout()
plt.show()

# Exportar dataframe limpio para reporte
# df.to_csv("telecomx_limpio.csv", index=False)

# =====================================================
# FIN DEL ANÁLISIS INICIAL DE TELECOMX
# =====================================================
