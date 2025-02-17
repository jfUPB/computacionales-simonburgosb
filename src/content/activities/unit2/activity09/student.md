# Codigo traducido a alto nivel

``` c#
using System;

class HackSim
{
    const int SCREEN_START = 16384;
    const int SCREEN_SIZE = 8192; // 512 * 256 / 16
    const int KBD = 24576;

    public int[] SCREEN = new int[SCREEN_SIZE];
    public int KBD_Value = 0; // Simulación del teclado

    static void Main()
    {
        int R16 = SCREEN_START;

        while (true)
        {
            int keyboardInput = KBD_Value; // Leer el teclado

            if (keyboardInput > 19)
            {
                R16++;
            }

            if (R16 == keyboardInput)
            {
                SCREEN[R16 - SCREEN_START] = -1; // Escribir en la pantalla
                console.writeLine(SCREEN[]);
                R16--;
            }
        }
    }
}
```
