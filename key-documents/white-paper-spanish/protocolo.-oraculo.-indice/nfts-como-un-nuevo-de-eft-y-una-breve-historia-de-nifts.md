# NFTs como un nuevo de EFT y una breve historia de NIFTS

Primero que es una EFT? Un fondo cotizado en la bolsa de valores ("EFT") es un fondo índice cuyas unidades (acciones) son intercambiadas en una bolsa. Eso significa, es casi una unidad, pero a diferencia de los fondos mutuos indexados, las acciones EFT pueden ser manejadas de la misma forma que una acción ordinaria en la bolsa.

Porque el mercado crypto necesita esto?, las respuestas son varias

* **Primero** es mucho más conveniente para los novatos tomar portafolios "de un estante" (discutidos abajo) que construir sus propios portafolios desde cero, especialmente - a menos que estemos hablando de las criptomonedas/tokens en el top 10. Solo mira la historia del mercado en 2009 solo había 1 activo a 2021 hay más de 7000, sin incluir derivados, para el tender eso un modelo así es será demandado.
* **Segundo**, para inversionistas profesionales compartir portafolios, diversificación, valuación objetiva de activos son importantes y aquí la diversidad también es confusa. Pero lo más importante no siempre permite una valuación rápida y precisa de nuevos activos. Otro problema es que hace difícil intercambiar portafolios, revelarlos, o de forma inversa mantenerse anónimo. Las transacciones OTC requieren un garantizador de colateral mientras que una EFT creado vía NFT puede ser intercambiado solamente a través del protocolo
* **Tercero**, en la evolución de los sistemas p2p es evidente que el principio de pareto funciona: 80% de la actividad es creada por el 20% de los jugadores. Al menos inicialmente. Y aquí es importante evitar la manipulación: el protocolo provee exactamente está posibilidad, y el oráculo e índice extienden la funcionalidad a un sistema completo y objetivo de activos auto-evaluados

El protocolo es la base para protocolos de siguiente orden, eso es mientras que cualquier solución blockchain en Nivel 0/Nivel 1 (L0/L1), el protocolo puede descansar en el plano L1/L2 y más allá. Y aquí está lo que NIFTSY ofrece en esta rama:

* **Primero** tokenización de canales de pago: en este caso no importa si estamos viendo a implementaciones específicas (red relámpago, plasma) o sus agregaciones  (plasma+ZK-rollups, puentes de diferentes niveles), si tomamos una sola blockchain o integración multi-chain, pero la cosa importante es que la salida desde la cadena principal puede y debería ser usada, dándole liquidez al canal mismo (entre las partes) y los activos atados a través de este (antes de cerrar el canal). En este caso la misma mecánica del protocolo Cross-chain aplica cuando el proyecto vincula la economía fuera de línea con proyectos en línea.
* **Segundo**, el protocolo no trabaja por sí mismo, pero junto con otros elementos sirve como como una herramienta de descubrimiento de precio descentralizada On-chain a través de varios mercados. Eso es, ya sea que hagas un depósito asegurado en Fiat y lo intercambias por una cantidad equivalente de tokens y/o monedas de diferente orden en la economía p2p, o intercambiar activos equivalentes atados en NFT en diferentes blockchains, las mecánicas del protocolo serán las mismas y así verificables para cada participante en la transacción.
* **Tercero**, el protocolo es un normalizador  de relaciones entre diferentes participantes en los mercados DEX, DAO (DeFi): sin importancia de que Sao (Sujeto-objeto) es el participante. Por esta razón el proyecto puede ser integrado no sólo con mercados p2p clásicos, pero también por ejemplo con soluciones IoT dónde los actores principales son dispositivos programables, scripts de evaluación de hardware o sistemas (semi) autónomos  que proveen interacción directa entre diferentes elementos IOT.
* **Cuarto**, el protocolo de hecho crea la posibilidad de agregación de de liquidez a través de la transferencia Cross-chain de la titularidad NFT: b2bx 1inch y agregadores de liquidez similares podrán ser considerados los análogos más cercanos, pero con la diferencia que ellos representan la primera generación de esta rama evolucionará de la esfera DAO & DEX.

Sin embargo, las posibilidades del protocolo no terminan ahí, vamos a tratar de describirlas brevemente pero en detalle desde una perspectiva general de desarrollo.

En un lado, la tendencia a la integración de DeFi y NFT es clara hoy porque tokens intercambiables (ERC-20, TRC-20, BIP-20, etc.) Pueden ser cambiados en diferentes niveles: atomic swaps, si estamos hablando sobre soluciones blockchain  (DCR-LTC y otras); vía protocolos inteligentes como bancor; directamente vía soluciones DEX\&DAO, la primera y más simple implementación del cual es DeFi. En el otro lado es gracias a los atadores de NFT que intercambios entre diferentes soluciones blockchain (de aquí en adelante referidas como DDS: sistemas descentralizados y/o distribuidos) son posibles sin recurrir a puentes o implementaciones incluso más complejas. Ejemplos de este aspecto -Uniswap, YFI.Finance, AAVE- están arriba.

Pero al mismo tiempo otro aspecto importante se levanta - los problemas del mercado NFT mismo. Aquí hay solo algunos de ellos:

