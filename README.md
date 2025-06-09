[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=19669236&assignment_repo_type=AssignmentRepo)
# Lab02 - Parte 1: Sumador de 1 bit y sumador de 4 bits.

## Integrantes 


[Gabriel Santiago Rodriguez Torres](https://github.com/santiago85319)

[Luis Allberto Mendoza Rojas](https://github.com/lmendozar2001)

[cristian stiven hoyos peralta](https://github.com/hoyoscristian)

### Semi sumador de 1 bit.
Hicimos un semi sumador de 1 bit no por el hecho de la practica de laboratorio, sino por el repaso de la clase magistral, ya que sabemos que instanciando 2 semisumadores de 1 bit podemos hacer un sumador de 1 bit,  este sumador solo lo hicimos en Digital.

Imagen del semi sumador.
![Imagen del semisumador de 1 bit](imagenes/semisumador.png)

[arvhivo .dig del semi sumador](src/semisumador_1bit.dig)


### sumador de 1 bit 
Para hacer el sumador de 1 bit utilizamos la tabla de verdad para luego proceder a hacer mapas de Karnaugh y encontrar sus respectivas ecuaciones.

Tabla de verdad para el sumador de 1 bit.
| A | B | Ci | So | Co |
|---|---|----|----|----|
| 0 | 0 | 0  | 0  | 0  |
| 0 | 0 | 1  | 1  | 0  |
| 0 | 1 | 0  | 1  | 0  |
| 0 | 1 | 1  | 0  | 1  |
| 1 | 0 | 0  | 1  | 0  |
| 1 | 0 | 1  | 0  | 1  |
| 1 | 1 | 0  | 0  | 1  |
| 1 | 1 | 1  | 1  | 1  |

Mapa de Karnaugh
![Imagen del semisumador de 1 bit](imagenes/Karnaugh.png)

Con estas ecuaciones procedemos a hacer nuestro circuito en digital y programarlo en verilog, en digital instanciamos el semisumador 2 veces.

Imagen del sumador de 1 bit.
![Imagen del sumador de 1 bit](imagenes/sumador1bit.png)

[arvhivo .dig del sumador de 1 bit](src/sumador_1bit.dig)

[arvhivo .v del sumador de 1 bit](src/sum1bit.v)

para verificar su funcionamiento hicimos un tb del sumador y esta fue el resultado de ello.

Simulacion del sumador de 1 bit.
![Simulacion del sumador de 1 bit](imagenes/1bit_sim.png)
[arvhivo .v del tb del sumador de 1 bit](src/sum1bit_tb.v)


### Sumador de 4 Bits.
Al realizar el sumador de 4 bits omitimos mapas de Karnaugh porque se hace tedioso, por ende prefirimos la practicidad de instanciar modulos, asi como con el de 1 bit instanciamos el de un semisumador, aca aplicamos lo mismo.

Imagen del sumador de 4 bits.
![Imagen del sumador de 4 bits](imagenes/sumador4bits.png)
[arvhivo .dig del sumador de 4 bits](src/sumador_4bits.dig)

[arvhivo .v del sumador de 1 bit](src/sum1bit.v)

Como todo necesitamos comprobarlo le hicimos su respectivo tb y su simulacion.

Simulacion del sumador de 4 bits.
![Simulacion del sumador de 4 bits](imagenes/4bit_sim.png)
[arvhivo .v del tb del sumador de 4 bits](src/sum4bit_tb.v)

Durante la practtiva de laboratorio mostramos y sustentamos la implementacion de la fpga con los respectivos sumadores.

# Lab02 - Parte 2: Sumador/restador de 4 bits.
Reutiliza el mismo circuito para sumar solo que le agregamos una compuerta  XOR  a la entrada B unida con el bit de signo o seleccion, el funcionamiento de la la compuerta XOR es para aplicar complemento a2 si la entrada seleccion esta activa

con esto sumamos y restamos numeros de 4 bits, algo a tener encuenta en el momento de hacer estas operaciones es que nos dan numeros en complento a2, voy dar los ejemplos de nuestar simulacion:   A=3, B=2, S= 5, CO=0, este pasa directo ya que es una suma normal,  A=7, B=-2, S= 5, CO=1 , aca hay acarreo de salida, pero no afecta,   A=5, B=5, S= A, CO=0, en este nos da A que rrepresenta 10, ya que estamos en 4 bits, S puede abarcar hasta F que es 15, esto estara normal para cuando estemos sumandodumeros positivo. la diferencia comienza es con sus numeros negativo o restas, A=4, B=-6, S= E, CO=0, aca deberia ser 2 o bueno -2 pero lo estamos viendo en su complemento a2 que es 14,  A=15, B=-15, S= 0, CO=1 , aca hay deborde y en S vemos cero y asi 


Imagen del sumador/restador de 4 bits.
![Imagen del sumador/restador de 4 bits](imagenes/sumadorrestador4bits.png)

[arvhivo .dig del sumador/restador de 4 bits](src/sumador_restador.dig)

[arvhivo .v del sumador/restador de 4 bits](src/sumador_restador4bits.v)

Simulacion del sumador/restador de 4 bits.
![Simulacion del sumador/restador de 4 bits](imagenes/sumres4bit_sim.png)
[arvhivo .v del tb del sumador/restador de 4 bits](src/sumador_restador4bits_tb.v)

## Preguntas

1. Describa el enfoque estructural y comportamental en el contexto de electrónica digital y cómo los implementó. ¿Qué hace Quartus con cada uno?

En este laboratorio usamos el enfoque estructural, que consiste en construir un módulo grande a partir de módulos más pequeños conectados entre sí. Es como armar un circuito usando bloques o piezas individuales.

Por ejemplo, nosotros hicimos un sumador de 4 bits (sum4b) conectando cuatro módulos sum1b, que cada uno suma 1 bit. Es decir, armamos el circuito completo conectando las salidas y entradas de cada sumador con los acarreos intermedios (C1, C2, C3).

El enfoque comportamental se usa cuando se quiere describir cómo se comporta un circuito sin armarlo con bloques pequeños, pero eso todavía no lo usamos.

Quartus, al compilar, toma ese diseño estructural y lo traduce a compuertas lógicas como AND, OR, XOR, etc., y las acomoda dentro de la FPGA para que funcione físicamente como lo escribimos en el código.


2. ¿Cómo afecta el diseño del sumador y de comparadores al uso de recursos en la FPGA (LUTs, FFs, BRAMs, etc.)? Muestren el uso de recursos de su diseño.

Nuestro diseño es completamente combinacional, lo que significa que solo usamos compuertas lógicas, sin memoria ni almacenamiento. Entonces, lo que más se usa en la FPGA son las LUTs, que sirven para implementar funciones lógicas.

Como conectamos 4 módulos sum1b, y cada uno hace operaciones lógicas básicas (XOR, AND, OR), el uso de recursos fue bajo.

Por ejemplo, según el informe de Quartus (puede variar según el diseño), se usaron:

LUTs (Look-Up Tables): 16

Flip-Flops: 0 (porque no usamos nada que guarde valores)

BRAMs: 0

Pines: 9 (4 de A, 4 de B, 1 de acarreo de entrada)

Esto muestra que el diseño está bien optimizado, ya que todo se basa en lógica combinacional y no requiere componentes complejos.

3. Describa las diferencias entre los tipos de dato ```wire``` y  ```reg``` en Verilog y compare ambos con el tipo de dato ```logic``` en System Verilog.

Hasta ahora solo hemos usado wire, que es el tipo que se usa para conectar señales entre módulos. Por ejemplo, usamos wire para los acarreos intermedios (C1, C2, C3) entre los sumadores.

El tipo reg todavía no lo usamos porque está más relacionado con cosas que guardan valores (como memoria o registros), y eso lo veremos más adelante.

En resumen:

wire: se usa para conectar señales entre módulos y para señales que salen de compuertas.

reg: se usa más adelante cuando trabajemos con cosas que guarden valores (aún no visto).

En SystemVerilog (que todavía no usamos), hay un tipo llamado logic, que junta lo que hacen wire y reg, pero por ahora solo trabajamos con Verilog básico.

4. Únicamente con lo que se vio en clase, describa cómo se usó el bloque ```always```. Enfoque su respuesta hacia la implementación de lógica combinacional.

Hasta el momento, no usamos bloques always, ya que todo lo hicimos de forma estructural, es decir, conectando módulos como sum1b para hacer uno más grande.

En lugar de usar always, armamos la lógica combinacional usando conexiones directas entre señales (wire) y creando instancias de los módulos, como se ve en el código del sum4b.

Por eso, por ahora no usamos always, y todo se basa en compuertas lógicas combinadas usando el enfoque estructural.



## Conclusiones
En esta práctica, nosotros tres (Gabriel, Luis y Cristian) aprendimos a diseñar sumadores usando Verilog y a implementar circuitos digitales en la FPGA con un enfoque estructural. Nos dimos cuenta que es muy útil construir módulos pequeños, como un sumador de 1 bit, y luego conectarlos para crear módulos más grandes, como el sumador de 4 bits. Esto facilita el diseño y la organización del código.

Además, entendimos que el uso de recursos en la FPGA depende mucho del diseño que hagamos. Al trabajar con sumadores combinacionales sin memoria, el consumo de recursos como LUTs fue bajo y eficiente.

Aunque todavía no usamos bloques always ni elementos secuenciales, pudimos ver cómo se puede implementar lógica combinacional usando solo módulos conectados y señales tipo wire.

En general, esta práctica nos ayudó a reforzar los conceptos básicos de electrónica digital y Verilog, y nos preparó para avanzar hacia proyectos más complejos en FPGA.