import random

# Función para generar una palabra de 4 letras al azar
def generar_palabra():
    palabra = ""
    for _ in range(4):
        # Letras de la 'a' a la 'z' son del 97 al 122 en ASCII
        letra = chr(random.randint(97, 122))
        palabra += letra
    return palabra

# Función para crear la matriz cuadrada de palabras
def crear_matriz(n):
    matriz = []
    for _ in range(n):
        fila = []
        for _ in range(n):
            fila.append(generar_palabra())
        matriz.append(fila)
    return matriz

# Función para mostrar la matriz en forma cuadrada
def mostrar_matriz(matriz):
    for fila in matriz:
        print(" ".join(fila))

# Función para verificar si una palabra tiene al menos una vocal
def tiene_vocal(palabra):
    vocales = "aeiou"
    for letra in palabra:
        if letra in vocales:
            return True
    return False

# Función divide y vencerás para contar palabras con vocal en una submatriz
def contar_vocales(matriz):
    # Caso base: si la matriz es 1x1, solo una palabra
    if len(matriz) == 1 and len(matriz[0]) == 1:
        return 1 if tiene_vocal(matriz[0][0]) else 0
    
    # Dividir la matriz en 4 submatrices
    n = len(matriz)
    mitad = n // 2
    
    # Submatrices
    submatriz1 = [fila[:mitad] for fila in matriz[:mitad]]
    submatriz2 = [fila[mitad:] for fila in matriz[:mitad]]
    submatriz3 = [fila[:mitad] for fila in matriz[mitad:]]
    submatriz4 = [fila[mitad:] for fila in matriz[mitad:]]
    
    # Contar recursivamente en cada submatriz
    return (contar_vocales(submatriz1) + contar_vocales(submatriz2) +
            contar_vocales(submatriz3) + contar_vocales(submatriz4))

# Programa principal
def main():
    n = int(input("Ingrese el tamaño de la matriz cuadrada: "))
    matriz = crear_matriz(n)
    
    print("\nMatriz generada:")
    mostrar_matriz(matriz)
    
    total_con_vocal = contar_vocales(matriz)
    print(f"\nCantidad de palabras que tienen al menos una vocal: {total_con_vocal}")

# Ejecutar el programa
main()
