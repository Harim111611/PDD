# Actividad B24B21
Alumno: Luna Hernandez Harim 

No.Control 20211803

# Primer giro
![image](https://github.com/user-attachments/assets/bce07dd8-b161-4841-b5c0-a9e10abe9fff)


* Categoría: Comportamiento
* Dominio: Entretenimiento
* Requisito: Encapsulación de Comportamientos
* Patrón de diseño seleccionado: 

# Problema:
En el universo de Los Caballeros del Zodiaco, cada caballero tiene un comportamiento de ataque que varía según su signo y armadura. Queremos encapsular estos diferentes comportamientos de ataque para que puedan ser intercambiables sin modificar el código del caballero. Esto ayudará a cambiar el comportamiento de un caballero en tiempo de ejecución sin modificar la clase principal.

# Solución:
Para resolver este problema, podemos usar el Patrón Estrategia (Strategy Pattern), que pertenece a las categorías creacional y comportamental. Este patrón permite definir una familia de algoritmos o comportamientos, encapsularlos en clases separadas y hacerlos intercambiables, permitiendo que el comportamiento del objeto cambie dinámicamente.

# Diseño:
Cada caballero tendrá un comportamiento de ataque encapsulado en una estrategia de ataque.
Cada estrategia será una clase separada y podrá intercambiarse dinámicamente.

# Codigo en C#
```csharp
using System;

// Interfaz que define la estrategia de ataque
public interface IAttackStrategy
{
    void Attack();
}

// Estrategia de ataque: Meteoro de Pegaso
public class PegasusMeteorAttack : IAttackStrategy
{
    public void Attack()
    {
        Console.WriteLine("¡Pegaso: Meteoro de Pegaso!");
    }
}

// Estrategia de ataque: Polvo de Diamante
public class DiamondDustAttack : IAttackStrategy
{
    public void Attack()
    {
        Console.WriteLine("¡Cisne: Polvo de Diamante!");
    }
}

// Estrategia de ataque: Excalibur
public class ExcaliburAttack : IAttackStrategy
{
    public void Attack()
    {
        Console.WriteLine("¡Capricornio: Excalibur!");
    }
}

// Clase Caballero del Zodiaco que usa una estrategia de ataque
public class Saint
{
    private IAttackStrategy _attackStrategy;

    public Saint(IAttackStrategy attackStrategy)
    {
        _attackStrategy = attackStrategy;
    }

    // Método para cambiar la estrategia de ataque en tiempo de ejecución
    public void SetAttackStrategy(IAttackStrategy newStrategy)
    {
        _attackStrategy = newStrategy;
    }

    public void PerformAttack()
    {
        _attackStrategy.Attack();
    }
}

// Clase de prueba
public class Program
{
    public static void Main(string[] args)
    {
        // Crear un caballero con el ataque Meteoro de Pegaso
        Saint seiya = new Saint(new PegasusMeteorAttack());
        seiya.PerformAttack();

        // Cambiar el comportamiento a Polvo de Diamante
        seiya.SetAttackStrategy(new DiamondDustAttack());
        seiya.PerformAttack();

        // Cambiar el comportamiento a Excalibur
        seiya.SetAttackStrategy(new ExcaliburAttack());
        seiya.PerformAttack();
    }
}

```
# Corrida
```plaintext
¡Pegaso: Meteoro de Pegaso!
¡Cisne: Polvo de Diamante!
¡Capricornio: Excalibur!
```


# Explicación del Código

El código utiliza el Patrón Estrategia para permitir que un Caballero del Zodiaco (representado por la clase Saint) pueda ejecutar diferentes ataques sin cambiar su estructura interna.

* Interfaz `IAttackStrategy`: Define el método Attack(), que debe ser implementado por todas las estrategias de ataque.

* Clases concretas de ataque: Cada ataque (`PegasusMeteorAttack, DiamondDustAttack, ExcaliburAttack`) implementa la interfaz `IAttackStrategy` y define su propio comportamiento en el método Attack().

* Caballero `Saint`: Tiene una referencia a una estrategia de ataque (`IAttackStrategy`). Usa esta referencia para realizar ataques mediante el método `PerformAttack()`.

* Cambio dinámico: El caballero puede cambiar su ataque en tiempo de ejecución con el método `SetAttackStrategy`().

El caballero realiza ataques diferentes (Pegaso, Cisne y Capricornio) sin modificar su propia clase.

# Codigo en el Compilador online
https://dotnetfiddle.net/8UmIAl

# Segundo Giro

![image](https://github.com/user-attachments/assets/ca2a9a2b-19a3-437e-a246-cd3af8a4fc03)


* Categoría: Creacional
* Dominio: Tecnología
* Requisito: Reutilización de Código y Componentes
* Patrón de diseño seleccionado:  

# Problema:


# Solución:


# Diseño:

# Codigo en C#

# Corrida
```plaintext

```

# Explicación del Código


# Codigo en el Compilador online

