<img width="670" height="384" alt="image" src="https://github.com/user-attachments/assets/4096f1e6-6f4a-404b-89b2-c88eb45c5e32" /># MSFP2
Práctica 2 — Modelado y control del sistema cardiovascular mediante el modelo Windkessel

Repositorio académico de la asignatura Modelado de Sistemas Fisiológicos, del programa de Ingeniería Biomédica del Tecnológico Nacional de México / Instituto Tecnológico de Tijuana.

Esta práctica estudia el comportamiento dinámico del sistema arterial utilizando el modelo Windkessel de cuatro elementos. Se comparan tres condiciones simuladas —hipotenso, normotenso e hipertenso— y se diseñan controladores PID independientes para reducir las diferencias de presión respecto al modelo normotenso de referencia. Todo el trabajo se desarrolla mediante simulación in silico.

Estudiante: Maria Luisa Michelle Muñoz Meneses
Número de control: 23210714
Correo institucional: l23210714@tectijuana.edu.mx
Docente: Dr. Paul Antonio Valle Trujillo
Correo del docente: paul.valle@tectijuana.edu.mx
Asignatura: Modelado de Sistemas Fisiológicos
Carrera: Ingeniería Biomédica
Institución: Tecnológico Nacional de México / Instituto Tecnológico de Tijuana
Departamento: Ingeniería Eléctrica y Electrónica
Sede: Blvd. Alberto Limón Padilla s/n, Tijuana, C. P. 22454, B. C., México.

Repositorio de la asignatura: https://github.com/DrPaulValle/MSF-IBF1020
Contenido
1. Resumen
2. Competencia y objetivos
3. Introducción
4. Modelo Windkessel y analogía eléctrica
5. Variables y parámetros
6. Formulación matemática
7. Función de transferencia
8. Condiciones de simulación
9. Implementación en MATLAB y Simulink
10. Análisis en lazo abierto
11. Diseño y sintonización PID
12. Análisis en lazo cerrado
13. Implementación en Python
14. Verificación cruzada
15. Diagrama biológico
16. Actividades y entregables
17. Estructura del repositorio
18. Requisitos y reproducción
19. Resultados y conclusiones
20. Referencias
    
Resumen
El sistema cardiovascular puede analizarse mediante modelos matemáticos que relacionan la presión arterial, el flujo sanguíneo y las propiedades mecánicas de los vasos. En esta práctica se utiliza el modelo Windkessel de cuatro elementos, compuesto por una impedancia característica Z, una distensibilidad arterial C, una resistencia periférica R y una inertancia L.

Se obtiene una representación mediante ecuaciones diferenciales ordinarias y su función de transferencia. Posteriormente se simulan tres condiciones cardiovasculares cambiando únicamente la distensibilidad arterial. El modelo normotenso se utiliza como referencia para diseñar dos sistemas de control PID: uno para el caso hipotenso y otro para el hipertenso.

Las respuestas se comparan utilizando MATLAB, Simulink, Simscape Electrical y Python. Finalmente se relacionan los componentes del circuito con estructuras cardiovasculares mediante un diagrama biológico.

Palabras clave: Windkessel; sistema cardiovascular; presión arterial; flujo sanguíneo; distensibilidad arterial; controlador PID; MATLAB; Simulink; Simscape Electrical; Python; simulación in silico.

Competencia y objetivos

Competencia a desarrollar
Modelar sistemas fisiológicos mediante circuitos eléctricos equivalentes, ecuaciones diferenciales y funciones de transferencia para analizar su comportamiento dinámico y diseñar estrategias de control clásico.

Objetivo general
Analizar y comparar la dinámica de tres condiciones cardiovasculares simuladas mediante el modelo Windkessel de cuatro elementos y diseñar controladores PID que reduzcan las diferencias entre los casos hipotenso e hipertenso y la respuesta normotensa.

Objetivos específicos
- Identificar las variables hemodinámicas y su correspondencia con las magnitudes eléctricas.
- Aplicar las leyes de Kirchhoff para obtener el modelo de estados.
- Calcular la función de transferencia entre la presión de entrada y la presión arterial del modelo.
- Simular las tres condiciones con una misma señal de excitación.
- Comparar las respuestas de presión arterial en lazo abierto.
- Diseñar y sintonizar dos controladores PID independientes.
- Evaluar el seguimiento de referencia y el comportamiento transitorio en lazo cerrado.
- Reproducir las simulaciones en Python y comparar sus resultados con MATLAB/Simulink.
- Relacionar los elementos eléctricos con la anatomía y fisiología cardiovascular.
  
