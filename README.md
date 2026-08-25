Estimado profesor,

Por la presente comparto la reentrega de la Parte III junto con un detalle claro de cada corrección aplicada. En entregas anteriores hubo algo de confusión con las versiones del trabajo, así que esta vez dejé todo bien especificado punto por punto:

Dataset  
Reemplacé el dataset generado manualmente (que había sido el motivo del rechazo inicial) por uno real con 50.000 estudiantes y 16 variables. El archivo impacto_ia_estudiantes.xlsx está en el repositorio junto al notebook.

Codificación de variables nominales  
Ajusté este punto según tu devolución. Las variables nominales sin orden natural (Major_Category, Primary_Use_Case, Institutional_Policy) ahora usan One-Hot Encoding. Las ordinales (Year_of_Study, Prompt_Engineering_Skill, Paid_Subscription) se codifican con un diccionario que respeta su orden semántico. Ya no hay Label Encoding en ninguna parte del notebook.

Data leakage en objetos con .fit()  
Los únicos objetos que requieren ajuste se entrenan exclusivamente con el conjunto de entrenamiento:

ohe.fit(X_train[COLS_NOMINALES])

selector.fit(X_train_enc, y_train)  
Luego se aplican con .transform() por separado en train y test. La división train/test ocurre antes de cualquier transformación.

Correlación y variable binaria  
El mapa de calor calcula correlación solo entre variables numéricas entre sí, sin incluir el target. En el código se ve claramente: df[vars_num].corr(), donde vars_num contiene únicamente predictores numéricos. No se calcula correlación Pearson contra la variable objetivo.

Selección de atributos  
Incorporé SelectKBest con el estadístico F de ANOVA (f_classif), que es el método adecuado para comparar variables continuas con un target binario. El selector también se ajusta únicamente sobre el conjunto de entrenamiento.

Algoritmo  
Cambié el modelo a DecisionTreeClassifier, tal como se vio en clase. Entiendo que el criterio era usar Árbol de Decisión o KNN. Sé que algunos compañeros usaron otros algoritmos y fueron aprobados, pero en mi caso seguí estrictamente lo indicado en la devolución.

Evaluación en train y test  
El modelo se evalúa en ambos conjuntos. Las métricas (accuracy, recall, classification report y matriz de confusión) están en celdas consecutivas para train y test. La comparación muestra que no hay sobreajuste significativo.

Notebook ejecutado  
Todas las celdas están ejecutadas y con sus outputs visibles. El archivo pesa 546 KB con los resultados incluidos.

Uso de IA en el trabajo  
Aclaro explícitamente que el uso de herramientas de IA se limitó únicamente a ordenar y mejorar la presentación del notebook. No intervino en la selección de variables, en la construcción metodológica del trabajo, ni en ninguna de las decisiones técnicas o analíticas. Todo el contenido, las transformaciones, el modelo y la estructura del proyecto fueron desarrollados íntegramente por mí.

El repositorio actualizado está acá:
https://github.com/sofidemier/ProyectoParteIII-Algamiz

Quedo a disposición por cualquier duda.
Gracias.

Sofía Algamiz
