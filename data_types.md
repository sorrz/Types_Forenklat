# Data typer

# Grundläggande datatyper i C#

Nedan förklaras de vanligaste datatyperna. De är grundläggande byggstenar i C# (programmering)  och används för att lagra olika typer av data i dina program. Valet av datatyp beror på vilken information du behöver hantera och hur du planerar att använda den i din kod.

## Heltal (Integer)

- **int:** 32-bitars heltal, mest använd
    
    Exempel: `int ålder = 25;`
    
- **long:** 64-bitars heltal för större numeriska värden
    
    Exempel: `long befolkning = 7800000000;`
    
- **short:** 16-bitars heltal för mindre numeriska värden
    
    Exempel: `short temperatur = -5;`
    
- **byte:** 8-bitars osignerat heltal (0 till 255)
    
    Exempel: `byte ljusstyrka = 128;`
    

## Flyttal (Floating-point)

- **float:** 32-bitars flyttal med enkel precision
    
    Exempel: `float pi = 3.14f;`
    
- **double:** 64-bitars flyttal med dubbel precision, mest använd
    
    Exempel: `double distans = 384400.0;`
    
- **decimal:** 128-bitars flyttal med hög precision, ofta använd för finansiella beräkningar
    
    Exempel: `decimal pris = 19.99m;`
    

## Boolesk

- **bool:** Representerar sant (true) eller falskt (false)
    
    Exempel: `bool ärStudent = true;`
    

## Tecken och strängar

- **char:** Enskilt 16-bitars Unicode-tecken
    
    Exempel: `char första = 'A';`
    
- **string:** Sekvens av Unicode-tecken
    
    Exempel: `string namn = "Anna";`
    

## Datum och tid

- **DateTime:** Representerar datum och tid
    
    Exempel: `DateTime nu = DateTime.Now;`
    
- **TimeSpan:** Representerar en tidsperiod
    
    Exempel: `TimeSpan varaktighet = TimeSpan.FromHours(2);`
    

## Objekt

- **object:** Bastyp för alla andra typer i C#
    
    Exempel: `object data = 42;`
    

---

# Sammansatta typer och egna typer

För att hantera mer komplexa datastrukturer, som till exempel beskrivningen av en bil eller flera bilar, kan man använda sammansatta typer och skapa egna typer i C#. Här är några exempel:

## Klasser

Klasser är den vanligaste typen för att skapa egna datatyper. De kan innehålla både data (egenskaper) och beteenden (metoder).

```csharp
public class Bil
{
    public string Märke { get; set; }
    public string Modell { get; set; }
    public int Årsmodell { get; set; }
    public double Pris { get; set; }
}
```

## Structs

Structs är värdetyper och används ofta för små datastrukturer.

```csharp
public struct Färg
{
    public byte Röd;
    public byte Grön;
    public byte Blå;
}
```

## Enums

Enums används för att representera en grupp av konstanter.

```csharp
public enum BilTyp
{
    Sedan,
    Kombi,
    SUV,
    Sportbil
}
```

## Listor och arrayer

För att hantera flera bilar kan man använda listor eller arrayer:

```csharp
List<Bil> bilLista = new List<Bil>(); // Ny tom lista är muterande och tar så mykt plats den behöver i minnet.
Bil[] bilArray = new Bil[10]; // Skapar en tom array med 10 lediga platser för datatypen som används, i detta fall Bil. Arrayer låser plats i minnet även om de är tomma.
```

## Exempel på användning

Här är ett exempel på hur man kan använda dessa typer tillsammans:

```csharp
// Typ, Variabel = tilldelning eller initiering
Bil minBil = new Bil      // Detta kallas att initiera ett object.
{
    Märke = "Volvo",
    Modell = "V60",
    Årsmodell = 2023,
    Pris = 450000
};

minBil.Färg = new Färg { Röd = 255, Grön = 0, Blå = 0 };
minBil.Typ = BilTyp.Kombi;

List<Bil> bilpark = new List<Bil>();
bilpark.Add(minBil);
```

Genom att använda dessa tekniker kan du skapa mer komplexa och meningsfulla datastrukturer som bättre representerar verkliga objekt och koncept i dina C#-program.

---

# Träningsuppgift: Skapa en produkttyp för en mataffär

Mål:

Denna uppgift är utformad för att hjälpa dig att förstå hur man skapar och använder egna typer i C#, samt grundläggande kunskap i hur man kan arbeta med listor och enums. 
Lycka till!

Uppgiften: 

I denna uppgift ska du skapa en egen datatyp för att representera produkter i en mataffär. Detta kommer att ge dig praktisk erfarenhet av att arbeta med egna typer i C#.

## Uppgiftsbeskrivning

- Skapa en klass som heter `Produkt` med följande egenskaper:
    - Namn (string)
    - Pris (decimal)
    - Vikt (double, i kg)
    - Kategori (använd en enum för olika matkategorier)

**Avancerade uppgifter:**

- Lägg till en konstruktor som tar emot värden för alla egenskaper
- Implementera en metod `VisaInfo()` som skriver ut all information om produkten
- Skapa en lista av typen produkt och lägg till minst 5 olika produkter

**Överkurs:**

- Skriv en metod som hittar den dyraste produkten i listan
- Skriv en metod som beräknar det totala värdet av alla produkter i listan
