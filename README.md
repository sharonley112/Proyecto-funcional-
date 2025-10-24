# Proyecto-funcional-
#========== GESTOR_DE_CURSOS_Y_NOTAS ==========

# Se crea una lista para almacenar las notas ingresadas 

cursos = ["Algoritmos", "Álgebra Lineal", "Precálculo", "Contabilidad", "Matemática Discreta"]
notas = [62, 80, 65, 90, 97]

# Estructuras 
cola_revisiones = [] # COLA (FIFO)
historial_cambios = [] # FILAS (LIFO)

#==================== MENÚ ====================

def mostrar_menu():
    print("""
========= MENÚ =========
1. Registrar nuevo curso
2. Mostrar todos los cursos y notas
3. Calcular promedio general
4. Contar cursos aprobados y reprobados
5. Buscar curso por nombre (búsqueda lineal)
6. Actualizar nota de un curso
7. Eliminar curso
8. Ordenar cursos por nota (ordenamiento burbuja)
9. Ordenar cursos por nombre (ordenamiento burbuja)
10. Buscar curso por nombre (búsqueda binaria)
11. Simular cola de solicitudes de revisión
12. Mostrar historial de cambios (pila)
13. Salir
========================
""")
    
#========== FUNCIONES ==========
# 1. Registrar nuevo curso
def registrar_curso():
    """Permite al usuario agregar un nuevo curso con su nota"""
    nombre = input("Ingrese el nombre del curso: ").strip()

  #Verifica que el curso no esté duplicado
    if nombre in cursos:
        print("Ese curso ya está registrado.")
        return

  # Pide la nota y valida que esté entre 0 y 100
  try:
        nota = float(input("Ingrese la nota (0 a 100): "))
        if 0 <= nota <= 100:
            cursos.append(nombre)
            notas.append(nota)
            print("Curso registrado correctamente.")
        else:
            print("La nota debe estar entre 0 y 100.")
    except ValueError:
        print(" Ingrese una nota válida.")

# 2. Mostrar todos los cursos y notas
def mostrar_cursos():
    if not cursos:
        print("No hay cursos registrados aún")
        return
    print("\n=== Cursos y notas actuales ===")
    for i in range(len(cursos)):
        print(f"{i + 1}. {cursos[i]} → {notas[i]}")
    print("===============================")

# 3. Calcular Promedio General 
def promedio():
    if not cursos:
        print("No hay cursos registrados")
        return
    prom = sum(notas) / len(notas)
    print(f"\n El promedio general es: {prom:.2f}")
    
# 4. Contar cursos aprobados y reprobados
def contar_aprobados_reprobados():
    aprobados = 0
    reprobados = 0
    for nota in notas:
        if nota >= 61:
            aprobados += 1
        else:
            reprobados += 1
    print(f"\n Aprobados: {aprobados}")
    print(f"Reprobados: {reprobados}")
    
# 5. Buscar curso por nombre (búsqueda lineal)

def busqueda_curso_lineal():
    nombre = input("Ingrese el nombre del cursos a buscar: ").strip()
    for i in range(len(cursos)):
        if cursos[i].lower() == nombre.lower():
            print(f"\nCurso encontrado: {cursos[i]} - Nota: {notas[i]}")
            return
    print("Curso no encontrado")
    
   
# 6. Actualizar Nota 
def actualizar_nota():
    nombre = input("Ingrese el nombre del curso: ").strip()
    
  if nombre in cursos:
        i = cursos.index(nombre)
        print(f"Nota actual de {nombre}: {notas[i]}")
        
  try:
            nueva = float(input("Ingrese la nueva nota: "))
            if 0 <= nueva <= 100:
                
  historial_cambios.append(f"{nombre} | Nota anterior: {notas[i]} | Nueva nota: {nueva}")
               notas[i] = nueva
               print("Nota Actualizada")
            else:("la Nota debe estar entre 0 y 100")
        except ValueError:
            print("Ingrese un número válido") 
    else:
        ("Curso no encontrado")    
        
# 7. Eliminar Curso
def eliminar_curso():
    mostrar_cursos()    
    try:
        pos = int(input("Ingrese el número de cursos a eliminar: ")) - 1 
        if 0 <= pos < len(cursos):
            eliminado = cursos.pop(pos)
            nota_eliminada = notas.pop(pos)
            print(f"Curso '{eliminado}' eliminado (nota {nota_eliminada}).")
        else:
            print("Número Inválido")   
    except ValueError:
        print("Debe ingresar un número válido")
        
