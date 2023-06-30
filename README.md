def mostrar_menu():
  print()
  print("menu")
  print("1 comprar entradas")
  print("2 mostrar ubicacion disponibles")
  print("3 ver listado de asistentes")
  print("4 mostrar ganancias totales")
  print("5 salir")

def mostrar_ubicaciones_disponibles():
  print("VIP: ", end="")
  for repeticion in range(len(entradas_vip)):
    if(entradas_vip[repeticion]==""):
      print(repeticion+20, end=" ")
    else:
      print("X",end=" ")

  print()

  print("normales: ", end="")
  for repeticion in range(len(entradas_normales)):
    if(entradas_normales[repeticion]==""):
      print(repeticion+30, end=" ")
    else:
      print("X",end=" ")

    print()

  print("Económico: ", end="")
  for repeticion in range(len(entradas_economicas)):
    if(entradas_economicas[repeticion]==""):
      print(repeticion+50, end=" ")
    else:
      print("X",end=" ")

def comprar_entradas():
  global ganancias_totales
  cantidad = int(input("Ingrese la cantidad de entradas a comprar (1 o 2)"))
  if(cantidad <= 1 or cantidad >= 2):
    print("Error en la cantidad, debe ser 1 o 2")
    return
 
  print(cantidad)
  for repeticion in range(cantidad):
    print("Ubicaciones disponibles:")
    mostrar_ubicaciones_disponibles()
    ubicacion_valida = False
    while not ubicacion_valida:
      ubicacion = int(input("Seleccione una ubicacion: "))
      if ubicacion >= 1 and ubicacion <= 50:
        if ubicacion <= 20 and entradas_vip[ubicacion-1] == "":
          entradas_vip[ubicacion-1] = ingresar_rut()
          ubicacion_valida = True
          ganancias_totales = ganancias_totales + 100000
          asistentes.append(entradas_vip[ubicacion -20])
        
        elif ubicacion <= 30 and entradas_normales[ubicacion-21] == "":
          entradas_normales[ubicacion-11] = ingresar_rut()
          ubicacion_valida = True
          ganancias_totales = ganancias_totales + 50000
          asistentes.append(entradas_normales[ubicacion -30])

        elif ubicacion <= 50 and entradas_economicas[ubicacion-31] == "":
          entradas_economicas[ubicacion-31] = ingresar_rut()
          ubicacion_valida = True
          ganancias_totales = ganancias_totales + 10000
          asistentes.append(entradas_economicas[ubicacion -50])

        if not ubicacion_valida:
          print("Ubicacion no disponible, favor seleccione otra")
    print("Operación realizada exitosamente")


def ingresar_rut():
  run_valido = False
  while not run_valido:
    run = input("Ingrese el RUN sin Digito Verificador ni guiones:")
    if(len(run) == 7 or len(run) == 8):
      run_valido = True

  return run

def mostrar_asistentes():
  print("Listado de asistentes")
  for asistente in asistentes: 
    print(asistente)
def mostrar_ganancias():
  print (ganancias_totales)

def inicio():
  try:
    while True:

      mostrar_menu()
      opcion = int(input("Ingrese opcion: "))
      if opcion == 1:
        comprar_entradas()
      elif opcion == 2:
        mostrar_ubicaciones_disponibles()
      elif opcion == 3:
        mostrar_asistentes()
      elif opcion == 4:
        mostrar_ganancias()
      elif opcion == 5:
        print("Gracias por usar el Sofware")
        break
  except:
    print("Ha ocurrido un error")



inicio()