Introducción
La presión arterial depende de la interacción entre el flujo sanguíneo impulsado por el corazón y las propiedades de las arterias. La resistencia periférica, la capacidad de distensión de las paredes arteriales y los efectos inerciales de la sangre influyen en la respuesta del sistema.
El modelo Windkessel representa estas propiedades mediante una analogía eléctrica. Su versión de dos elementos incluye resistencia y capacitancia; la versión de cuatro elementos incorpora además la impedancia característica de la región proximal y la inertancia asociada al movimiento de la sangre.
En esta práctica se mantienen constantes Z, L y R, mientras que se modifica C para representar tres condiciones de estudio. Estos casos son modelos académicos simplificados: no constituyen una caracterización clínica completa de la hipotensión o la hipertensión.
Modelo Windkessel y analogía eléctrica
En el circuito, la impedancia Z y la inertancia L se encuentran en paralelo entre el nodo de entrada Pa(t) y el nodo Pp(t). Desde el nodo Pp(t), la distensibilidad C y la resistencia periférica R se conectan en paralelo hacia la referencia.

Magnitud cardiovascular	Equivalente eléctrico	Significado
Presión arterial	Voltaje	Diferencia de potencial de presión
Flujo sanguíneo	Corriente	Volumen de sangre transportado por unidad de tiempo
Z	Resistencia	Impedancia característica de la región arterial proximal
L	Inductancia	Inertancia de la sangre en movimiento
R	Resistencia	Oposición al flujo en la circulación periférica
C	Capacitancia	Distensibilidad o capacidad arterial de almacenar volumen ante cambios de presión


Figura 1. Circuito equivalente Windkessel de cuatro elementos. Agregar aquí la figura del instructivo o una representación propia: imagenes/windkessel.png.

[Circuito Windkessel de cuatro elementos](<img width="670" height="384" alt="image" src="https://github.com/user-attachments/assets/bde9c1f1-3fe0-415d-a7c5-fdbb8081619f" />)

Variables y parámetros
Variables principales
Símbolo	Descripción	Unidad
Pa(t)	Presión arterial de entrada	mmHg
Pp(t)	Presión asociada a la distensibilidad arterial; salida del modelo	mmHg
Fa(t)	Flujo sanguíneo total de entrada	ml/s
FL(t)	Flujo por la inertancia arterial	ml/s
FZ(t)	Flujo por la impedancia característica	ml/s
FC(t)	Flujo por la distensibilidad arterial	ml/s
FR(t)	Flujo por la resistencia periférica	ml/s


Parámetros de los tres modelos
Parámetro	Hipotenso	Normotenso	Hipertenso	Unidad
Z	0.010	0.010	0.010	mmHg·s/ml
L	0.001	0.001	0.001	mmHg·s²/ml
R	1.000	1.000	1.000	mmHg·s/ml
C	3.500	1.500	1.000	ml/mmHg


La diferencia entre los tres casos se encuentra únicamente en la distensibilidad $C$:
- Hipotenso: C=3.5 ml/mmHg. Mayor capacidad de distensión y almacenamiento de volumen.
- Normotenso: C=1.5 ml/mmHg. Modelo de referencia.
- Hipertenso: C=1.0 ml/mmHg. Menor capacidad de distensión y mayor rigidez arterial representada.
Una menor distensibilidad puede producir cambios de presión más pronunciados ante una variación del volumen sanguíneo.

Formulación matemática
Leyes de Kirchhoff
La presión entre los nodos de entrada y salida es la misma para las ramas Z y L:

Pa(t)-Pp(t) = L\frac{dF_L(t)}{dt}

