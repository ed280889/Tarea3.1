"""
Este programa permite gestionar clientes y sus servicios contratados.
"""

# Importación de bibliotecas necesarias
import os                 # Para operaciones con archivos y directorios
import datetime           # Para obtener la fecha actual
import sys                # Para acceder a los argumentos de línea de comandos

# Función para crear la carpeta de clientes si no existe
def inicializar_directorio():
    """Crea el directorio 'clientes' si no existe."""
    if not os.path.exists('clientes'):
        os.makedirs('clientes')
    return True

# Función para mostrar el menú principal
def mostrar_menu():
    """Muestra el menú principal y devuelve la opción elegida."""
    print("\n=== GESTOR DE CLIENTES SKY ===")
    print("1. Ver lista de clientes")
    print("2. Ver cliente")
    print("3. Crear cliente nuevo")
    print("4. Agregar servicio")
    print("5. Salir")
    print("=============================")
    return input("Elija una opción: ")

# Función para ver la lista de clientes
def ver_lista():
    """Muestra la lista de todos los clientes existentes."""
    print("\nCLIENTES:")
    archivos = os.listdir('clientes')
    if len(archivos) == 0:
        print("No hay clientes")
    else:
        for archivo in archivos:
            # Muestra el nombre sin la extensión .txt
            nombre = archivo.replace('.txt', '')
            print(f"- {nombre}")
    return True

# Función para ver información de un cliente específico
def ver_cliente(nombre=None):
    """
    Muestra la información de un cliente específico.
    
    Args:
        nombre (str, opcional): Nombre del cliente a consultar.
                               Si es None, lo solicitará al usuario.
    
    Returns:
        bool: True si el cliente existe, False si no existe.
    """
    # Si no se proporcionó un nombre, solicitarlo
    if nombre is None:
        nombre = input("\nNombre del cliente: ")
    
    # Construir la ruta al archivo del cliente
    ruta = f"clientes/{nombre}.txt"

    # Verificar si el cliente existe
    if os.path.exists(ruta):
        # Leer y mostrar la información del cliente
        with open(ruta, 'r') as archivo:
            contenido = archivo.read()
        print("\nINFORMACIÓN DEL CLIENTE:")
        print(contenido)
        return True
    else:
        print(f"Cliente '{nombre}' no existe")
        return False

# Función para crear un nuevo cliente
def crear_cliente(nombre=None, direccion=None, telefono=None, servicio=None):
    """
    Crea un nuevo cliente con su información básica.
    
    Args:
        nombre (str, opcional): Nombre del cliente.
        direccion (str, opcional): Dirección del cliente.
        telefono (str, opcional): Teléfono del cliente.
        servicio (str, opcional): Primer servicio contratado.
        
    Returns:
        bool: True si se creó correctamente, False si ya existía.
    """
    # Si no se proporcionó un nombre, solicitarlo
    if nombre is None:
        nombre = input("\nNombre del cliente nuevo: ")
    
    # Construir la ruta al archivo del cliente
    ruta = f"clientes/{nombre}.txt"

    # Verificar si el cliente ya existe
    if os.path.exists(ruta):
        print(f"Este cliente '{nombre}' ya existe")
        return False

    # Solicitar información faltante si no se proporcionó
    if direccion is None:
        direccion = input("Dirección: ")
    
    if telefono is None:
        telefono = input("Teléfono: ")
    
    if servicio is None:
        servicio = input("Servicio: ")
    
    # Obtener la fecha actual
    fecha = datetime.datetime.now().strftime("%Y-%m-%d")

    # Crear el archivo del cliente y escribir su información
    with open(ruta, 'w') as archivo:
        archivo.write(f"Nombre: {nombre}\n")
        archivo.write(f"Dirección: {direccion}\n")
        archivo.write(f"Teléfono: {telefono}\n")
        archivo.write(f"Fecha registro: {fecha}\n\n")
        archivo.write(f"SERVICIOS:\n")
        archivo.write(f"- {servicio} ({fecha})\n")

    print(f"Cliente '{nombre}' creado correctamente")
    return True

# Función para agregar un servicio a un cliente existente
def agregar_servicio(nombre=None, servicio=None):
    """
    Agrega un nuevo servicio a un cliente existente.
    
    Args:
        nombre (str, opcional): Nombre del cliente.
        servicio (str, opcional): Servicio a agregar.
        
    Returns:
        bool: True si se agregó correctamente, False si el cliente no existe.
    """
    # Si no se proporcionó un nombre, solicitarlo
    if nombre is None:
        nombre = input("\nNombre del cliente: ")
    
    # Construir la ruta al archivo del cliente
    ruta = f"clientes/{nombre}.txt"

    # Verificar si el cliente existe
    if os.path.exists(ruta):
        # Solicitar el servicio si no se proporcionó
        if servicio is None:
            servicio = input("Nuevo servicio: ")
        
        # Obtener la fecha actual
        fecha = datetime.datetime.now().strftime("%Y-%m-%d")

        # Añadir el servicio al archivo del cliente
        with open(ruta, 'a') as archivo:
            archivo.write(f"- {servicio} ({fecha})\n")

        print(f"Servicio '{servicio}' agregado correctamente a '{nombre}'")
        return True
    else:
        print(f"Cliente '{nombre}' no existe")
        return False

# Función principal
def main():
    """
    Función principal que maneja tanto el modo interactivo como el modo de línea de comandos.
    """
    # Crear el directorio de clientes si no existe
    inicializar_directorio()
    
    # Verificar si hay argumentos de línea de comandos
    if len(sys.argv) > 1:
        # Obtener el comando (primer argumento)
        comando = sys.argv[1]
        
        # Ejecutar el comando correspondiente
        if comando == "listar":
            # Listar todos los clientes
            return ver_lista()
        
        elif comando == "ver" and len(sys.argv) > 2:
            # Ver información de un cliente específico
            return ver_cliente(sys.argv[2])
        
        elif comando == "crear" and len(sys.argv) > 5:
            # Crear un nuevo cliente con la información proporcionada
            return crear_cliente(sys.argv[2], sys.argv[3], sys.argv[4], sys.argv[5])
        
        elif comando == "agregar" and len(sys.argv) > 3:
            # Agregar un servicio a un cliente existente
            return agregar_servicio(sys.argv[2], sys.argv[3])
        
        else:
            # Mostrar instrucciones si el comando no es válido o faltan argumentos
            print("Uso del programa en línea de comandos:")
            print("  python gestor_clientes.py listar")
            print("  python gestor_clientes.py ver <nombre>")
            print("  python gestor_clientes.py crear <nombre> <direccion> <telefono> <servicio>")
            print("  python gestor_clientes.py agregar <nombre> <servicio>")
            return False
    
    # Modo interactivo (sin argumentos de línea de comandos)
    else:
        # Bucle principal del modo interactivo
        while True:
            # Mostrar menú y obtener opción
            opcion = mostrar_menu()

            # Procesar la opción elegida
            if opcion == "1":
                ver_lista()
            elif opcion == "2":
                ver_cliente()
            elif opcion == "3":
                crear_cliente()
            elif opcion == "4":
                agregar_servicio()
            elif opcion == "5":
                print("Adiós")
                break
            else:
                print("Opción no válida")
        
        return True

# Punto de entrada del programa
if __name__ == "__main__":
    # Llamar a la función principal
    main()
