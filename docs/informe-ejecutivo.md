# Optimización de tarifa eléctrica y potencia contratada: caso Antonio

| Equipo / Departamento | Proyecto individual de análisis de datos |
| :-------------------- | :--------------------------------------- |
| **Analista**          | Jose Maderas                             |
| **Contribuyentes**    | Ninguno                                  |
| **Status**            | Entregado                                |
## Resumen ejecutivo

Antonio mantenía 16,44 kW de potencia contratada dos años después de cesar la actividad profesional que los justificaba. El análisis de 17.542 registros horarios de consumo y de 57 registros del maxímetro demuestra que su demanda máxima real es de 6 kW, es decir, un 36,50 % de lo contratado. Simulando tres escenarios de contrato sobre su consumo real de 2025, la reducción a 10 kW con peaje 2.0TD supone 586,07 € anuales menos en los términos de energía y potencia (-37,8 %). El 71,6 % de ese ahorro procede del término de potencia, no de la tarifa de energía: el problema no era qué tarifa tenía contratada, sino cuántos kilovatios.

## Planteamiento del Problema / Antecedentes

Antonio, jubilado de 66 años, compartía un único suministro eléctrico entre su vivienda y una actividad profesional que requería maquinaria en funcionamiento continuado. Esa actividad justificaba tanto un consumo elevado como una potencia contratada de 16,44 kW bajo peaje 3.0TD.

Tras jubilarse, Antonio cesa la actividad y vende la maquinaria. Sus necesidades energéticas cambian de forma radical, pero la instalación y el contrato permanecen intactos, porque vivienda y negocio nunca tuvieron contadores ni contratos separados. Antonio sigue recibiendo facturas que no se corresponden con su nueva realidad y no dispone de criterio para valorar si el contrato sigue siendo adecuado.

El problema es representativo de una situación frecuente y con coste silencioso: la potencia contratada se revisa a la baja con muchísima menos frecuencia que al alza, porque nada en la factura señala el sobredimensionamiento.

> La identidad de Antonio y cualquier dato que permita identificarle se ha omitido, de acuerdo con la normativa de protección de datos.

## Propósito

Este análisis no responde a un objetivo de negocio interno, sino a una consulta concreta de un particular. Los resultados que persigue son:

- **Reducir el coste eléctrico anual del suministro** sin comprometer el servicio.
- **Dimensionar la potencia contratada** con un margen de seguridad justificado frente a la demanda real medida.
- **Documentar un criterio de decisión reutilizable** para revisar el contrato en el futuro, en lugar de entregar solo una recomendación puntual.

## Análisis

|Rango de tiempo|Consumo y reactiva: 01/01/2024 a 31/12/2025. Potencia máxima: 01/06/2024 a 31/12/2025. Simulación económica: año 2025 completo|
|:--|:--|
|**Localización**|Un único punto de suministro, península española|
|**Dispositivos**|No aplica. Fuente: contador telegestionado del suministro (e-distribución)|
|**Métricas incluídas**|Energía activa consumida (kWh), energía reactiva inductiva (kVARh), potencia máxima registrada (kW), % de utilización de la potencia contratada, coste simulado de los términos de energía y potencia (€), ahorro absoluto y relativo por escenario|
|**Resumen**|La demanda máxima real es de 6 kW frente a 16,44 kW contratados. El consumo cae un 8,72 % en 2025 y la energía reactiva un 56,29 %, confirmando físicamente el cese de actividad. De los tres escenarios simulados, los dos que reducen la potencia a 10 kW bajo peaje 2.0TD son equivalentes entre sí y ambos mejoran el contrato actual en torno a un 38 %|
|**Impacto Financiero**|586,07 €/año de ahorro en los términos de energía y potencia (-37,8 %). Desglose: 298,26 € por reducir la potencia de 16,44 a 10 kW, 121,26 € por el cambio de peaje 3.0TD a 2.0TD y 166,54 € por el precio de energía de la nueva oferta. **Alcance:** la cifra cubre únicamente energía consumida y potencia contratada, los dos únicos conceptos sobre los que el cliente decide al elegir tarifa. Quedan fuera impuestos, alquiler del contador y financiación del bono social|

## Descubrimientos / Hallazgos

**1. El contrato está sobredimensionado en un factor de 2,7.**

|Indicador|Valor|
|---|---|
|Potencia contratada|16,44 kW|
|Potencia máxima real registrada|6 kW|
|Utilización de la potencia contratada|36,50 %|
|Margen no utilizado|10,44 kW|

**2. El consumo cae y lo hace en el momento y en la franja esperados.** El consumo total de 2025 baja un 8,72 % frente a 2024, pero el dato anual esconde el patrón relevante: la caída se concentra en la franja de mañana de los días laborables (-33,32 %), que es cuando operaba la maquinaria. Los meses anteriores a abril de 2024 se sitúan muy por encima de la mediana mensual de 281 kWh; a partir de esa fecha el consumo se estabiliza por debajo.

