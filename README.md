# An-lisisAlgoritmos
import pandas as pd

# Paso 1: Leer el archivo CSV usando pandas
data = pd.read_csv('fragmentos.csv')

# Paso 2: Convertir los datos a una lista de fragmentos
fragmentos = data['Fragmento'].tolist()

# Función para reconstruir la secuencia objetivo
def reconstruir_secuencia(fragmentos):
    # Si no hay fragmentos, devuelve una cadena vacía
    if not fragmentos:
        return ''
    
    # Determina la longitud de cada fragmento
    longitud_fragmento = len(fragmentos[0])
    
    # Determina la cantidad de fragmentos
    cantidad_fragmentos = len(fragmentos)
    
    # Determina el tamaño de solapamiento entre fragmentos
    solapamiento = longitud_fragmento // 2
    
    # Reconstruye la secuencia objetivo utilizando el enfoque de divide y vencerás
    mitad = cantidad_fragmentos // 2
    secuencia_izquierda = reconstruir_secuencia(fragmentos[:mitad])
    secuencia_derecha = reconstruir_secuencia(fragmentos[mitad:])
    
    # Combina las dos secuencias con el solapamiento
    for i in range(solapamiento, longitud_fragmento):
        if secuencia_izquierda[-i:] == secuencia_derecha[:i]:
            return secuencia_izquierda + secuencia_derecha[i:]
    
    # Si no hay solapamiento, concatena las secuencias
    return secuencia_izquierda + secuencia_derecha

# Paso 3: Reconstruir la secuencia objetivo
secuencia_objetivo = reconstruir_secuencia(fragmentos)
print("Secuencia Objetivo:", secuencia_objetivo)