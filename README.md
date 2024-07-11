# Peptide Profiler Data Base (PPBD)

![Resumen gráfico](graphical_abstract.png)

## Introducción

La creciente resistencia a los antibióticos convencionales ha impulsado la búsqueda de nuevas alternativas terapéuticas. Entre estas, los péptidos antimicrobianos (AMPs) destacan debido a su eficacia en inhibir o eliminar microorganismos patógenos como bacterias, hongos y virus. Los AMPs ejercen su actividad antimicrobiana a través de mecanismos como la perturbación de la membrana celular, la interferencia con la síntesis de la pared celular, proteínas o ácidos nucleicos, y la activación de respuestas inmunológicas. Su capacidad para actuar en múltiples frentes reduce la posibilidad de que los patógenos desarrollen resistencia, convirtiéndolos en candidatos ideales para desarrollar nuevos medicamentos. Por otro lado, es importante considerar los péptidos sin actividad antimicrobiana (noAMP), aunque en la literatura no están definidos como un grupo. Estos péptidos pueden desempeñar otras funciones biológicas, como roles estructurales, de señalización o en la regulación de procesos celulares, pero no contribuyen directamente a la defensa contra infecciones.

El objetivo global de este trabajo es elaborar una base de datos o catálogo que recoja péptidos con actividad antimicrobiana y sin actividad antimicrobiana. Esta base de datos servirá como recurso fundamental para trabajar en problemas de clasificación mediante técnicas de machine learning. Al proporcionar un conjunto de datos amplio y bien caracterizado de péptidos, se facilitará el desarrollo y la evaluación de modelos de aprendizaje automático que puedan predecir la actividad antimicrobiana de nuevos péptidos. Esta aproximación tiene el potencial de acelerar el descubrimiento de nuevos AMPs y optimizar su diseño, contribuyendo así a la lucha contra la resistencia a los antibióticos.

## Creación de PPDB

Se han fusionado tres bases de datos de secuencias peptídicas con diversas actividades y orígenes: dbAMP 2.0 (https://doi.org/10.1093/nar/gkab1080), FermFooDb (FMDB; https://doi.org/10.1016/j.heliyon.2021.e06668 ) y el Data Repository of Antimicrobial Peptides (DRAMP; https://doi.org/10.1093/nar/gkab651 ). Para cada secuencia, se añadieron identificadores adicionales (PubMed, Uniprot, APD3) y targets específicos cuando fue posible. Se calcularon predictores estadísticos, fisicoquímicos y codificaciones (One-hot, Blosum 62, NFL, Z-scale y EDSSMat75) mediante ProPythia. Se implementó un proceso para aplanar y concatenar estas codificaciones en un solo vector con padding aplicado para asegurar que todas las secuencias tuvieran la misma longitud.

## Validación de PPDB como herramienta de predicción de AMP

Se aplicó un protocolo de filtrado basado en la longitud de las secuencias peptídicas, reteniendo solo aquellas secuencias de entre 7 y 150 aminoácidos para asegurar la consistencia de los datos. Se implementaron tres modelos de Random Forest para validar la base de datos: RF_FQ (predictores fisicoquímicos), RF_Encode (codificaciones) y RF_ALL (todos los predictores), optimizados mediante GridSearchCV. Posteriormente, se calcularon las matrices de confusión para determinar la sensibilidad y especificidad del mejor resultado de Random Forest para cada modelo. Se analizó la importancia de los predictores para cada modelo, permitiendo comparar la contribución de cada técnica de codificación al rendimiento del modelo.

## Análisis estadístico

Se realizó un análisis estadístico detallado para evaluar la composición y el enriquecimiento de las tres bases de datos originales (DRAMP, FMDB y dbAMP) comparándolas con nuestra base de datos desarrollada (PPDB). Este análisis incluyó técnicas de análisis de componentes principales (PCA)  UMAP, así como un análisis de clusterización mediante el algoritmo K-means.
