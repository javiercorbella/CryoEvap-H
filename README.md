# Modelo 1D de Evaporación Criogénica en Estanques Horizontales

## Introducción



## Contexto del problema y relevancia para Chile

El almacenamiento criogénico es una tecnología clave para la transición energética, particularmente en la distribución de hidrógeno líquido (LH₂) y gas natural licuado (GNL). En Chile, el interés por estas tecnologías está creciendo debido al desarrollo de la industria del hidrógeno verde, los proyectos portuarios asociados y las aplicaciones de movilidad y respaldo energético en zonas aisladas.

El modelamiento térmico y de evaporación (BOG, *Boil-Off Gas*) de estanques criogénicos permite cuantificar pérdidas energéticas, estimar tasas de evaporación y diseñar estrategias de operación más seguras y eficientes. Sin embargo, la mayoría de los estudios existentes se enfocan en tanques verticales, por lo que este trabajo busca extender y adaptar los modelos a geometrías horizontales, más representativas de estanques de transporte y almacenamiento intermedio.

En el contexto chileno, donde se proyecta una rápida expansión de la cadena de valor del hidrógeno verde, incluyendo producción, transporte, almacenamiento y exportación, contar con modelos confiables para predecir el comportamiento térmico de estanques criogénicos es fundamental para disminuir pérdidas, mejorar la seguridad operacional y optimizar el diseño de infraestructura. La geografía del país, caracterizada por extensas distancias, zonas climáticas extremas y proyectos situados en puertos o regiones aisladas, hace especialmente relevante el estudio de estanques horizontales, que son la configuración dominante en transporte terrestre. En este sentido, el presente modelo contribuye directamente a la evaluación técnico-económica de proyectos futuros en Chile, permitiendo a empresas, centros de investigación y desarrolladores anticipar el rendimiento real de los sistemas criogénicos y apoyar decisiones de ingeniería con mayor rigurosidad.

Además, el desarrollo de tecnologías de almacenamiento criogénico tiene un impacto social, económico y ambiental significativo para Chile. Desde el punto de vista económico, una infraestructura criogénica eficiente reduce pérdidas por evaporación, disminuye costos operacionales y favorece la competitividad del país en la exportación de hidrógeno y sus derivados. En el ámbito ambiental, un control adecuado del BOG contribuye a minimizar emisiones fugitivas y a asegurar que la cadena del hidrógeno verde mantenga su carácter bajo en carbono. Finalmente, en términos sociales, la disponibilidad de tecnologías de almacenamiento más seguras y confiables habilita nuevas aplicaciones de energía limpia en regiones aisladas, mejora la resiliencia energética de comunidades y promueve la creación de empleos especializados vinculados a la transición energética. En conjunto, el avance en el modelamiento y comprensión de sistemas criogénicos constituye un habilitador clave para el desarrollo sostenible del país.

Mirando hacia el futuro, Chile presenta condiciones favorables para consolidarse como un actor relevante en tecnologías criogénicas asociadas al hidrógeno y otros vectores energéticos. La combinación de un potencial renovable excepcional, políticas públicas orientadas a la descarbonización, creciente inversión privada y una posición geográfica estratégica para mercados asiáticos y europeos crea un escenario favorable para la instalación de infraestructura de almacenamiento y transporte de hidrógeno líquido. La maduración de modelos como el desarrollado en este proyecto aporta a la factibilidad técnica y económica de implementar sistemas criogénicos a gran escala, permitiendo reducir riesgos, optimizar diseños y acelerar la curva de aprendizaje del país. En conjunto, estas capacidades fortalecen la posibilidad real de que Chile lidere la adopción de tecnologías criogénicas en Sudamérica y se proyecte como un ejemplo internacional de producción y exportación de hidrógeno verde en las próximas décadas.

---

## Estado del arte

Numerosos modelos se han desarrollado para predecir el comportamiento termodinámico de líquidos criogénicos dentro de estanques aislados. A continuación, se muestran ejemplos de investigaciones en las cuales se proponen y validan modelos de estanques cilíndricos horizontales, relevantes para el desarrollo del proyecto individual. 
Kalikatzarakis et. al. [1] desarrollaron un modelo dinámico de tanque criogénico horizontal utilizado para almacenas GNL en buques propulsados por gas natural licuado. 

El objetivo principal fue analizar el comportamiento del tanque bajo condiciones reales de operación, con el fin de determinar estrategias de control óptimas para evitar sobre presurización debido a la generación de Boil Off Gas (BOG). 
Se propone un modelo no estacionario con presión variable (no isobárico) pero con control para mantener la presión en límites definidos. El modelo separa el estanque en dos fases, líquido y vapor, y trata cada una por separado. 
Para modelar la transferencia de calor se asumió conducción y convección desde los alrededores al estanque. Por otro lado, los autores separan la contribución de calor desde el ambiente hacia cada una de las fases de manera independiente. 

