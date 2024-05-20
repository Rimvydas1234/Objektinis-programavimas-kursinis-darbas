1. Įvadas
a. Kas yra jūsų programa?
Ši programa yra skaičiuotuvo programa, skirta atlikti pagrindinius skaičiavimus (sudėtis, atimtis, daugyba ir dalyba), taip pat pažangius mokslinius skaičiavimus (kvadratas ir šaknis).
Ji įgyvendina pagrindinius objektinio programavimo principus ir dizaino šablonus, siekiant užtikrinti patikimumą ir skalėjimą.

b. Kaip paleisti programą?
Įsitikinkite, kad jūsų kompiuteryje įdiegta „Python“ programa.
Įrašykite pateiktą Python scenarijų į failą pavadinimu „calculator.py“.
Sukurkite CSV formato failą pavadinimu „operations.csv“, kuriame būtų pateikiami atliekami skaičiavimai, pateikti tokia pat tvarka, kaip parodyta žemiau:

add,5,3

subtract,10,4

multiply,2,8

divide,9,3

divide,5,0

Atidarykite terminalą arba komandinę eilutę.
Naviguokite į katalogą, kuriame yra „calculator.py“ ir „operations.csv“ failai.
Paleiskite scenarijų naudodami komandą:

python calculator.py

c. Kaip naudotis programa?
Programa nuskaito skaičiavimus iš „operations.csv“, juos apdoroja naudodama skaičiuotuvą ir rezultatus išveda į terminalą ir į failą pavadinimu „results.csv“. Norint plėsti funkcionalumą, į „operations.csv“ galima pridėti papildomų skaičiavimų.

2. Kūnas/Analizė
a. Paaiškinkite, kaip programa padengia (įgyvendina) funkcinius reikalavimus
Objektinis Programavimo Pagrindai:
Abstrakcija: Įgyvendinta per „AbstractCalculator“ klasę, kuri apibrėžia abstrakčias metodus pagrindiniams skaičiavimo veiksmams.

class AbstractCalculator(ABC):
    @abstractmethod
    def add(self, x, y):
        pass

    @abstractmethod
    def subtract(self, x, y):
        pass

    @abstractmethod
    def multiply(self, x, y):
        pass

    @abstractmethod
    def divide(self, x, y):
        pass
Paveldimumas: Demonstruojama „Calculator“ klasės paveldėjimu iš „AbstractCalculator“ ir „ScientificCalculator“ paveldėjimu iš „Calculator“.

class Calculator(AbstractCalculator):
    # Konkrečių metodų įgyvendinimas
    ...

class ScientificCalculator(Calculator):
    # Papildomi moksliniai metodai
    ...
    
Inkapsuliacija: Įgyvendinta uždarant rezultatą „Calculator“ klasėje naudojant privačią savybę „_result“.

class Calculator(AbstractCalculator):
    def __init__(self):
        self._result = 0  # Uždaras rezultatas
    ...
    def get_result(self):
        return self._result  # Viešas metodas, skirtas pasiekti rezultatą

        
Polimorfizmas: Pasiekiamas, tvarkant tiek „Calculator“, tiek „ScientificCalculator“ objektus kaip „AbstractCalculator“ objektus funkcijoje „perform_operations“.

def perform_operations(calc: AbstractCalculator, operations):
    ...


Dizaino Šablonai:
Factory Method (Requirement 2):

The create_calculator function acts as a factory method.
It creates instances of either the Calculator or ScientificCalculator class based on the input type specified.
This approach enhances flexibility, allowing the code to easily switch between different types of calculators based on requirements.

# Example usage
filename = 'operations.csv'
operations = read_input_from_file(filename)

results = []
for operation in operations:
    op, x, y = operation
    calc = create_calculator("basic")  # Create calculator based on operation type
    if op == 'add':
        result = calc.add(x, y)
    elif op == 'subtract':
        result = calc.subtract(x, y)
    elif op == 'multiply':
        result = calc.multiply(x, y)
    elif op == 'divide':
        result = calc.divide(x, y)
    print(f"Operation: {op}, Inputs: {x}, {y}, Result: {result}")
    results.append((op, x, y, result))

output_filename = 'results.csv'
write_output_to_file(output_filename, results)

# Demonstration of using inheritance
sci_calc = create_calculator("scientific")
sci_calc.add(2, 3)
print(sci_calc.get_result())  # Output: 5
sci_calc.square(4)
print(sci_calc.get_result())  # Output: 16
sci_calc.square_root(16)
print(sci_calc.get_result())  # Output: 4.0


Singletonas: Užtikrina, kad skaičiuotuvo vienintelis egzempliorius būtų naudojamas visoje programoje, nors tai šiame pavyzdyje nėra tiesiogiai rodoma.


Failų Operacijos:
Nuskaitymas iš Failo: Skaito skaičiavimus iš CSV formato failo.

def read_input_from_file(filename):
    ...
Rašymas į Failą: Rašo rezultatus į CSV formato failą.

python
Kopijuoti kodą
def write_output_to_file(filename, output):
    ...
    
Vienetinių Testų Vykdymas:
Pagrindinės skaičiavimo funkcijos yra testuojamos naudojant „unittest“ karkasą.

class TestCalculator(unittest.TestCase):
    def setUp(self):
        self.calc = Calculator()

    # Testavimo metodai kiekvienai operacijai
    ...
3. Rezultatai ir Santrauka

Sėkmingai įgyvendintas skaičiuotuvo programa, palaikanti pagrindinius ir mokslinius skaičiavimus.
Rezultatas buvo uždaromas „Calculator“ klasėje, kad būtų laikomasi objektinio programavimo principų.
Polimorfizmas buvo sėkmingai naudojamas, naudojant bendrą sąsają skirtingų skaičiuotuvų tipams.
Implementuotos failų nuskaitymo ir rašymo operacijos, skirtos įvesties ir išvesties operacijoms tvarkyti.
Iššūkiai
Užtikrinti patikimą nuliu dalijimo tvarką.
Plėsti pagrindinį skaičiuotuvą, įtraukiant mokslinius metodus, nesugriaunant esamos funkcionalumo.

4. Išvados
Svarbiausių Išvadų Santrauka
Skaičiuotuvo programa sėkmingai demonstruoja pagrindinius objektinio programavimo principus.
Polimorfizmas ir paveldimumas buvo efektyviai naudojami, siekiant išplėsti skaičiuotuvo funkcionalumą.
Programos struktūra leidžia lengvai praplėsti ir palaikyti ją.

Būsimi Perspektyvai
Įdiegti papildomus mokslinius metodus ir galbūt integruoti daugiau dizaino šablonų.
Kūrimas grafinės vartotojo sąsajos (GUI) siekiant pagerinti vartotojo sąveiką.
Plėsti failų tvarkymą, kad būtų palaikomi skirtingi formatai (pvz., JSON, XML).
