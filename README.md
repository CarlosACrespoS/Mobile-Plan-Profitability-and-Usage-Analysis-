# 📞 Megaline Service Profitability Pipeline

**Análisis de Rentabilidad y Comportamiento mediante Modelado Estadístico**

**Proyecto ID:** 05

---

## 📝 Descripción del Proyecto

Este proyecto desarrolla un pipeline de análisis de datos para la operadora **Megaline**, enfocado en la evaluación de rentabilidad de sus planes tarifarios (_Surf_ vs. _Ultimate_). El desafío técnico reside en la orquestación de **5 fuentes de datos transaccionales** para ejecutar una ingeniería de costos precisa y validar, mediante inferencia estadística, la viabilidad comercial de cada perfil de usuario.

## 🎯 Objetivos Estratégicos

1.  **Financial Engineering**: Implementación de la lógica de facturación corporativa (redondeo _ceiling_ y consolidación de tráfico de datos) para el cálculo de ingresos.
2.  **User Segmentation**: Identificación de patrones de consumo para diagnosticar la eficiencia de los límites actuales de los planes.
3.  **Statistical Validation**: Aplicación de pruebas de hipótesis (T-Test) para determinar diferencias significativas en los ingresos por plan y región (NY-NJ).

## 🛠️ Stack Técnico

- **Python**: Núcleo del análisis.
- **Pandas & NumPy**: Procesamiento y limpieza de datos transaccionales.
- **SciPy (Stats)**: Ejecución de pruebas de Levene y T-Test de muestras independientes.
- **Matplotlib & Seaborn**: Visualización de distribuciones y tendencias de ingresos.

## 📊 Hallazgos Clave

- **Planes**: Se rechazó la hipótesis nula, confirmando que los planes _Surf_ y _Ultimate_ generan ingresos significativamente distintos debido a los cargos por excedentes en el plan básico.
- **Geografía**: Se identificó una anomalía estadística en la región de **NY-NJ**, la cual presenta un comportamiento de consumo diferenciado respecto al promedio nacional.