Otro modelo fue propuesto por K.Appel [2], en su tesis sobre modelado de almacenamiento de hidrógeno líquido. En esta tesis se desarrollaron dos modelos, uno para estanques verticales y otro para horizontales. Ambos tienen los mismos principios y supuestos, pero difieren en las ecuaciones de la geometría del modelo. 
Este modelo cae en la categoría de dinámico no equilibrio térmico (NTEM). La tesis se enfoca en reducir perdidas por BOG mediante cambios operacionales como retorno de vapor, extracción de líquido, re-enfriamiento, patrones de venteo, entre otros. El modelo es no isobárico y se estructuró un modelo multi nodo (vapor, líquido e interfase). 

Recientemente, Al Ghafri et al [3] desarrollaron e implementaron un modelo en el paquete BoilFAST, que presenta un modelo termodinámico no equilibrio con vapor sobrecalentado (SHV). Este modelo estima auto-presurización y boil off de LH2 en distintas geometrías de tanque, incluidos horizontales con cabezales. 
El modelo también opera en condiciones no isobáricas, sin equilibrio térmico y modela dos nodos correspondientes a la fase líquida y vapor. 
La validación del modelo fue realizada frente a datos experimentales de un estanque horizontal de 125m3 del Jennedy Space Centre. El modelo confirma que la conducción es la que domina la transferencia de calor por sobre la convección en estanques grandes.

---

## Modelo implementado

El modelo implementado corresponde a una adaptación del enfoque no en equilibrio de **Huerta & Vesovic (2019)** para estanques horizontales, bajo las siguientes hipótesis:

- Isobárico
- Evaporación de un líquido puro (LH₂, LNG, LN₂, etc.).
- Transferencia de calor por conducción y advección en el vapor.
- Interfaz líquido-vapor plana y lisa.
- Tanque aislado con ingreso de calor por paredes laterales.

En base al modelo para estanques verticales, se hizo una adaptación de las ecuaciones modificando la geometría para el caso horizontal. El modelo explicado se encuentra en el Jupyter Notebook "Modelo.ipynb"

---

## Estanque a modelar

El estanque corresponde a un **cilindro horizontal** con tapas planas, típicamente utilizado para transporte terrestre o almacenamiento de GNL/LH₂ en plantas piloto.  
El código permite evaluar estanques con distintas dimensiones. En los Jupyter Notebook llamados "Air_Liquide_Tank", se encuentran las simulaciones de un estanque con dimensiones similares a las del estanque de Air Liquide "Hopu SR-57 LH2".

Los parámetros geométricos principales son:

| Parámetro | Valor típico | Unidad |
|------------|--------------|--------|
| Diámetro interno | 2.3 | m |
| Largo | 13.9 | m |
| Volumen total | 56 | m³ |
| Nivel de llenado inicial | 20 y 80 | % volumen de líquido |
| Coeficientes globales de transf. de calor | 0.0045 | W/m2 K |

Nota: Los coeficientes de transferencia de calor fueron calculados en base a obtener un BOR de 1%, valor estimado por bibliografía. 

Datos obtenidos de:

https://www.airliquidehoupu.com/productinfo/935696.html

https://www.airliquidehoupu.com/productinfo/935703.html

El modelo permite evaluar perfiles de temperatura, tasas de evaporación y flujos de calor en función del tiempo y del nivel de llenado.

---

## Archivos relevantes 
A continuación, se explican los archivos más relevantes para la correcta utilización del modelo.

CryoEvap/Modelo/horzontal_tank_model.ipynb : Jupyter Notebook que muestra la explicación de cada una de las ecuaciones implementadas en el modelo.

Cryoevap/cryoevap/storage_tanks/tank.py : implementa el modelo matemático, utilizando el método de líneas para resolver las ODE. 

Cryoevap/cryoevap/storage_tanks/plots.py : Archivo que define funciones para graficar variables relevantes del modelo. 

Cryoevap/notebooks/LH2_AirLiquide_tank_LF_0.8.ipynb : Jupyter Notebook que muestra la simulación de un estanque de 56 m3, en base a un nivel de llenado de 80% del volumen total en líquido

Cryoevap/notebooks/LH2_AirLiquide_tank_LF_0.2.ipynb : Jupyter Notebook que muestra la simulación de un estanque de 56 m3, en base a un nivel de llenado de 20% del volumen total en líquido



## Referencias

1.  Kalikatzarakis, M., et al., Model based analysis of the boil-off gas management and control for LNG fuelled vessels. Energy, 2022. 251: p. 123872.
2.	Appel, K., Numerical Modeling of Liquid Hydrogen Storage Tanks for the Reduction of Boil-Off Losses, J. Leachman, K. Matveev, and S. Banerjee, Editors. 2024, Washington State University.
3.	Wan, C., et al., Experimental study on self-pressurization and active pressure management in a horizontal liquid hydrogen tank. International Journal of Hydrogen Energy, 2025. 152: p. 149399.
4.	Lee, D.-H., et al., Practical Prediction of the Boil-Off Rate of Independent-Type Storage Tanks. Journal of Marine Science and Engineering, 2021. 9: p. 36.


## Créditos

Este trabajo fue desarrollado en conjunto con los siguientes autores, quienes formaron parte del proceso de modelación e implementación del código:

Ignacio Tapia
Felipe Huerta
Javier Corbella


