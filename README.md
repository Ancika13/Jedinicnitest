Opšti pregled koda
Kod sadrži metodu za evaluaciju i izračunavanje matematičkih izraza, podržavajući osnovne aritmetičke operacije: sabiranje, oduzimanje, množenje i deljenje. Osnovne funkcije su:

Run(String expression): Metoda koja prima matematički izraz kao string i vraća rezultat kao string.
evaluateExpression(String expression): Metoda koja obrađuje string izraz, razdvaja brojeve i operacije, i prosleđuje ih metodi Calculate za izračunavanje.
Calculate(List<Float> numbers, List<String> operations): Rekurzivna metoda koja obračunava finalni rezultat na osnovu lista brojeva i operacija.
2. Detektovani nedostaci
Problem sa inicijalizacijom izraza: Ako izraz počinje sa znakom plus (+) ili minus (-), program dodaje nulu na početak, ali ovo može dovesti do grešaka u interpretaciji izraza.
Parseovanje izraza: Metoda koristi Operations.ToString() za kreiranje regexa koji se koristi za razdvajanje brojeva, što nije efikasno jer rezultira stringom +*-, što nije validan regex izraz. Potrebno je escape-ovati specijalne karaktere.
Rekurzivni poziv u Calculate: Logika rekurzije može dovesti do stack overflow greške ako je izraz previše kompleksan zbog velikog broja operacija.
Greške u proračunavanju prioriteta operacija: Postoji mogućnost da prioritet operacija nije uvek ispoštovan, naročito u kompleksnijim izrazima zbog načina na koji se operacije i brojevi uklanjaju iz lista.
Handleovanje beskonačnosti i grešaka: Ako korisnik unese Infinity ili -Infinity, program to prihvata, ali nije jasno kako su ovi slučajevi testirani u praksi.
Obrada grešaka: Program vraća "ERROR" za bilo koju grešku prilikom parsiranja brojeva, što može biti zbunjujuće jer ne specificira tip greške.
Jedinični test za metodu `Calculate`

Za testiranje metode `Calculate`, mogli bismo napisati jednostavan test koji proverava osnovne funkcionalnosti:

public class Simple_Test {

    public static void main(String[] args) {
        testExpression();
    }

    public static void testExpression() {
        String[] expressions = {
                "2+2",
                "5-2",
                "2*2",
                "2/2",
                "8/0"
        };

        String[] expectedResults = {
                "4.0",
                "3.0",
                "4.0",
                "1.0",
                "0.0"
        };

        for (int i = 0; i < expressions.length; i++) {
            String expression = expressions[i];
            String expectedResult = expectedResults[i];
            String actualResult = Calculator.Run(expression);

            if (expectedResult.equals(actualResult)) {
                System.out.println("Test case " + (i + 1) + " Passed");
            } else {
                System.out.println("Test case " + (i + 1) + "Failed" + "Expected: " + expectedResult);
                System.out.println("Actual: " + actualResult);
            }
        }
    }

}


---