# 8. Ordenar cursos por nota (ordenamiento burbuja)
def ordenar_por_nota():
    n = len(notas)
    for i in range(n - 1 ):
        for j in range(n - i - 1 ):
            if notas[j] > notas[j - 1]:
                notas[j], notas[j + 1] = notas[j + 1], notas[j]
                cursos[j], cursos[j + 1 ] = cursos[j + 1 ], cursos[j]
    print("Cursos ordenados por nota (menor a mayor): ")   
    mostrar_cursos()        
    
# 9. Ordenar cursos por nombre (ordenamiento burbuja)
def ordenar_por_nombre():
    n = len(curos)
    for i in range(n - 1 ):
        for j in range(n - i - j):
            if cursos[j].lower() > cursos[j + 1].lower():
                cursos[j], cursos[j + 1] = cursos[j + 1], cursos[j]
                notas[j], notas[j + 1] = notas[j + 1], notas[j]
        print("Cursos ordenados alfabéticamente")
        mostrar_cursos()
        
# 10.  Buscar curso por nombre (búsqueda binaria)   
def buscar_curso_binario():
    ordenar_por_nombre() # la busqueda binaria necesita una lista ordenada
    nombre = input("Ingrese el nombre del curso a buscar: ").strip().lower()
    izq, der = 0, len(cursos) - 1 
    
   while izq <= der:
        medio  = (izq + der) // 2
        if cursos[medio].lower() == nombre:
            print(f"\nCurso encontrado: {cursos[medio]} - Nota: {notas[medio]}")
            return
        elif nombre < cursos[medio].lower():
            der = medio - 1 
        else:
            izq = medio - 1 
            
  print("Curso no encontrado")
    
# 11. Simular cola de solicitudes de revisión
def simular_cola():
    cola_revisiones = []
    
  while True:
        print("\n=== Menú de Solicitudes de Revisión ===")
        print("1. Agregar solicitud")
        print("2. Atender siguiente solicitud")
        print("3. Mostrar cola actual")
        print("4. Salir de la simulación")
        
  opcion = input("Seleccione una opción: ")
        
  if opcion == "1":
            solicitud = input("Ingrese el nombre del curso para revisión: ")
            cola_revisiones.append(solicitud)
            print(f"Solicitud agregada: {solicitud}")
            
  elif opcion == "2":
            if cola_revisiones:
                atendida = cola_revisiones.pop(0)
                print(f"Se atendió la solicitud de: {atendida}")
            else:
                print("No hay solicitudes en la cola")
        
  elif opcion == "3":
            if cola_revisiones:
                print("\nSolicitudes en espera:")
                for i in range(len(cola_revisiones)):
                    print(f"{i + 1}. {cola_revisiones[i]}")
                else: 
                    print("No hay solicitudes pendientes")
                    
  elif opcion == "4":
            print("Saliendo de la simulación de cola")
            break
        
  else:
            print("Opción inválida. Intente de nuevo")
            
# 12. Mostrar historial de cambios (pila)
def mostrar_historial():
    # Muestra los cambios realizados en una pila. último en entrar, primero en salir
    if historial_cambios:
        print("\n Historial de cambios")
        for cambio in reversed(historial_cambios):
            print(cambio)
    else:
        print("No hay cambios registrados")
        
#         Bucle Principal
while True:
    mostrar_menu()
    try:
        opcion = int(input("Elija una opción (1-13): "))
    except ValueError:
        print("Debe ingresar un número válido.")
        continue
    
#Estructura con todas las opciones del menú
    if opcion == 1: registrar_curso()
    elif opcion == 2: mostrar_cursos()
    elif opcion == 3: promedio()
    elif opcion == 4: contar_aprobados_reprobados()
    elif opcion == 5: busqueda_curso_lineal()
    elif opcion == 6: actualizar_nota()
    elif opcion == 7: eliminar_curso()
    elif opcion == 8: ordenar_por_nota()
    elif opcion == 9: ordenar_por_nombre()
    elif opcion == 10: buscar_curso_binario()
    elif opcion == 11: simular_cola()
    elif opcion == 12: mostrar_historial()
    elif opcion == 13:
        print("Gracias por usar el programa. ¡Hasta pronto!")
        break
    else:
        print("Opción inválida.")

   #Pregunta si el usuario quiere continuar
    continuar = input("\n¿Desea realizar otra operación? (s/n): ").lower()
    if continuar != "s":
        print(" Programa finalizado.")
        break
