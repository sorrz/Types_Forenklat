# Klasser forts.

När vi pratar om klasser, så pratar vi oftast om en fil som heter tillexempel `bil.cs` och innehåller information för hur datorn ska skapa typen BIL. Vissa har en konstruktor som kräver att man vi initiering av en ny Bil skickar in information som krävs för att skapa ett objekt. 

Till exempel, om jag vill skapa en ny bil i verkliga världen, så kanske jag måste ha ett chassi-nummer från staten, därefter kan jag börja bygga den och vartefter lägga till information kring modell, märke, år, drivmedel osv.

Nedan finns tydliga exempel på hur lite olika klasser kan se ut och fungera.

### 1. **Klasser som skapar egna typer**

Dessa klasser definierar de objekt vi arbetar med, t.ex. klassen `Bil`, och de kan ha olika egenskaper som definierar dem.

### 2. **Klasser som tar in andra typer**

Det här är klasser som arbetar med eller bearbetar andra typer, t.ex. en klass som tar in en lista av `Bil`-objekt och utför operationer på den.

### 3. **Utility-klasser**

Utility-klasser innehåller generella metoder som är oberoende av specifika datatyper, och kan till exempel sortera listor, filtrera data eller returnera statistik baserat på en given lista.

### Exempel:

### Klass: `Bil` (skapar en typ)

```cs
using System;
using System.Collections.Generic;
using System.Linq;

public class Bil
{
    public string Märke { get; set; }
    public string Modell { get; set; }
    public int Årsmodell { get; set; }
    public double Pris { get; set; }
    public Färg Färg { get; set; }
    public BilTyp Typ { get; set; }
}

```

### Struct: `Färg` (definierar en värdetyp)

```cs
public struct Färg
{
    public byte Röd;
    public byte Grön;
    public byte Blå;
}

```

### Enum: `BilTyp` (representerar en grupp av konstanter)

```csharp
csharp
Kopiera kod
public enum BilTyp
{
    Sedan,
    Kombi,
    SUV,
    Sportbil
}

```

### Klass: `BilService` (tar in listor av bilar och utför operationer)

Denna klass tar in andra typer, t.ex. en lista av `Bil`-objekt, och utför operationer på dem. Det kan handla om att söka efter bilar med ett visst märke eller att filtrera bilar baserat på pris.

```cs
public class BilService
{
    private List<Bil> _bilar;

    public BilService(List<Bil> bilar)
    {
        _bilar = bilar;
    }

    // Metod för att filtrera bilar baserat på pris
    public List<Bil> FiltreraBilarEfterPris(double maxPris)
    {
        return _bilar.Where(b => b.Pris <= maxPris).ToList();
    }

    // Metod för att hitta bilar av ett specifikt märke
    public List<Bil> HittaBilarAvMarke(string marke)
    {
        return _bilar.Where(b => b.Märke == marke).ToList();
    }

    // Metod för att sortera bilar efter årsmodell
    public List<Bil> SorteraBilarEfterÅrsmodell()
    {
        return _bilar.OrderBy(b => b.Årsmodell).ToList();
    }
}

```

### Utility-klass: `BilUtility` (sorterar och returnerar resultat, oberoende av typ)

Detta är en utility-klass som inte är beroende av specifika objekt men kan bearbeta generella listor och ge information som statistik eller sortering.

```cs
public static class BilUtility
{
    // En metod som returnerar genomsnittspriset för en lista av bilar
    public static double BeräknaGenomsnittPris(List<Bil> bilar)
    {
        if (bilar.Count == 0)
        {
            return 0;
        }
        return bilar.Average(b => b.Pris);
    }

    // En metod som räknar antalet bilar av en viss typ
    public static int RäknaBilarAvTyp(List<Bil> bilar, BilTyp typ)
    {
        return bilar.Count(b => b.Typ == typ);
    }
}

```

### Exempel på användning

```cs
class Program
{
    static void Main()
    {
        // Skapa en lista med några bilar
        List<Bil> bilpark = new List<Bil>
        {
            new Bil { Märke = "Volvo", Modell = "V60", Årsmodell = 2023, Pris = 450000, Färg = new Färg { Röd = 255, Grön = 0, Blå = 0 }, Typ = BilTyp.Kombi },
            new Bil { Märke = "BMW", Modell = "X5", Årsmodell = 2021, Pris = 650000, Färg = new Färg { Röd = 0, Grön = 255, Blå = 0 }, Typ = BilTyp.SUV },
            new Bil { Märke = "Audi", Modell = "A4", Årsmodell = 2020, Pris = 300000, Färg = new Färg { Röd = 0, Grön = 0, Blå = 255 }, Typ = BilTyp.Sedan }
        };

        // Använd BilService för att filtrera och sortera bilar
        BilService bilService = new BilService(bilpark);
        List<Bil> bilarUnder500k = bilService.FiltreraBilarEfterPris(500000);
        List<Bil> sorteradeBilar = bilService.SorteraBilarEfterÅrsmodell();

        // Använd BilUtility för att beräkna genomsnittspris
        double genomsnittPris = BilUtility.BeräknaGenomsnittPris(bilpark);
        int antalSUV = BilUtility.RäknaBilarAvTyp(bilpark, BilTyp.SUV);

        // Visa resultaten
        Console.WriteLine("Bilar under 500 000 kr:");
        foreach (var bil in bilarUnder500k)
        {
            Console.WriteLine($"{bil.Märke} {bil.Modell} - {bil.Pris} kr");
        }

        Console.WriteLine($"\nGenomsnittspriset på bilar: {genomsnittPris} kr");
        Console.WriteLine($"Antal SUV-bilar: {antalSUV}");
    }
}

```

### Förklaring av vad vi har gjort:

1. **Klass `Bil`**: Skapar en egen typ med egenskaper som `Märke`, `Modell`, `Årsmodell`, `Pris`, `Färg`, och `BilTyp`.
2. **Struct `Färg`**: Definierar en enkel värdetyp som representerar bilens färg med tre `byte`värden: `Röd`, `Grön`, och `Blå`.
3. **Enum `BilTyp`**: Definierar olika biltyper som en uppsättning konstanter (t.ex. `Sedan`, `Kombi`, `SUV`, `Sportbil`).
4. **Klass `BilService`**: Är en tjänst som tar en lista av `Bil`objekt och utför operationer som filtrering efter pris, sortering efter årsmodell och sökning baserat på märke.
5. **Utility-klass `BilUtility`**: Är en klass som innehåller statiska metoder som kan användas oberoende av ett specifikt objekt. Dessa metoder är användbara för att t.ex. beräkna genomsnittspris eller räkna bilar av en viss typ.