Por lo tanto,
\[
\frac{dF_L(t)}{dt}=\frac{1}{L}P_a(t)-\frac{1}{L}P_p(t).
\]
El flujo a través de la impedancia característica es
\[
F_Z(t)=\frac{P_a(t)-P_p(t)}{Z}.
\]
Aplicando la ley de corrientes de Kirchhoff en el nodo de salida:
\[
F_L(t)+F_Z(t)=F_C(t)+F_R(t).
\]
Para la distensibilidad y la resistencia periférica:
\[
F_C(t)=C\frac{dP_p(t)}{dt},\qquad F_R(t)=\frac{P_p(t)}{R}.
\]
Al sustituir y despejar:
\[
\frac{dP_p(t)}{dt}=\frac{1}{C}F_L(t)-\left(\frac{1}{ZC}+\frac{1}{RC}\right)P_p(t)+\frac{1}{ZC}P_a(t).
\]
Representación en espacio de estados
Se seleccionan las variables de estado
\[
x_1(t)=F_L(t),\qquad x_2(t)=P_p(t),\qquad u(t)=P_a(t).
\]
El sistema se representa como
\[
\dot{x}(t)=Ax(t)+Bu(t),\qquad y(t)=Cx(t)+Du(t),
\]
con
\[
x(t)=\begin{bmatrix}F_L(t)\\P_p(t)\end{bmatrix},
\]
\[
A=\begin{bmatrix}
0 & -\frac{1}{L}\\
\frac{1}{C} & -\frac{1}{C}\left(\frac{1}{Z}+\frac{1}{R}\right)
\end{bmatrix},\quad
B=\begin{bmatrix}\frac{1}{L}\\\frac{1}{ZC}\end{bmatrix},
\]
\[
C_{\mathrm{salida}}=\begin{bmatrix}0&1\end{bmatrix},\qquad D=0.
\]
Aquí $C_{\mathrm{salida}}$ es la matriz de salida y no debe confundirse con el parámetro de distensibilidad arterial $C$.
Función de transferencia
Con condiciones iniciales nulas se aplica la transformada de Laplace. A partir de las ecuaciones de estado:
\[
LsF_L(s)=P_a(s)-P_p(s)
\]
\[
CsP_p(s)=F_L(s)+\frac{P_a(s)-P_p(s)}{Z}-\frac{P_p(s)}{R}.
\]
Al sustituir $F_L(s)$ y despejar la relación entrada-salida se obtiene
\[
\boxed{G(s)=\frac{P_p(s)}{P_a(s)}=\frac{R(Ls+Z)}{RLCZs^2+L(R+Z)s+RZ}.}
\]
Forma equivalente:
\[
G(s)=\frac{Ls+Z}{LCZs^2+L\left(1+\frac{Z}{R}\right)s+Z}.
\]
La función de transferencia es de segundo orden, con un cero y dos polos. Los coeficientes cambian según el valor de C utilizado en cada caso.
Funciones de transferencia de los casos
Sustituyendo Z=0.010, L=0.001 y R=1:
\[
G_{\mathrm{hipo}}(s)=\frac{0.001s+0.010}{0.000035s^2+0.00101s+0.010}
\]
\[
G_{\mathrm{normo}}(s)=\frac{0.001s+0.010}{0.000015s^2+0.00101s+0.010}
\]
\[
G_{\mathrm{hiper}}(s)=\frac{0.001s+0.010}{0.000010s^2+0.00101s+0.010}
\]

Estas expresiones deben implementarse y verificarse contra los modelos por ecuaciones de estado y circuito equivalente.

Condiciones de simulación
Las tres condiciones deben recibir exactamente la misma realización de la señal aleatoria para que las diferencias observadas dependan de los parámetros y no de entradas distintas.
- Intervalo: $0\leq t\leq15$ s.
- Entrada: señal aleatoria Pa(t), común a los tres modelos.
- Salida: presión Pp(t).
- Referencia de control: respuesta normotensa $P_{p,\mathrm{normo}}(t)$.
- Condiciones iniciales: emplear las mismas condiciones iniciales para comparar las representaciones.


Para cada condición se sustituyen los parámetros de la tabla sin modificar la estructura del modelo. Las señales deben almacenarse en el Workspace para facilitar las comparaciones.

Análisis en lazo abierto
Aplicar la misma entrada a los tres modelos sin controladores y registrar
\[
P_{p,\mathrm{hipo}}(t),\qquad P_{p,\mathrm{normo}}(t),\qquad P_{p,\mathrm{hiper}}(t).
\]
La comparación debe considerar las diferencias en amplitud, variaciones de presión y respuesta transitoria asociadas con los valores de distensibilidad.

