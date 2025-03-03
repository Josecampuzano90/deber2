using System;
using System.Collections.Generic;

class Traductor
{
    private static Dictionary<string, string> diccionario = new Dictionary<string, string>
    {
        {"time", "tiempo"}, {"person", "persona"}, {"year", "año"}, {"way", "camino"},
        {"day", "día"}, {"thing", "cosa"}, {"man", "hombre"}, {"world", "mundo"},
        {"life", "vida"}, {"hand", "mano"}, {"part", "parte"}, {"child", "niño/a"},
        {"eye", "ojo"}, {"woman", "mujer"}, {"place", "lugar"}, {"work", "trabajo"},
        {"week", "semana"}, {"case", "caso"}, {"point", "punto/tema"}, {"government", "gobierno"},
        {"company", "empresa/compañía"}
    };

    static void Main()
    {
        while (true)
        {
            Console.WriteLine("\nMENU");
            Console.WriteLine("=======================================================");
            Console.WriteLine("1. Traducir una frase");
            Console.WriteLine("2. Ingresar más palabras al diccionario");
            Console.WriteLine("0. Salir");
            Console.Write("Seleccione una opción: ");
            string opcion = Console.ReadLine();

            switch (opcion)
            {
                case "1":
                    TraducirFrase();
                    break;
                case "2":
                    AgregarPalabra();
                    break;
                case "0":
                    return;
                default:
                    Console.WriteLine("Opción no válida. Intente de nuevo.");
                    break;
            }
        }
    }

    static void TraducirFrase()
    {
        Console.Write("Ingrese la frase: ");
        string frase = Console.ReadLine().ToLower();
        string[] palabras = frase.Split(' ');
        
        for (int i = 0; i < palabras.Length; i++)
        {
            if (diccionario.ContainsKey(palabras[i]))
            {
                palabras[i] = diccionario[palabras[i]];
            }
            else if (diccionario.ContainsValue(palabras[i]))
            {
                palabras[i] = ObtenerClavePorValor(diccionario, palabras[i]);
            }
        }
        
        Console.WriteLine("Su frase traducida es: " + string.Join(" ", palabras));
    }

    static void AgregarPalabra()
    {
        Console.Write("Ingrese la palabra en inglés: ");
        string ingles = Console.ReadLine().ToLower();
        
        Console.Write("Ingrese la traducción en español: ");
        string espanol = Console.ReadLine().ToLower();
        
        if (!diccionario.ContainsKey(ingles))
        {
            diccionario.Add(ingles, espanol);
            Console.WriteLine("Palabra agregada exitosamente.");
        }
        else
        {
            Console.WriteLine("La palabra ya existe en el diccionario.");
        }
    }

    static string ObtenerClavePorValor(Dictionary<string, string> dicc, string valor)
    {
        foreach (var kvp in dicc)
        {
            if (kvp.Value == valor)
            {
                return kvp.Key;
            }
        }
        return valor;
    }
}
