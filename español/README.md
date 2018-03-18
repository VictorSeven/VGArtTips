# Arte para videojuegos -consejos básicos    

Esta página contiene consejos para realizar gráficos que puedan ser usados cómodamente por programadores. **Ten cuenta que esto NO es un tutorial sobre cómo dibujar sprites o hacer arte en general.** El objetivo es más bien orientar al artista a cómo debe presentar su trabajo para que pueda usarse directamente en el juego, sin carga de trabajo extra para el programador o necesidad de hacer retoques posteriores al material.    

>  **¡Contribuye!** Ayuda a más artistas a hacer arte para juegos: si programas en cierta plataforma específica que tenga requerimientos especiales, añade una sección al final del documento con tu engine y sus particularidades para gráficos con una pull request.    

## 2D: consejos generales    

### Formato PNG, siempre    

En general, si no recibes instrucciones expresas de hacer lo contrario, exporta siempre los sprites a formato PNG. Este es compatible con prácticamente cualquier engine de videojuegos, es ligero y soporta transparencias.    

### Nombra correctamente el archivo    

La programación, con los nombres, siempre es un poco quisquillosa.  Aunque son fáciles de cambiar, requiere tiempo del programador renombrar una buena cantidad de imágenes. Sigue estas reglas para evitar problemas con los nombres de archivo:    

1. Ojo con el espaÑol. Evita los nombres de archivo que contengan ñ, tildes, u otros caracteres especiales. Algunos motores podrían tener problemas para cargar estas imágenes.  
2. Evita los nombres que contengan espacios. Aunque a menudo estos no tienen por qué suponer un problema, en programación se prefiere trabajar siempre con archivos sin espacios. Usa guión bajo (`_`) en su lugar. 
3.  Sé ordenado. Si envías muchos gráficos en varias carpetas, procura seguir estas reglas también para las carpetas. Intenta que los gráficos estén separados más o menos por categorías (gráficos niveles, enemigos, personajes...).    

### Transparencia de fondo    

Los sprites deben tener algo que se identifique con un fondo transparente. Muchos motores utilizan el color (255, 0, 255) con este propósito. En otros, simplemente, puedes eliminar el fondo para que haya  transparencia. Pregunta siempre a tu programador cuál es la opción preferida.

### Tamaño   

El tamaño de la imagen suele ser un factor importante. Ten en cuenta las siguientes reglas generales:

1. Cuando una memoria se carga en el juego, esto se hace en la RAM. Cargar muchas texturas, de gran tamaño, lleva a requerir una cantidad respetable de memoria. Intenta evitar, en general, texturas demasiado grandes. Esto es especialmente importante en el caso de Android, donde los dispositivos son más limitados. Como regla general, evita texturas mayores de 2048x2048 píxeles siempre. Si necesitas algo más grande, simplemente divídelo en varias texturas.
2. Si puedes, ajusta siempre el tamaño de las imágenes a potencias de 2. Algunos motores de videojuegos pueden aprovechar esto para optimizar la carga en memoria de las imágenes. Algunos motores retro solo admiten estos tamaños.

### Tilesets    

Un *tileset* es una imagen maestra que contiene todos los *tiles* o bloques que se usan para construir los niveles. A la hora de hacer y enviar un tileset, ten en cuenta los siguientes consejos:    

1. Los tiles deben tener tamaño fijo. Usualmente se usan potencias de 2. (16x16, 32x32, 64x64...).  
2. Lo mejor es ordenarlos en una especie de tabla, con filas y columnas. Al hacerlo, pueden ponerse juntos tiles para que se vea cómo funcionan.
3. Si has dejado algunos píxeles de margen entre el primer píxeles y el principio de la tabla, házselo saber al programador.
4. Ten cuenta que muchos motores pueden girar o reflejar las imágenes, luego no es necesario hacer plataforma izquierda / plataforma derecha. Solamente con la izquierda, el motor puede obtener la otra sin problema, reduciendo el tamaño de imagen considerablemente.

