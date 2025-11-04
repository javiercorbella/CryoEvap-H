# Modelo 1D de Evaporación Criogénica en Estanques Horizontales

## Introducción



## 📘 Contexto del problema y relevancia para Chile

El almacenamiento criogénico es una tecnología clave para la transición energética, particularmente en la distribución de **hidrógeno líquido (LH₂)** y **gas natural licuado (GNL)**. En Chile, el interés por estas tecnologías está creciendo debido al desarrollo de la **industria del hidrógeno verde**, los proyectos portuarios asociados y las aplicaciones de **movilidad y respaldo energético** en zonas aisladas.

El modelamiento térmico y de evaporación (BOG, *Boil-Off Gas*) de estanques criogénicos permite cuantificar pérdidas energéticas, estimar tasas de evaporación y diseñar estrategias de operación más seguras y eficientes. Sin embargo, la mayoría de los estudios existentes se enfocan en tanques verticales, por lo que este trabajo busca **extender y adaptar los modelos a geometrías horizontales**, más representativas de estanques de transporte y almacenamiento intermedio.

---

## 🔬 Estado del arte

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

## 🧮 Modelo implementado

El modelo implementado corresponde a una adaptación del enfoque no en equilibrio de **Huerta & Vesovic (2019)** para estanques horizontales, bajo las siguientes hipótesis:

- Isobárico
- Evaporación de un líquido puro (LH₂, LNG, LN₂, etc.).
- Transferencia de calor por conducción y advección en el vapor.
- Interfaz líquido-vapor plana y lisa.
- Tanque aislado con ingreso de calor por paredes laterales.

En base al modelo para estanques verticales, se hizo una adaptación de las ecuaciones modificando la geometría para el caso horizontal. El modelo explicado se encuentra en el Jupyter Notebook "Modelo.ipynb"

---

## 🧱 Estanque a modelar

El estanque corresponde a un **cilindro horizontal** con tapas planas, típicamente utilizado para transporte terrestre o almacenamiento de GNL/LH₂ en plantas piloto.  
El código permite evaluar estanques con distintas dimensiones. En el Jupyter Notebook llamado "Modelado estanque 50m3", se encuentra la simulación de un estanque con dimensiones similares a las del estanque de Air Liquide "Hopu SR-57 LH2".

Los parámetros geométricos principales son:

| Parámetro | Símbolo | Valor típico | Unidad |
|------------|----------|--------------|--------|
| Diámetro interno | \( D_i \) | 2.5 | m |
| Largo | \( L \) | 10 | m |
| Volumen total | \( V_t \) | ≈ 50 | m³ |
| Nivel de llenado inicial | \( LF \) | 0.3–0.9 | - |
| Espesor de pared | \( e \) | 0.02 | m |
| Conductividad térmica del aislante | \( k_{ins} \) | 0.03 | W/m·K |

El modelo permite evaluar perfiles de temperatura, tasas de evaporación y flujos de calor en función del tiempo y del nivel de llenado.

---

## 📂 Estructura del repositorio


