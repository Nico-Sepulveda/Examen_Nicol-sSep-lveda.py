productos = {
    "8475HD": ['HP', 15.6, '8GB', 'DD', '1T', 'Intel Core i5', 'Nvidia GTX1050'],
    "2175HD": ['lenovo', 14, '4GB', 'SSD', '512GB', 'Intel Core i5', 'Nvidia GTX1050'],
    "JjfFHD": ['Asus', 14, '16GB', 'SSD', '256GB', 'Intel Core i7', 'Nvidia RTX2080Ti'],
    "fgdxFHD": ['HP', 15.6, '8GB', 'DD', '1T', 'Intel Core i3', 'integrada'],
    "GF75HD": ['Asus', 15.6, '8GB', 'DD', '1T', 'Intel Core i7', 'Nvidia GTX1050'],
    "123FHD": ['lenovo', 14, '6GB', 'DD', '1T', 'AMD Ryzen 5', 'integrada'],
    "342FHD": ['lenovo', 15.6, '8GB', 'DD', '1T', 'AMD Ryzen 7', 'Nvidia GTX1050'],
    "UWU131HD": ['Dell', 15.6, '8GB', 'DD', '1T', 'AMD Ryzen 3', 'Nvidia GTX1050']
}

stock = {
    "8475HD": [387990, 10],
    "2175HD": [327990, 4],
    "JjfFHD": [424990, 1],
    "fgdxFHD": [664990, 21],
    "123FHD": [298090, 32],
    "342FHD": [449990, 7],
    "GF75HD": [749990, 2],
    "UWU131HD": [349990, 1],
    "FS1230HD": [249990, 0]
}

def stock_marca(marca):
    total_stock = 0
    for modelo, datos in productos.items():
        if datos[0].lower() == marca.lower() and modelo in stock:
            total_stock += stock[modelo][1]
    print(f"El stock es: {total_stock}")

def busqueda_precio(p_min, p_max):
    if not (isinstance(p_min, int) and isinstance(p_max, int)):
        print("Debe ingresar valores enteros!!")
        return
    resultados = []
    for modelo, datos in stock.items():
        precio = datos[0]
        if p_min <= precio <= p_max and datos[1] > 0:
            if modelo in productos:
                marca = productos[modelo][0]
                resultados.append(f"{marca}--{modelo}")
    if resultados:
        print("Los notebooks entre los precios consultas son:", resultados)
    else:
        print("No hay notebooks en ese rango de precios.")

def actualizar_precio(modelo, nuevo_precio):
    if modelo in stock:
        stock[modelo][0] = nuevo_precio
        return True
    else:
        return False

def menu():
    while True:
        print("\n*** MENU PRINCIPAL ***")
        print("1. Stock marca.")
        print("2. Búsqueda por precio.")
        print("3. Actualizar precio.")
        print("4. Salir.")
        
        opcion = input("Ingrese opción: ")
        
        if opcion == "1":
            marca = input("Ingrese marca a consultar: ")
            stock_marca(marca)
        
        elif opcion == "2":
            try:
                p_min = int(input("Ingrese precio mínimo: "))
                p_max = int(input("Ingrese precio máximo: "))
                busqueda_precio(p_min, p_max)
            except ValueError:
                print("Debe ingresar valores enteros!!")
        
        elif opcion == "3":
            while True:
                modelo = input("Ingrese modelo a actualizar: ").strip()
                if modelo in stock:
                    try:
                        nuevo_precio = int(input("Ingrese precio nuevo: "))
                        if actualizar_precio(modelo, nuevo_precio):
                            print("Precio actualizado!!")
                        else:
                            print("Error al actualizar el precio.")
                    except ValueError:
                        print("Debe ingresar un precio válido.")
                else:
                    print("El modelo no existe!!")

                continuar = input("Desea actualizar otro precio (s/n)?: ").lower()
                if continuar != 's':
                    break
        
        elif opcion == "4":
            print("Programa finalizado.")
            break
        
        else:
            print("Debe seleccionar una opción válida!!")

menu()