* **Primero**, el mercado NFT era entendido de forma muy estrecha, no en el nivel teórico dónde habían formatos como ERC-721, ERC-998, ERC-1050, y muchos otros que están constantemente evolucionando, pero precisamente al nivel de aplicación, los nichos de las NFTs que comenzaron a tomar demanda entre 2014 y 2021 eran increíblemente pequeños: la industria de los videojuegos, arte digital avatarizacion  de cosas fuera de línea. Pero incluso estos nichos fueron capaces de contribuir una capitalización bastante sólida al mercado: tanto en términos de cheques promedio por NFT y parámetros máximos permisibles así como proyectos totales.
* **Segundo**, NFTs son vulnerables en muchas maneras a ataques, no a nivel de protocolos Y DDS en general, pero al nivel final de adquisición - la entidad: comenzando con en hecho de  que la identificación visible de una entidad conectada a una NFT es posible de sustituir e incluso si también existe en línea (Phishing de NFT), por no mencionar complejas implementaciones fuera de línea, a él hecho de  que es muy difícil para una persona sin conocimientos previos que está entrando en el mercado NFT determinar el precio de una de estos tokens no fungibles.
* **Tercero**, NFT también poseen otras enfermedades infantiles inherentes en cualquier proyecto de innovación en su infancia:
  * Baja capacidad de red
  * Escasez de liquidez en los mercados
  * Otras\


Como el CTO de NIFTSY de forma correcta y precisa describió "creo que las características génica del oro toco son:

1. Onchain. Todos los eventos del mundo exterior son casos donde se usa el protocolo, o un protocolo de OTRO nivel construido sobre nuestro núcleo Onchain.
2. Todo sobre NFT".\


Eso significa, todo lo que es hecho fuera del protocolo (a un nivel superior, inferior y/o varios niveles por encima) es un nuevo protocolo (L0, L2, L3), o oráculos que de alguna forma interactúan con ellos, o algún tipo de entidad tercera.

Con eso dicho hay dos tipos de oráculos:&#x20;

1. Esos que conectan la blockchain al mundo exterior: Chain Link es un ejemplo de esto.
2. Esos que analizan la blockchain y producen un cuerpo de datos en esta y esos datos ya son usados por otras soluciones blockchain, algunas descentralizadas incluyen: Chainalytics.com.

En este caso, estamos hablando sobre el primer y segundo punto a la vez, osea el tercer tipo de oráculo - sintético: por una parte tiene que analizar todos los datos pasando a través del protocolo y por otro lado conectar el protocolo al mundo exterior.

Por eso que un estudio de este mercado y sus segmentos fueron conducidos en noviembre- diciembre 2020 [estudio 1](https://hub.forklog.com/kanaly-lightning-network-raiden-i-drugie-kak-budushhee-daodex-mira/) [estudio 2,](https://hub.forklog.com/web-3-0-proekty-i-kejsy-chast-ii-nft-agregator-arhitektura-kejsy-perspektivy-problemy/) y entonces en la primera d 2021 la arquitectura principal de NIFTSY fue desarrollada, y entonces el MVP, presentado en el hackaton del mayor exchange de criptomonedas, binance, entre otros.

Es por esta razón que, para responder a la pregunta, "qué problemas soluciona el protocolo?" - fue por la cual que la primera respuesta conjunta del equipo fue que el primer y principal problema es asegurando NFTs poniendo varios activos digitales, y en el futuro cualquier activo tokenizado NO digital en un contenedor/colateral o disco colateral. Esto puede ser Wrapped Bitcoin (wBTC y otros), tokens ERC-20 y/o BIP-20 criptomonedas de varios tipos, etc. El protocolo es construido de forma inicial en la blockchain de Ethereum  (incluyendo vía la capa L2 - por ejemplo polygon) y BSC, pero en el futuro (vea el mapa de ruta ("Roadmap") está planeado crear implementaciones en Flow, WAX, Solana, Polkadot, Cosmos, Avalanche y otros DRS, porque estamos profundamente convencidos de cross chain es el futuro de todos los sistemas descentralizados y distribuidos. Exactamente lo mismo aplica para soluciones de segundo nivel y subsecuentes niveles.

Vamos Vamos a resumir conclusiones sobre el protocolo:

1. Permite la unificación de WUM;
2. Tiene colaterales simple o Multi-colaterales;
3. Contiene una parte de almacenamiento estática (no refinable) y una parte de almacenamiento dinámica;
4. Para el usuario promedio - funciona como una evaluación de nuevo cero de una NFT de cualquier orden (así como cualquier derivado);
5. Para jugadores b2b - provee un mecanismo para lidiar con liquidez atada en NFT de cualquier orden por un lado, por el otro provee un mecanismo claro para la creación creación de una NFT (es un proveedor b2b de NFT);
6. Para fondos (pensiones, seguros, inversiones, coberturas, etc.) Actúa como una herramienta objetiva de valuación de activos dónde cualquier cliente del fondo recibe NFT sin atar en un evento/fecha y simple sabe exactamente el nivel primario de colateral de esa NFT.

Pero el protocolo no podía y no debía solucionar todos los problemas del mercado NFT y sus vínculos con DeFi y otras industrias. Así es como el oráculo vino a la vida.
