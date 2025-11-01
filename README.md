class Calculadora:
    numero1 = 0
    numero2 = 0

    def _init_(self, numero1=0, numero2=0):  
        self._numero1 = numero1  
        self._numero2 = numero2  
        self._historial = []  
   
    """-------setter an getter-------"""  
    @property  
    def numero1(self):  
        return self._numero1  
   
    @numero1.setter  
    def numero1(self, nuevo_numero1):  
        if type(nuevo_numero1) in (int, float):  
            self._numero1 = nuevo_numero1  
        else:  
            raise ValueError("Debe ser un número")  

    @property  
    def numero2(self):  
        return self._numero2  
       
    @numero2.setter  
    def numero2(self, nuevo_numero2):  
        if type(nuevo_numero2) in (int, float):  
            self._numero2 = nuevo_numero2  
        else:  
            raise ValueError("Debe ser un número")  
           
    # Métodos de operaciones  
    def sumar(self):  
        return self._numero1 + self._numero2  

    def restar(self):  
        return self._numero1 - self._numero2  

    def multiplicar(self):  
        return self._numero1 * self._numero2  

    def dividir(self):  
        if self._numero2 != 0:  
            return self._numero1 / self._numero2  
        else:  
            return "Error: No se puede dividir entre cero."  

    def ver_historial(self):  
        for operacion in self._historial:  
            print(operacion)  

    def agregar_a_historial(self, operacion):  
        self._historial.append(operacion)


def interpretar_expresion(expresion):
    """Interpreta expresión matemática ingresada"""
    for operador in ['+', '-', '*', '/']:
        if operador in expresion:
            partes = expresion.split(operador)
            if len(partes) == 2:
                try:
                    num1 = float(partes[0].strip())
                    num2 = float(partes[1].strip())
                    return num1, num2, operador
                except ValueError:
                    print("Solo se aceptan números, intente de nuevo\n")
                    return None
    return None


def main():
    calc = Calculadora()
    print("Calculadora Básica. Escribe 'salir' para terminar o 'historial' para ver operaciones.\n")

    while True:  
        entrada = input("Ingresa la operación (ejemplo: 5+5): ")  
      
        if entrada.strip().lower() == "salir":  
            print("¡Hasta pronto!")  
            break  
                      
        if entrada.strip().lower() == "historial":  
            calc.ver_historial()  
            continue  
                      
        resultado = interpretar_expresion(entrada)  
        if not resultado:  
            print("Expresión no válida. Usa el formato: número operador número (ej. 5 + 5)\n")  
            continue  

        num1, num2, operador = resultado  
        calc.numero1 = num1  
        calc.numero2 = num2  

        if operador == '+':  
            print("Resultado:", calc.sumar())  
        elif operador == '-':  
            print("Resultado:", calc.restar())  
        elif operador == '*':  
            print("Resultado:", calc.multiplicar())  
        elif operador == '/':  
            print("Resultado:", calc.dividir())  
                          
main()







Calculadora.py

class Calculadora:
    def __init__(self):
        self.historial = []

    def interpretar_expresion(self, expresion):
        """
        Interpreta la expresión matemática ingresada y realiza la operación correspondiente.
        """
        partes = expresion.split()
        if len(partes) != 3:
            raise ValueError("La expresión debe contener exactamente tres números y dos operadores.")

        num1 = float(partes[0])
        operador1 = partes[1]
        num2 = float(partes[2])
        operador2 = partes[3]
        num3 = float(partes[4])

        if operador1 == '+':
            resultado = num1 + num2
        elif operador1 == '-':
            resultado = num1 - num2
        elif operador1 == '*':
            resultado = num1 * num2
        elif operador1 == '/':
            if num2 == 0:
                raise ValueError("Error: División entre cero.")
            resultado = num1 / num2
        else:
            raise ValueError("Operador no válido.")

        if operador2 == '+':
            resultado += num3
        elif operador2 == '-':
            resultado -= num3
        elif operador2 == '*':
            resultado *= num3
        elif operador2 == '/':
            if num3 == 0:
                raise ValueError("Error: División entre cero.")
            resultado /= num3
        else:
            raise ValueError("Operador no válido.")

        self.historial.append(expresion)
        return resultado

    def ver_historial(self):
        for operacion in self.historial:
            print(operacion)






principal.py

from calculadora import Calculadora

def main():
    calc = Calculadora()
    print("Calculadora Básica. Escribe 'salir' para terminar o 'historial' para ver operaciones.")

    while True:
        entrada = input("Ingresa la operación (ejemplo: 5 + 5 + 5): ")

        if entrada.strip().lower() == "salir":
            print("¡Hasta pronto!")
            break

        if entrada.strip().lower() == "historial":
            calc.ver_historial()
            continue

        try:
            resultado = calc.interpretar_expresion(entrada)
            print("Resultado:", resultado)
        except ValueError as e:
            print(e)

if __name__ == "__main__":
    main()
