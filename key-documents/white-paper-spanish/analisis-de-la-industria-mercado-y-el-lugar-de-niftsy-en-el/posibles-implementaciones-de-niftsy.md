# Posibles implementaciones de NIFTSY

Viendo al mercado en general, los siguientes [segmentos](https://niftsy.medium.com/nfts-market-meta-analysis-by-niftsy-e9f131234041) de intención son importantes de mencionar para la parte de protocolo de NIFTSY a ser implementada primero (MVP - marzo-abril-2021, Alfa - mayo-julio de 2021):

1. **Mercados** (OpenSea, rarible, NFT stars y otros):&#x20;
   1. En un lado, los puntos de implementación del protocolo; en el otro los compradores B2B de atados y otros productos NFT complejos. Eso es para el proyecto y el protocolo los mercados son los puntos de venta al por menor de los NFT creados con el protocolo.
   2. Varios casos son posibles. Aquí hay uno de ellos: el dueño de una NFT entrega en garantía un activo digital dentro de una NFT de segundo orden recientemente creada, que funciona como una garantía inquemable del valor de la NFT para cualquier dueño del activo (esto crea un precio seguro de balance: un piso).
   3. La precedía de un valor base definido como piso incrementa el interés en los compradores en el activo: cualquier cosa puede caer a 0, pero si un activo contiene apoyo mínimo es mucho mejor que un activo sin apoyo. Adicionalmente en la segunda etapa está el oráculo, que da una valuación independiente de activos en que ya se encuentran en la primera etapa - WUM.
   4. El autor/dueño/otra persona en el momento de circulación de la NFT define las mecánicas para incrementar el valor base de la MFT en ciertos eventos, (transacciones, caídas, etc) para incrementar el atractivo de intercambiar su NFT; y activo que el protocolo trabaja junto con la funcionalidad utilitaria de el token NIFTSY.
2. **Protocolos** (NFTx, NFT20, NFT, DoDoNFT, etx.):
   1. Primero los servicios usados en la parte del oráculo del proyecto, osea los proveedores de datos del protocolo son solo diferentes protocolos, soluciones blockchain, oráculos de tipos particulares etc.
   2. Segundo, elementos incrustados de protocolos de siguiente nivel dentro del protocolo: osea, el protocolo está construido en nivel 1 pero es posible extender su funcionalidad el nivel 2, por ejemplo a través de la implementación de polygon&#x20;
3. **Plataformas** de creación de NFTs, incluyendo niveles bajos (Nivel 0 (L0)/Nivel 1 (L1)):
   1. Primero que nada - proveedores de NFT para colateral.
   2. Consumidores de activos, para los cuales el protocolo es una confirmación cero para los NFT entregados en garantía de cualquier orden de cripto activos.
   3. Así, el protocolo funciona como una manera no sólo de crear NFTs pero también para verificar automáticamente a las expensas de la presencia/ausencia de la porción entregada en garantía al mismo tiempo.
4. **Lanzadores de NFT**:
   1. El protocolo puede ser usado para lanzar ("Drop") tokens de cualquier formato mientras tengas un atado de NFT
   2. Algoritmo de IDO vía NFT
      1. Un "Startup" (DAO) emite un set de diferentes NFTS
      2. Apila los tokens ERC/BEP-20/ETC de su proyecto en la NFT (ejemplo: formato  de 100/500/1000/5000)
      3. Después define el costo de la NFT
      4. Finalmente describe las condiciones de rodaje de la NFT, vamos a decir que podría ser para él tiempo - después de una semana/ después y/o para cuando Ethereum/Bitcoin/BSC/ llegue a una altura de bloque. Adicionalmente las condiciones piden ser no los en el rango de tiempo pero también en cualquier rango cuantitativo o de evento
      5. Una vez que la NFT es desplegado, la contraparte (participante en la IDO) recibe la cantidad de ERC-20 y/o otros tokens intercambiables a una cartera (cuenta)
5. **Mercados de valoración de NFT**:
   1. El protocolo (en conjunto con el oráculo e índice) permiten brindar una determinación del valor exacto de la NFT basó en herramientas analítica a la precisión deseada como
      1. Hay un valor inicial de el valor intrínseco subyacente
      2. Un coeficiente/multiplicador del valor subyacente de cualquier orden también puede ser introducido
      3. Así que, no es difícil determinar el valor de un token que en consecuencia puede ser soportado por una piscina de liquidez y/o otros parámetros de piso
      4. Finalmente cuando el oráculo está conectado también conseguimos algoritmos para estimar el valor de mercado de la NFT fuera de los sujetos que requieren confianza
6. **DeFi**:
   1. Por supuesto ya hay casos hoy en día dónde se usan NFTs como un objeto se intercambió, colateral, depósito, etc. Pero eso solo recientemente que la transferencia de liquidez a través del segmento NFT se ha vuelto posible.
   2. De hecho, esto significa que en los siguiese 1 a 3 años tendremos un nuevo tipo de activo DeFi, donde una NFT ya contiene un colateral mientras que el colateral mismo puede ser también complejo como se desee, lo que significa un punto de entrada alto, mientras que el protocolo hace la entrada al mercado disponible al público general.
7. **Gaming en línea (principalmente P2P)**:
   1. Los tokens de formato 1155 y 998 fueron creados originalmente para la industria de juegos.
   2. El valor colateral de activos de juegos es un tema de debate constate y el protocolo puede solucionar este problema en 2 formas&#x20;
      1. A través del oráculo
      2. Directamente, dando un precio de umbral menor
   3. Es también posible crear un disco multi-colateral dentro de la MFT inicial, donde cada activo podría ser ubicado a la parte del disco que corresponde a un juego particular (series de juegos)&#x20;
8. **Meta-universos**:
   1. Está categoría no es algo entre realidad aumentada (aumentada mixta), realmente pero trata sobre mundos en línea dentro de juegos, espacios de realidad virtual, etc
   2. Ejemplo: si tienes tierras agua y las semillas correcta puedes cultivar un árbol del cual puedes cosechar activos digitales, etc pero si ese árbol solo está disponible dentro de un mundo el valor de las semillas sería bajo, mientras que la dificultad de accesibilidad desde diferentes mundos hará al contraria que ese objeto VR/AR/MR aumente de valor
   3. De nuevo es el protocolo multicolateral lo que es una propiedad importante aquí
9. **El mercado de cyber-deportes**:
   1. Uno de los posibles contendientes para los mercados del trillón de dólares&#x20;
   2. Los artefactos en el ya son valiosos: ejemplo el "arma" condicional aumenta de valor con el aumento del valor intrínseco básico debido a largos tiempos de guardado, número de transacciones de compra y venta, intercambios desarrollados etc.
   3. Por otra parte emitir tokens de fanáticos también es posible dónde, de nuevo hay una mezcla de mundos virtuales y la realidad&#x20;
   4. Un objeto de aplicación separado del protocolo en atar a través de NFT dende WUM podría ser aplicado a premios, copas y otros bonos; más desarrollo es posible, por ejemplo a través de de añadir propiedades económicas multiplicando el valor del evento
   5. Por supuesto, tickets de eventos, vouchers de regalo que aumenta en valor para la fecha del evento y más también son comerciables vía el protocolo&#x20;
10. **Mercado de deportes clásicos**:
    1. cartas para jugadores  favoritos: la industria del fútbol es famosa por esto en el momento, pero el tiempo no está muy lejos, donde todos los deportes están digitalizados en algún grado y los NFT claramente jugarán un papel aquí.
    2. La apuestas de deportes descentralizadas también es un gran área de discusión
11. **El mercado de realidad aumentada  (AR) y realidad virtual (VR) mismo así como nuevas especies (XR/MR) y la adquisición de activos digitales como resultado de cierto actos dentro del espacio digital**:
    1. Quizá el ejemplo más importante y al mismo tiempo el más obvio es la reserva programada de recompensas. Esto es parcialmente ilustrado por ready player one: de hecho el proyecto es el oasis en esta perspectiva&#x20;
    2. Misiones: llaves y pistas estas escondida en el la son y cualquier cosa que pueda ser atada en entidades digitales también son fácilmente implementadas usando el protocolo
    3. Rompecabezas("Puzzles"): las respuestas correctas liberan piezas de colateral interno para el beneficio del jugador y/o para los que está jugando. El protocolo es entonces la primera parte de la integración de juegos en la vida diaria
12. **El mercado de la música**:
    1. De hecho - música NFT: canciones/melodías/ritmos con fechas de estreno y términos de propiedad personalizados. Con colaboraciones planeadas con proyectos como SharpShark, el proyecto puede participar en el desarrollo de derechos de autor y derechos relacionados a cualquier nivel de la industria.
    2. Automatizar el proceso de guardar y acceder a archivos mp3/wav y otro tipos así como compartir la titularidad de esos archivos.
    3. Uso de música NFT en meta universos monetizando cada componente
13. **Mercado de bienes raíces**:
    1. Desbloqueando la NFT original (titularidad) cuando cierto valor colateral subyacente sea alcanzado - un sustituto excelente para los créditos de hipoteca y de forma simultánea el génesis para un nuevo mercado para la adquisición de propiedades fuera del entorno bancario
    2. Alquileres vía llaves inteligentes, donde el acceso es mediante NFT, limitado en tiempo/número de usos así como la extensión de derechos de alquiler
14. **Mercado clásico de finanzas**:
    1. Bonos como NFTs con colateral en garantía&#x20;
    2. Seguros: NFT como contrato/póliza  digital de Seguros y cualquier otro contrato&#x20;
    3. Transacciones de portafolios/índices: inclusión de NFT en un número de activos que se mueven a través de billeteras de acuerdo a condiciones programadas, pero de una manera totalmente abierta y descentralizada  (problemas legales son un punto de discusión separado)
    4. Tarjetas de regalo digitales: con depósitos que aumentan en el tiempo como base para nuevas mecánicas para programas de lealtad&#x20;
    5. NFT cambiantes de forma dinámica, concentradas a un objetivo. Ejemplo: una foto en blanco y negro de un gato, que se vuelve a color a medida que la cantidad necesaria en el balance se acerca a la acumulación: digamos por acumular en un depósito, o un pozo de liquidez de un equipo/familia/otro grupo
    6. Acceso automático a baúles digitales vía NFT como una llave. Al mismo tiempo, debido a la reputación transaccional generada el baúl mismo puede convertirse en colateral.
15. **Mercado de lotería NFT**:
    1. Si el presupuesto de la lotería es colocado dentro de una multi colateral el siguiente algoritmo comienza a funcionar:
       1. Un crypto activo como DAI es depositado dentro del colateral NFT dentro de esta NFT hay muchas otras NFTs que participan en la lotería cuando un evento ocurre los fondos de el colateral son distribuidos a la cuenta del propietario. Al mismo tiempo los tickets son creados como NFTs, haciendo la lotería completamente transparente. Un problema importante aquí son las mecánicas para determinar números aleatorios, pero este problema va más allá de WP
    2. El presupuesto de la lotería está fuera de la garantía
       1. Un pozo promociona es creado de ETH, BNB ERC/BEP-20 (tokens de proyectos, monedas estables, tokens de liquidez) y/o otros
       2. Solo el contrato inteligente NIFTSY tiene acceso al pozo dónde en la ocurrencia de un evento (por ejemplo una fecha) selecciona un número aleatorio de NFTs y envía el contenido del pozo a las direcciones especificadas
16. **Otros** mercados.\


Hay otros jugadores y segmentos enteros que se pueden beneficiar del protocolo, pero el protocolo es una parte pequeña del proyecto, así que vamos a tratar de describirlo completamente, revelando también los aspectos principales del oráculo y el índice, viendo a los casos y el desarrollo del proyecto en relación a ellos.\
