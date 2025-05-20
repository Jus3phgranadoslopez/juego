# juego
import random
import time

class Personaje:
    def __init__(self, nombre, vida, ataque):
        self.nombre = nombre
        self.vida = vida
        self.ataque = ataque

    def atacar(self, otro_personaje):
        daño = random.randint(0, self.ataque)
        otro_personaje.vida -= daño
        print(f"{self.nombre} ataca a {otro_personaje.nombre} y le causa {daño} de daño.")
        if otro_personaje.vida <= 0:
            print(f"{otro_personaje.nombre} ha sido derrotado.")

def crear_personaje(nombre, vida, ataque):
    return Personaje(nombre, vida, ataque)

def seleccionar_personaje(nombre_jugador):
    print(f"\n{nombre_jugador}, elige tu personaje:")
    print("1. Guerrero (Vida: 120, Ataque: 25)")
    print("2. Mago (Vida: 100, Ataque: 35)")
    print("3. Arquero (Vida: 110, Ataque: 30)")

    while True:
        opcion = input("Ingresa el número de tu personaje: ")
        if opcion == '1':
            return crear_personaje(f"{nombre_jugador} el Guerrero", 120, 25)
        elif opcion == '2':
            return crear_personaje(f"{nombre_jugador} el Mago", 100, 35)
        elif opcion == '3':
            return crear_personaje(f"{nombre_jugador} el Arquero", 110, 30)
        else:
            print("Opción inválida. Por favor, elige un número del menú.")

def combate(personaje1, personaje2):
    input("\n¡Comienza el combate! Presiona Enter para continuar...")
    turno = 0
    while personaje1.vida > 0 and personaje2.vida > 0:
        if turno % 2 == 0:
            atacante = personaje1
            defensor = personaje2
        else:
            atacante = personaje2
            defensor = personaje1

        atacante.atacar(defensor)

        if defensor.vida <= 0:
            break

        time.sleep(0.2)
        turno += 1

    if personaje1.vida > 0:
        print(f"¡{personaje1.nombre} gana el combate!")
        return personaje1
    else:
        print(f"¡{personaje2.nombre} gana el combate!")
        return personaje2

def main():
    nombre_jugador1 = input("Nombre del Jugador 1: ")
    jugador1 = seleccionar_personaje(nombre_jugador1)

    nombre_jugador2 = input("\nNombre del Jugador 2: ")
    jugador2 = seleccionar_personaje(nombre_jugador2)

    print(f"\n¡{jugador1.nombre} pelea contra {jugador2.nombre}!")

    ganador = combate(jugador1, jugador2)

if __name__ == "__main__":
    main()