Es importante que se vea ordenado, de golpe de vista.  Por ejemplo, [este tileset](https://telles0808.deviantart.com/art/RPG-Maker-VX-RTP-Tileset-159218223) tiene todos los tiles con tamaño fijo, y está claramente ordenado. Además, los tiles aparecen más o menos juntos. Se entiende cuáles deben usarse en conjunto y de qué manera. Todos los objetos han sido preparados para funcionar al ser cortados en trocitos.  
  
Para juegos de plataformas, a veces es necesario, además de los tiles, tener ciertos objetos decorativos. Muchos serán simplemente del mismo tamaño que el mapa y se pueden encajar dentro de un tile. Sin embargo, otros serán mucho más grandes. Si son objetos estáticos hay dos opciones:  
  
1. Cuadrarlos dentro de la tabla, por ejemplo, con un árbol que ocupe 3x5 tiles. Sin embargo, no se debe romper el orden de la tabla bajo ningún concepto.  
2. Que no sigan en absoluto el orden del tileset. La forma más sencilla, en mi opinión, es hacer una imagen aparte para el objeto. Si preferimos incluirlo dentro del propio tileset hay que ser cuidadoso, indicando al programador las coordenadas donde se encuentra esta imagen (x,y) y su tamaño. No olvides indicar también en qué coordenada empieza la tabla de tiles. Esto se puede enviar en un fichero de texto adjunto con las imágenes.  
  
> Las coordenadas dependen del motor. Usualmente el (0,0) está en la esquina superior izquierda, con x aumentando hacia la derecha e y hacia abajo. En caso de duda, consulta con el programador.  
  
Para los objetos que sean animados o que se muevan, lo mejor es hacerles una imagen aparte para ellos solos. Estos casos suelen ser, sin embargo, más particulares y probablemente recibas instrucciones explícitas del programador.

### Animaciones

Los personajes, enemigos, y otros elementos del juego suelen estar animados. Los consejos para realizar las animaciones son similares a los del tileset, si bien en este caso a menudo debemos ser más flexibles y el diseño se complica un poco.

Para empezar, lo ideal es que todas las animaciones tengan el mismo tamaño de fotograma y vayan empaquetadas en una única imagen organizada como una tabla, el *spritesheet*. Si el fotograma más alto tiene 36 px, la altura de cada fotograma será 36 px, incluso cuando la mayor parte de los demás fotogramas tengan, por ejemplo, 32 px. Esto hace sencillo cargar todas las animaciones. 

Una excepción importante a esta regla es cuando unos pocos fotogramas son exageradamente grandes con respecto al resto -ya que estaríamos haciendo una textura enorme con demasiado espacio vacío. En este caso, tal vez es mejor hacer una imagen distinta por cada animación, de modo que se aproveche mejor el espacio. 

Con esto en mente, estas son aproximadamente las reglas:

1. Si has organizado el spritesheet como una tabla, di al programador en fila y columna empieza cada animación y cuántos fotogramas tiene.  Una práctica usual es que cada fila de la tabla sea una animación distinta, para poder verlo de forma sencilla a golpe de vista.
2. Generalmente se asume que cada frame es visible durante cierto tiempo. A veces, la animación queda más dinámica si algunos frames están durante más tiempo en pantalla. Esto es algo que has indicar expresamente al programador que lo añada.
3. Al igual que ocurre con los tileset, no es necesario hacer sprites del personaje moviéndose a izquierda y derecha, solamente una de las direcciones basta. 
4. Cuando usas diferentes imágenes para cada animación, **ten cuidado de centrar siempre correctamente el sprite**, porque si no al cambiar de animación tendŕa movimientos "raros".  

Un ejemplo extremo de este último caso es el siguiente: dos animaciones,  A y B. Los fotogramas de A tienen 32x64 píxeles, y los de B 32x72.  En muchos motores,  al cambiar de animación de A a B, el personaje se teletransportará hacia abajo, ya utilizan como (0,0) la esquina superior izquierda. Al haber un montón de espacio vacío en B, se desplaza hacia abajo el personaje. La solución es añadir una corrección a la posición, subiendo el sprite 72-64 = 8 píxeles. Procura indicar siempre esta corrección al programador. 
En el eje X normalmente no hay este problema, así que intenta que el sprite quede siempre centrado en esta dirección.
