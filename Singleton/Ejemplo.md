# Problema que resuelva Singleton

## Contexto y Solución del Problema
Contexto: En aplicaciones grandes, como configuraciones de usuario, hay a menudo la necesidad de acceder y modificar configuraciones desde diferentes partes del programa. Si permitimos que múltiples instancias de un objeto de configuración coexistan, podríamos enfrentar problemas de sincronización y inconsistencias, como configuraciones que no se actualizan en todas las partes del programa o accesos concurrentes que provocan errores.

## Cómo el Patrón Singleton Ayuda:

* Instancia Única: Asegura que solo haya una instancia de la clase ConfigManager en todo el programa. Esto previene inconsistencias en la configuración ya que todas las partes del programa acceden a la misma instancia.

* Sincronización Segura: Usa un bloqueo (lock) para garantizar que en un entorno multi-hilo, solo una instancia de ConfigManager se cree, evitando problemas de sincronización y condiciones de carrera.

* Acceso Global: Proporciona un punto de acceso global a la configuración a través de ConfigManager.Instance, facilitando el acceso y la modificación de configuraciones desde cualquier lugar en el programa sin tener que pasar referencias de la instancia.

Este patrón es ideal para casos donde se necesita una única fuente de verdad y control centralizado sobre una funcionalidad específica, como la gestión de configuraciones en este ejemplo.

```csharp
using System;

public class ConfigManager
{
    // Instancia privada y estática del Singleton
    private static ConfigManager _instance;

    // Objeto para la sincronización de acceso a hilos
    private static readonly object _lock = new object();

    // Propiedad para acceder a la instancia del Singleton
    public static ConfigManager Instance
    {
        get
        {
            // Usamos doble verificación para garantizar que solo se cree una instancia
            if (_instance == null)
            {
                lock (_lock)
                {
                    if (_instance == null)
                    {
                        _instance = new ConfigManager();
                    }
                }
            }
            return _instance;
        }
    }

    // Constructor privado para evitar instanciación externa
    private ConfigManager()
    {
        // Cargar configuraciones iniciales
    }

    // Método de configuración para establecer valores
    public void SetConfig(string key, string value)
    {
        // Lógica para guardar configuración
        Console.WriteLine("Setting config '" + key + "' to '" + value + "'");
    }

    // Método para obtener configuraciones
    public string GetConfig(string key)
    {
        // Lógica para recuperar configuración
        return "configValue"; // Ejemplo
    }
}

public class Program
{
    public static void Main()
    {
        // Ejemplo de uso del Singleton
        ConfigManager config = ConfigManager.Instance;
        config.SetConfig("Theme", "Dark");
        Console.WriteLine(config.GetConfig("Theme")); // Imprime "configValue"
    }
}

```
# Corrida del programa
```plaintext
Setting config 'Theme' to 'Dark'
configValue
```
# Explicacion de la salida

Setting config 'Theme' to 'Dark': Este mensaje se imprime desde el método SetConfig para indicar que la configuración 'Theme' se ha establecido en 'Dark'.

configValue: Este mensaje se imprime desde el método GetConfig, que devuelve el valor de la configuración solicitada. En el ejemplo, el valor devuelto es un valor fijo "configValue" para ilustrar el funcionamiento del patrón Singleton.
