# Control teclado matricial con raspberry pi pico

# Tabla de contenidos
1. [Materiales](#Materiales)
2. [Descripción](#Descripción)
3. [Código](#Código)

## Materiales
- Raspberry pi pico
- Teclado matricial 4x4
- Protoboard
- Jumpers 

## Descripción
Un teclado matricial 4×4 es un dispositivo que agrupa varios pulsadores y permite controlarlos empleando un número de conductores inferior al que necesitaríamos al usarlos de forma individual.
Este teclado matricial 4×4 se encuentra formado por la matriz de pulsadores que se encuentran dispuestos en filas (L1, L2, L3 y L4), y las columnas (C1, C2, C3 y C4)

![keypad](https://github.com/victorgjacobo/teclado_matricial_raspberry_pi_pico/assets/141197135/f6a75a32-f9d7-4cca-8638-01b1c0a34ab5)



En la figura observamos la conexión de la raspberry pi pico con el teclado matricial.  Los digitos están conectados de la siguiente manera: `1 -> GPIO 2`, `2 -> GPIO 3`, `3 -> GPIO 4`, `4 -> GPIO 5`, `5 -> GPIO 6`, `6 -> GPIO 7`, `7 -> GPIO 8`, `8 -> GPIO 9`.

![tercera_practica](https://github.com/victorgjacobo/teclado_matricial_raspberry_pi_pico/assets/141197135/213aae2d-50cb-4ab4-8390-35e1b98f4197)

## Código
```python
"""
  Nombre de la práctica: Control teclado matricial 4x4 con raspberry pi pico
  Autor: Ing. Víctor González Jacobo
"""
from machine import Pin
import utime

matrix_keys = [['1', '2', '3', 'A'],
               ['4', '5', '6', 'B'],
               ['7', '8', '9', 'C'],
               ['*', '0', '#', 'D']]

keypad_rows = [2,3,4,5]
keypad_columns = [6,7,8,9]

col_pins = []
row_pins = []

def asignacion():   
    for dato in range(len(keypad_rows)):
        row_pins.append(Pin(keypad_rows[dato], Pin.OUT))
        col_pins.append(Pin(keypad_columns[dato], Pin.IN, Pin.PULL_DOWN))

def main():
    asignacion()
    while True:
        for row in range(len(row_pins)):
            for col in range(len(col_pins)):
                row_pins[row].on()
                
                if col_pins[col].value() == 1:
                    print("Presionaste", matrix_keys[row][col])
                    utime.sleep(0.5)
                        
            row_pins[row].off()

if __name__ == '__main__':
    print("Ingrese el valor del teclado")
    main()
```
![](https://img.shields.io/github/followers/victorgjacobo)
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Raspberry Pi](https://img.shields.io/badge/-RaspberryPi-C51A4A?style=for-the-badge&logo=Raspberry-Pi)
![](https://img.shields.io/github/watchers/victorgjacobo/teclado_matricial_raspberry_pi_pico)