**3. La energía reactiva confirma el cese con una variable independiente del testimonio del cliente.** La reactiva inductiva la demandan las cargas inductivas, y los motores eléctricos son la principal de ellas. Si la maquinaria dejó de funcionar, debe desplomarse, y lo hace: -56,29 % interanual. El descenso no es uniforme. En las cuatro horas identificadas como horario de trabajo de la maquinaria (7:00, 8:00, 19:00 y 20:00) la caída va del 84,6 % al 90,6 %, frente a un 22,6 % en el resto del día. Es la evidencia más sólida del análisis porque no depende de hábitos domésticos, de estacionalidad ni de lo que el cliente recuerde.

**4. La reducción de potencia y el cambio de peaje son una sola decisión.** La Circular 3/2020 de la CNMC reserva la 3.0TD a los suministros de baja tensión con potencia superior a 15 kW y la 2.0TD a los de 15 kW o menos. Bajar a 10 kW no permite elegir peaje: lo determina.

**5. La elección entre precio único y discriminación horaria es económicamente irrelevante en este caso.** La diferencia entre ambas modalidades es de 1,86 € anuales. Dado que el consumo horario tiene resolución de 1 kWh, el error de redondeo esperado sobre esa diferencia es de aproximadamente ±1,23 €: bastaría con que 17 kWh de los 3.935 anuales estuvieran mal clasificados entre periodos para invertir el resultado. La razón de fondo es que la caída de consumo se concentró en punta (-19,02 %) y llano (-9,19 %), mientras que el valle, que es el periodo que hace atractiva la discriminación horaria, se mantuvo estable (+0,57 %).

**6. La decisión que más dinero mueve no es la tarifa.** El 71,6 % del ahorro está en el término de potencia. La elección entre modalidades, que es la que más tiempo consume en cualquier comparativa comercial, vale un 0,3 % del resultado.

## Recomendaciones / Conclusiones

**Recomendación:** peaje 2.0TD en modalidad de precio único 24 horas, con 10 kW de potencia contratada.

La modalidad con discriminación horaria es marginalmente más barata (1,86 €/año), pero esa diferencia no es distinguible del error de medición. Se opta por el precio único porque el cliente prioriza explícitamente la libertad de consumo sobre una ventaja económica que el dato no puede sostener.

Sobre la potencia se contratan 10 kW y no los 7 kW que ya darían un margen del 17 % sobre la demanda máxima medida. Esa decisión cuesta 102,56 €/año adicionales, 55 veces más que la diferencia entre modalidades de tarifa, y es la decisión económica más relevante después de bajar de 16,44 kW. Se mantiene porque aquí sí existe una consecuencia real de equivocarse a la baja, un corte de suministro, y porque la potencia máxima se mide con resolución de 1 kW, de modo que el valor de 6 kW podría corresponder a cualquier valor entre 5,5 y 6,5 kW.

**Conclusión de método:** el valor del análisis no está en comparar tarifas, que es lo que hace cualquier comparador, sino en medir la demanda real antes de comparar nada. El cliente llevaba dos años pagando por una potencia que sus propios datos de contador demostraban innecesaria.

**Este análisis no es una proyección de facturas futuras.** Los precios se mantienen fijos en los doce meses simulados, por lo que responde a qué habría pagado el cliente con cada oferta, no a qué pagará.

## Próximos Pasos

| Acción                                                                                                                                                    | Responsable | Plazo                      |
| :-------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------- | :------------------------- |
| Conciliar el coste simulado del escenario actual con el importe real facturado, para acotar la desviación del modelo antes de dar la cifra por definitiva | Analista    | Antes de cerrar el informe |
| Tramitar el cambio de peaje y la reducción de potencia con la comercializadora                                                                            | Cliente     | Inmediato                  |
| Monitorizar la potencia máxima mensual durante los primeros seis meses para confirmar que 10 kW son suficientes y no se producen penalizaciones           | Analista    | 6 meses                    |
| Repetir el análisis con un tercer año de datos para distinguir patrón estructural de variabilidad estacional                                              | Analista    | 12 meses                   |
| Extender la comparativa a otras comercializadoras bajo el mismo peaje 2.0TD                                                                               | Analista    | Opcional                   |

## Fuentes de Datos

| Fuente                   | Descripción                                                                                                                      | Enlace                                     |
| :----------------------- | :------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------- |
| Curva horaria de consumo | 17.542 registros horarios de energía activa y reactiva inductiva (ene 2024 - dic 2025), descargados del portal de e-distribución | `data/data.xlsx`, hoja `Consumo`           |
| Registros del maxímetro  | 57 registros: los 3 mayores picos de potencia de cada uno de los 19 meses del histórico, con marca temporal y periodo tarifario  | `data/data.xlsx`, hoja `Potencia`          |
| Facturas reales          | Importe mensual facturado en 2025. Documentos recortados previamente para excluir cualquier dato identificativo                  | `data/data.xlsx`, hoja `Facturas`          |
| Precios de tarifas       | Precios de energía y potencia por tarifa y periodo de la oferta comercial comparada                                              | `data/data.xlsx`, hoja `Comparativa`       |
| Marco normativo          | Circular 3/2020 de la CNMC, metodología de cálculo de peajes de transporte y distribución                                        | https://www.boe.es/eli/es/cir/2020/01/15/3 |
| Modelo y visualización   | Dashboard de 4 pestañas, modelo de 9 tablas y 19 medidas DAX                                                                     | `dashboard/dashboard.pbix`                 |
