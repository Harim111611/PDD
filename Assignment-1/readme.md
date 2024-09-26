# Actividad B24B21
Alumno: Luna Hernandez Harim 

No.Control 20211803

# Primer giro
![image](https://github.com/user-attachments/assets/bce07dd8-b161-4841-b5c0-a9e10abe9fff)


* Categoría: Comportamiento
* Dominio: Entretenimiento
* Requisito: Encapsulación de Comportamientos
* Patrón de diseño seleccionado: Strategy Pattern

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
<br>
<br>
<br>

# Segundo Giro

![image](https://github.com/user-attachments/assets/ca2a9a2b-19a3-437e-a246-cd3af8a4fc03)


* Categoría: Creacional
* Dominio: Tecnología
* Requisito: Reutilización de Código y Componentes
* Patrón de diseño seleccionado:  Factory

# Problema:

En el universo de Warhammer 40k, diferentes tipos de armas tecnológicas son usadas por diversas facciones, como los Marines Espaciales, la Guardia Imperial, o los Necrones. Cada facción tiene armas con características específicas (daño, rango, tipo de munición, etc.), pero todas siguen una estructura común de "Arma". El reto es crear un sistema en el que se puedan generar diferentes tipos de armas sin cambiar el código base, promoviendo la reutilización de código y facilitando la adición de nuevas armas en el futuro.


# Solución: Patrón Factory

Usamos el patrón de diseño Factory para crear objetos de diferentes tipos de armas sin exponer la lógica de creación al cliente. De esta manera, el cliente solo interactúa con una interfaz común y no tiene que preocuparse por las particularidades de cada tipo de arma.

# Codigo en C#
```csharp
using System;

// Interfaz común para las armas
public interface IWeapon
{
    void DisplaySpecifications();
}

// Clases concretas que implementan la interfaz para diferentes armas
public class Bolter : IWeapon
{
    public void DisplaySpecifications()
    {
        Console.WriteLine("Weapon: Bolter\nDamage: 20\nRange: 24 units\nAmmo Type: Standard Bolts");
    }
}

public class Lasgun : IWeapon
{
    public void DisplaySpecifications()
    {
        Console.WriteLine("Weapon: Lasgun\nDamage: 10\nRange: 36 units\nAmmo Type: Energy");
    }
}

public class GaussFlayer : IWeapon
{
    public void DisplaySpecifications()
    {
        Console.WriteLine("Weapon: Gauss Flayer\nDamage: 25\nRange: 30 units\nAmmo Type: Energy");
    }
}

// Fábrica para la creación de armas
public abstract class WeaponFactory
{
    public abstract IWeapon CreateWeapon();
}

// Fábricas concretas que crean armas específicas
public class BolterFactory : WeaponFactory
{
    public override IWeapon CreateWeapon()
    {
        return new Bolter();
    }
}

public class LasgunFactory : WeaponFactory
{
    public override IWeapon CreateWeapon()
    {
        return new Lasgun();
    }
}

public class GaussFlayerFactory : WeaponFactory
{
    public override IWeapon CreateWeapon()
    {
        return new GaussFlayer();
    }
}

// Cliente
public class WeaponSelectionSystem
{
    private WeaponFactory _weaponFactory;

    public WeaponSelectionSystem(WeaponFactory weaponFactory)
    {
        _weaponFactory = weaponFactory;
    }

    public void DisplayWeapon()
    {
        IWeapon weapon = _weaponFactory.CreateWeapon();
        weapon.DisplaySpecifications();
    }
}

// Ejecución
public class Program
{
    public static void Main(string[] args)
    {
        // Selección de un Bolter
        WeaponFactory bolterFactory = new BolterFactory();
        WeaponSelectionSystem weaponSystem = new WeaponSelectionSystem(bolterFactory);
        weaponSystem.DisplayWeapon();

        Console.WriteLine();

        // Selección de un Lasgun
        WeaponFactory lasgunFactory = new LasgunFactory();
        weaponSystem = new WeaponSelectionSystem(lasgunFactory);
        weaponSystem.DisplayWeapon();

        Console.WriteLine();

        // Selección de un Gauss Flayer
        WeaponFactory gaussFlayerFactory = new GaussFlayerFactory();
        weaponSystem = new WeaponSelectionSystem(gaussFlayerFactory);
        weaponSystem.DisplayWeapon();
    }
}

```

# Corrida
```plaintext
Weapon: Bolter
Damage: 20
Range: 24 units
Ammo Type: Standard Bolts

Weapon: Lasgun
Damage: 10
Range: 36 units
Ammo Type: Energy

Weapon: Gauss Flayer
Damage: 25
Range: 30 units
Ammo Type: Energy


```

# Explicación del Código
 
* Interfaz IWeapon: Define una interfaz común para todas las armas. Todas las armas tendrán que implementar el método DisplaySpecifications(), que mostrará las especificaciones de esa arma en particular.

* Clases concretas (Bolter, Lasgun, GaussFlayer): Cada clase concreta representa un tipo específico de arma. Estas clases implementan la interfaz IWeapon, proporcionando sus propias especificaciones.

* Fábrica abstracta WeaponFactory: Esta es una clase abstracta que declara el método CreateWeapon(). Las subclases concretas que la extienden implementarán la lógica de creación para diferentes tipos de armas.

* Fábricas concretas: Tenemos tres fábricas concretas (BolterFactory, LasgunFactory, GaussFlayerFactory), cada una de las cuales es responsable de crear su tipo de arma específico.

* Cliente WeaponSelectionSystem: El cliente no sabe ni le importa qué tipo de arma se está creando. Solo necesita interactuar con la fábrica y obtener un objeto de arma que sigue la interfaz común.

* Ejecución del sistema: El cliente selecciona un tipo de arma (usando una fábrica concreta) y el sistema se encarga de generar el arma correspondiente y mostrar sus especificaciones.

# Codigo en el Compilador online
https://dotnetfiddle.net
