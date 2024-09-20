###Ejemplo De Singleton Usando como tematica Los caballeros del zodiaco

```csharp

using System;

public class Santuario
{
    private static readonly Lazy<Santuario> instanciaUnica = new Lazy<Santuario>(() => new Santuario());

    public string CaballeroGuardian { get; private set; }

    private Santuario()
    {
        CaballeroGuardian = "Saga de Géminis";
    }

    public static Santuario ObtenerInstancia()
    {
        return instanciaUnica.Value;
    }

    public void CambiarGuardian(string nuevoGuardian)
    {
        CaballeroGuardian = nuevoGuardian;
        Console.WriteLine("El nuevo guardián del Santuario es: " + CaballeroGuardian);
    }
}

public class Programa
{
    public static void Main(string[] args)
    {
        Santuario santuario1 = Santuario.ObtenerInstancia();
        Console.WriteLine("Guardia actual: " + santuario1.CaballeroGuardian);

        Santuario santuario2 = Santuario.ObtenerInstancia();

        santuario1.CambiarGuardian("Seiya de Pegaso");

        Console.WriteLine("Guardia actual (desde la segunda instancia): " + santuario2.CaballeroGuardian);
    }
}
```