Evidencia pendiente: agregar la gráfica de los tres modelos en lazo abierto, identificando ejes, unidades y leyenda.
<!-- ![Comparación en lazo abierto](resultados/[Individuos.pdf](https://github.com/user-attachments/files/33846906/Individuos.pdf)) -->

Diseño y sintonización PID
Se construyen dos sistemas de control independientes, uno normotenso–hipotenso y otro normotenso–hipertenso. En ambos, el modelo normotenso proporciona la referencia.
Errores de seguimiento
Para el caso hipotenso:
\[
e_{\mathrm{hipo}}(t)=P_{p,\mathrm{normo}}(t)-P_{p,\mathrm{hipo}}(t).
\]
Para el caso hipertenso:
\[
e_{\mathrm{hiper}}(t)=P_{p,\mathrm{normo}}(t)-P_{p,\mathrm{hiper}}(t).
\]
La ley ideal de un controlador PID es
\[
u_c(t)=k_Pe(t)+k_I\int_0^t e(\tau)\,d\tau+k_D\frac{de(t)}{dt}.
\]
En Laplace:
\[
K(s)=k_P+\frac{k_I}{s}+k_Ds.
\]

La señal de control se aplica al modelo del paciente según el esquema de retroalimentación indicado en la práctica. Debe conservarse el modelo normotenso como referencia y no sustituirlo por una señal arbitraria.
Sintonización
Utilizar Tune del bloque PID Controller en Simulink para determinar las ganancias de manera independiente:
Controlador	kP	kI	kD
Hipotenso	Pendiente	Pendiente	Pendiente
Hipertenso	Pendiente	Pendiente	Pendiente


El ajuste debe buscar una respuesta estable y una reducción del error respecto a la referencia normotensa. Registrar las ganancias obtenidas y conservar una captura de la configuración utilizada. El material no establece valores numéricos obligatorios para las ganancias.
Análisis en lazo cerrado
Repetir las simulaciones con los controladores sintonizados.

Para el caso hipotenso, comparar
\[
P_{p,\mathrm{normo}}(t),\quad P_{p,\mathrm{hipo}}(t),\quad P_{p,\mathrm{hipo,PID}}(t).
\]
Para el caso hipertenso, comparar
\[
P_{p,\mathrm{normo}}(t),\quad P_{p,\mathrm{hiper}}(t),\quad P_{p,\mathrm{hiper,PID}}(t).
\]
Analizar la reducción del error, la estabilidad, el seguimiento de referencia y las diferencias del transitorio. Los resultados de los dos controladores deben presentarse por separado.

Evidencias pendientes: resultados/[hipotenso_matlab.pdf](https://github.com/user-attachments/files/33846951/hipotenso_matlab.pdf) y resultados/[hipertenso_python.pdf](https://github.com/user-attachments/files/33846959/hipertenso_python.pdf).
Implementación en Python
Reproducir en Visual Studio Code las tres funciones de transferencia con los mismos parámetros y la misma señal de entrada utilizada en MATLAB/Simulink.

El programa debe:
1. Definir los parámetros Z, L, R y los tres valores de
   C.
3. Construir $G_{\mathrm{hipo}}(s)$, $G_{\mathrm{normo}}(s)$ y $G_{\mathrm{hiper}}(s)$.
4. Importar o reproducir exactamente la señal de excitación común.
5. Calcular y representar las respuestas en lazo abierto.
6. Incorporar las ganancias PID obtenidas mediante Tune.
7. Simular los casos hipotenso e hipertenso en lazo cerrado.
8. Generar y guardar las figuras para compararlas con MATLAB.
Las bibliotecas necesarias deben registrarse según los módulos que se utilicen realmente en el archivo .py. Para una comparación válida se debe revisar también la interpolación y discretización de la señal aleatoria.

Verificación cruzada

Se deben contrastar cinco representaciones de los tres casos:
Método	Herramienta	Aspecto que se compara
Ecuaciones de estado	Simulink	Evolución de FL(t) y Pp(t)
Función de transferencia	Simulink	Respuesta entrada–salida
Circuito Windkessel	Simscape Electrical	Respuesta del circuito equivalente
Cuaderno computacional	MATLAB	Gráficas y datos recuperados del Workspace
Implementación independiente	Python	Respuestas con los mismos parámetros y controladores


Las diferencias pueden depender de la configuración del solucionador numérico, las condiciones iniciales, la discretización de la entrada aleatoria o errores de implementación. No se deben afirmar coincidencias sin revisar las gráficas o los datos obtenidos.
Diagrama biológico
Elaborar en BioRender o una herramienta equivalente un diagrama cardiovascular que incluya, como mínimo:
- Corazón.
- Aorta.
- Grandes arterias.
- Vasos periféricos.
- Flujo sanguíneo.
- Presión arterial.
- Distensibilidad arterial.
- Resistencia periférica.
Correspondencia fisiológica
Elemento del modelo	Relación fisiológica
Z Impedancia característica de la aorta proximal
L	Inertancia debida a la masa de sangre y su aceleración
C	Distensibilidad de las paredes arteriales
R	Resistencia vascular periférica
Pa(t)	Presión arterial de entrada
Pp(t)	Presión del compartimento arterial distensible
Fa(t)	Flujo sanguíneo de entrada


Se puede utilizar un mismo diagrama anatómico para explicar los tres casos, identificando los cambios de C que corresponden a cada uno.

Evidencia pendiente: imagenes/[Maria Luisa Michelle's First Illustration.pdf](https://github.com/user-attachments/files/33847406/Maria.Luisa.Michelle.s.First.Illustration.pdf)
Actividades y entregables
Etapa 1. Análisis matemático
- [ ] Identificar variables y parámetros del circuito.
- [ ] Relacionar cada elemento con su propiedad hemodinámica.
- [ ] Aplicar las leyes de Kirchhoff.
- [ ] Obtener las dos ecuaciones de estado.
- [ ] Formular las matrices del sistema.
- [ ] Obtener y verificar la función de transferencia.
Etapa 2. Simulación
- [ ] Construir los modelos en Simulink por ecuaciones de estado.
- [ ] Construir los modelos mediante funciones de transferencia.
- [ ] Construir el circuito en Simscape Electrical.
- [ ] Generar una única realización de la señal aleatoria.
- [ ] Simular los tres casos en el intervalo de 0 a 15 s.
- [ ] Comparar las presiones en lazo abierto.
Etapa 3. Controladores
- [ ] Implementar el control PID del caso hipotenso.
- [ ] Implementar el control PID del caso hipertenso.
- [ ] Sintonizar ambos controladores con Tune.
- [ ] Guardar las ganancias y las capturas de sintonización.
- [ ] Comparar referencia, caso sin control y caso controlado.
Etapa 4. Verificación y documentación
- [ ] Elaborar el cuaderno computacional MATLAB .mlx.
- [ ] Crear una función de gráficas con variables, unidades y leyendas.
- [ ] Guardar las figuras en PDF.
- [ ] Reproducir las funciones de transferencia en Python.
- [ ] Comparar los cinco métodos de simulación.
- [ ] Elaborar el diagrama cardiovascular en BioRender.
- [ ] Incorporar las evidencias y conclusiones al repositorio.


Requisitos y reproducción
Software
- MATLAB y Simulink.
- Simscape Electrical.
- Bloque PID Controller y herramienta de sintonización Tune.
- Python y Visual Studio Code.
- BioRender o herramienta equivalente.
- Git y GitHub.
Procedimiento general
1. Definir los parámetros de los tres modelos.
2. Construir el modelo de estados y la función de transferencia.
3. Implementar el circuito equivalente en Simscape Electrical.
4. Generar y conservar una sola señal aleatoria para todos los casos.
5. Simular las tres condiciones durante 15 segundos.
6. Obtener la respuesta normotensa como referencia.
7. Sintonizar independientemente los dos PID.
8. Ejecutar las simulaciones controladas.
9. Reproducir los resultados mediante MATLAB y Python.
10. Comparar gráficas y completar el análisis fisiológico.
11. Incorporar el diagrama biológico y las evidencias al repositorio.
    
Resultados y conclusiones
Resultados
Pendientes de completar después de ejecutar las simulaciones. Se incorporarán las gráficas de los tres modelos en lazo abierto, las respuestas con control PID, las ganancias obtenidas y la comparación entre herramientas.
Conclusiones
El modelo Windkessel de cuatro elementos permite relacionar la presión y el flujo sanguíneo con propiedades arteriales mediante un circuito eléctrico equivalente. Al variar la distensibilidad se pueden estudiar diferencias en el comportamiento dinámico de tres condiciones simuladas. La incorporación de controladores PID permitirá evaluar, una vez realizadas las simulaciones, en qué medida se reduce el error respecto a la respuesta normotensa.

La verificación entre MATLAB, Simulink, Simscape Electrical y Python es importante para comprobar la consistencia de las implementaciones. Las conclusiones cuantitativas sobre el desempeño de los controladores se añadirán después de obtener los resultados.
Nota de alcance: las estrategias de control se estudian exclusivamente con fines académicos y de simulación; no representan tratamientos ni recomendaciones clínicas.

Referencias
[1] M. C. Khoo, Physiological Control Systems: Analysis, Simulation, and Estimation, 2nd ed., IEEE Press, 2018.

[2] F. C. Hoppensteadt y C. S. Peskin, Modeling and Simulation in Medicine and the Life Sciences, Springer.

[3] J. E. Hall, Guyton and Hall Textbook of Medical Physiology, 14th ed., Elsevier, 2021.

[4] K. Ogata, Ingeniería de Control Moderna, 5.ª ed., Pearson Educación, 2010.

[5] N. S. Nise, Control Systems Engineering, 8th ed., John Wiley & Sons, 2020.

[6] P. A. Valle, Syllabus para Modelado de Sistemas Fisiológicos, Tecnológico Nacional de México / Instituto Tecnológico de Tijuana, Tijuana, B. C., México, 2026. https://biomath.xyz/course/

[7] Tecnológico Nacional de México, Programa de estudio de la asignatura Modelado de Sistemas Fisiológicos, IBF-1020.
