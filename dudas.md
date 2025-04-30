## Denominación  del grupo de pruebas Modelo A [Parte Tesis]
Variables (features)  
Día del año; Código de ría; Temperatura; Salinidad; bloom semana previa; 
bloom 2 semanas previas; Afloramiento actual; Afloramiento día previo; 
Afloramiento dos días previos; Afloramiento tres días previos; 
Afloramiento cuatro días previos.  

## Variables usadas por mi parte:
- TEMPERATURA	-> Temperatura de 1_5m
- SALINIDAD	-> Salinidad de 1_5m
- STATION	-> Las estaciones usadas fueron las M5, A0, P4 y V5
- UI	-> Índice de afloramiento
- UI_1, UI_2, UI_3, UI_4 -> valores del UI a 1,2,3,4 días previos
- PSEUSPP	-> valor de la Pseudo-nitzschia
- BLOOM, BLOOM_1w, BLOOM_2w	-> valor de BLOOM (1) 0 (-1) cuando no hay, y los valores de shift(1) una semana previa y shift(2) dos semanas previas 
- BLOOM_PREDICT	-> valor de BLOOM a una semana vista shift(-1)
- CA_G_1	-> valor de la Clorofila Grande A 
- RIA	 -> RIA [1,2,3,4]
- COD_BLOOM -> valor de 0 a 15 dependiendo de BLOOM y RIA 
- DAY	 -> Dia del año
- VAR_TEMPERATURA	-> variación de temperatura de una semana atrás y la actual
- VAR_SALINIDAD	-> variación de salinidad de una semana atrás y la actual


1. Todos los datos fueron escalados a -1,1 según pg 68 tesis apartado e)
2. Modelo usado: kérnel gaussiano, y además se han utilizado núcleos polinómicos de potencias de varios grados (como en la tesis)


### Dudas 
1. Los resultados no coinciden y se ven muy afectados en la métrica de Kappa por lo que no acierta tanto al predecir los Blooms
2. La cantidad de datos usados en prácticamente la misma y se puede ver en alguna gráfica de contar blooms que tengo una cantidad casi igual a la usada en la tesis
   entre los años 2002 y 2012

Sobretodo me gustaría saber en qué estoy fallando o que cosas me falta por hacer
