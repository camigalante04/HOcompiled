1) Pre-procesador:

Se encarga de las directivas # (como los include y las macros). En este caso, tenemos un 'calculator.h'. En este paso, se agregara al 'calculator.c' la referencia a 'calculator.h', ya que en la primera linea de 'calculator.c' aparece un #include "calculator.h". El archivo de salida de este paso es un .pp.c, que contiene muchisimas mas filas que el codigo original, donde aparecen un monton de referencias a funciones externas que se necesitan para hacer funcionar al programa, incluido el calculator.h.

2)  Compilacion I:

Tiene 3 partes:
-El Front End, que consiste en un analisis sintactico, semantico y lexico (este paso genera una IR)
-El Middle End, que toma la IR del front end y la optimiza
-El Back End, que genera el codigo en assembler y optimiza (en cuanto a hardware)

Este segundo paso se hace todo de una vez, y la salida es un archivo en assembler (.asm), que todavia se puede abrir, ver y editar, pero es bastante dificil de entender. Lo que podemos identificar son las dos funciones del programa, donde podemos observar los registros y las instrucciones, y en main vemos el call a la funcion add_numbers, printf. En la funcion add_numbers, podemos ver que en una oportunidad suma los dos numeros con 'addl'

3)  Compilacion II:

Pasa de assembler a maquina, genera un archivo objeto (.o) en binario. Este archivo ya no se puede abrir, pero con nm se pueden averiguar algunas cosas. La salida de nm reconoce algunas funciones con la letra "T" y otras con la letra "U". La primera se refiere a que la funcion esta bien definida, y la segunda se refiere a que esta "indefinida", reconoce que es una funcion pero no tiene la referencia necesaria para saber en que consiste. Esto se resuelve en el proximo paso.


4) Linkeo:

Pasa de lenguaje de maquina a ejecutable. En este paso se resuelven las referencias que necesitan las funciones externas, que se necesitan para que el programa funcione. Basicamente, le decimos al programa "a donde tiene que ir a buscar" las funciones externas. (las que en el .o aparecian con la letra "U").

Si ahora corremos nm al archivo ejecutable (.e), aparecen muchos mas simbolos, pero notamos que los que antes aparecian "indefinidos" en el .o, ahora tienen el "link" correspondiente.(@@GLIBC_2.2.5)