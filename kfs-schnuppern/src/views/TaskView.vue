<script setup>
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router'
import Editor from '../components/Editor.vue'
import Header from '../components/Header.vue'

const route = useRoute()

const tasks = ref([
  {
    id: 1,
    exampleCode: `"" // Schreibe hier "Hallo Welt" in Anführungszeichen!`,
    correct_answer: 'Hallo Welt'
  },
  {
    id: 2,
    exampleCode: `// Mache hier eine Funktion aus "Hallo Welt"
// Die Funktion soll "Hallo Welt" zurückgeben und "gibHalloWelt" heißen!

function <Funktionsname>() { // Eine Funktion ist ein Codeblock, der eine bestimmte Aufgabe erfüllt.
  return ""; // Hier muss "Hallo Welt" zurückgegeben werden. return heisst im programmieren "zurückgeben"
}

<Funktionsname>(); // Eine Funktion wird mit Funktionsname() aufgerufen. Die Klammern sind wichtig! Sie zeigen, dass es sich um eine Funktion handelt und diese ausgeführt werden soll.
    `,
    correct_answer: 'Hallo Welt'
  },
  {
    id: 3,
    exampleCode: `// Erstelle eine Variable mit dem Namen "name"
// und weise ihr den Wert "Max" zu.
// Gib dann die Variable zurück!

const name = <Wert>;

name;
    `,
    correct_answer: 'Max'
  },
  {
    id: 4,
    exampleCode: `// Erstelle eine Funktion "addiere", die zwei Zahlen als Parameter nimmt
// und deren Summe zurückgibt.

function addiere(a, b) {
  return <Ergebnis>; // Hier muss die Summe der beiden Zahlen zurückgegeben werden.
}

addiere(2, 3);
    `,
    correct_answer: '5'
  },
  {
    id: 5,
    exampleCode: `// Erstelle ein Array mit den Zahlen 1, 2 und 3.
// Greife auf das zweite Element zu.

const zahlen = [<Zahlen>];

zahlen[1]; // Ein Array beginnt bei 0 zu zählen und nicht bei 1! (Das heisst, dass das erste Element die Position 0 hat)
    `,
    correct_answer: '2'
  },
  {
    id: 6,
    exampleCode: `// Erstelle ein Objekt "person" mit den Eigenschaften "name" und "alter".
// Setze "name" auf "Lisa" und "alter" auf 25.

const person = { // Ein Objekt ist eine Sammlung von Eigenschaften. Diese Eigenschaften bestehen aus einem Namen und einem Wert.
  name: <Name>, 
  alter: <Alter>
};

person.name;
    `,
    correct_answer: 'Lisa'
  },
  {
    id: 7,
    exampleCode: `// Was muss in das Array geschrieben werden um die Zahlen 0-4 zu bekommen?

let zahlen = [];

for (let i = 0; i <= 6; i++) { // Die Schleife beginnt bei 0 und zählt bis 6. <= bedeutet "kleiner gleich" und bedeutet, dass die Schleife auch bei 6 noch einmal durchlaufen wird.
  zahlen.push(i); // push fügt ein Element am Ende des Arrays hinzu.
}

zahlen // Hier wird das Array ausgegeben.
    `,
    correct_answer: '0,1,2,3,4'
  },
  {
    id: 8,
    exampleCode: `// Schreibe eine Funktion, die prüft, ob eine Zahl gerade ist.
// Tipp: Eine Zahl ist gerade, wenn sie durch 2 teilbar ist. % ist der Modulo-Operator und gibt den Rest einer Division zurück.

function istGerade(zahl) {
  return <Bedingung>;
}

istGerade(4);
    `,
    correct_answer: 'true'
  },
  {
    id: 9,
    exampleCode: `// Erstelle eine Variable "alter" und prüfe, ob die Person volljährig ist.

// Erstelle hier die Variable "alter" und setze sie auf einen Wert.
// Eine Varbiable wird mit "let" oder "const" erstellt und bekommt einen Wert zugewiesen.


alter >= 18; // >= bedeutet "größer gleich" und prüft, ob die Zahl größer oder gleich 18 ist.
    `,
    correct_answer: 'true'
  },
  {
    id: 10,
    exampleCode: `// Erstelle eine Funktion, die einen Namen entgegennimmt 
// und "Hallo <Name>" zurückgibt.

function begruessen(name) {
  return <Ergebnis>; // Hier muss "Hallo <Name>" zurückgegeben werden.
}

begruessen("Anna");
    `,
    correct_answer: '"Hallo Anna"'
  },
  {
    id: 11,
    exampleCode: `// Erstelle eine Funktion, die ein Array von Zahlen annimmt und die Summe zurückgibt.
// Tipp: Um ein Array aufzusummieren, kann <array>.reduce() verwendet werden. Schaue hier nach, wie das funktioniert: https://www.w3schools.com/jsref/jsref_reduce.asp

function summe(zahlen) {
  return <Ergebnis>; // Hier muss die Summe der Zahlen zurückgegeben werden. 
}

summe([1, 2, 3]);
    `,
    correct_answer: '6'
  },
  {
    id: 12,
    exampleCode: `// Ändere die Zahl an der zweiten Stelle des Arrays in 42.

const zahlen = [10, 20, 30];

// Wie in Aufgabe 5 beschrieben, beginnt ein Array bei 0 zu zählen. Das bedeutet, dass die zweite Stelle die Position 1 hat.
zahlen[1] = <Neue Zahl>;

zahlen;
    `,
    correct_answer: '10,42,30'
  },
  {
    id: 13,
    exampleCode: `// Erstelle eine Funktion, die das Quadrat einer Zahl berechnet.

// Das Quadrat einer Zahl ist das Ergebnis der Formel: zahl^2.
function quadrat(zahl) {
  return <Ergebnis>;
}

quadrat(4);
    `,
    correct_answer: '16'
  },
  {
    id: 14,
    exampleCode: `// Erstelle eine Bedingung, die überprüft, ob eine Zahl positiv ist.

// In JavaScript gibt es den Datentyp "Boolean", der entweder "true" oder "false" sein kann.
// Dieser Datentyp wird oft verwendet, um Bedingungen zu überprüfen. (z.B. ob eine Zahl positiv ist)
function isPositive(zahl){
  return <Ergebnis>;
}

isPositive(${Math.floor(Math.random() * 10)})
    `,
    correct_answer: 'true'
  },
  {
    id: 15,
    exampleCode: `// Füge das Wort "JS" ans Ende des Arrays hinzu.

const sprachen = ["HTML", "CSS"];

// Füge hier das Wort "JS" ans Ende des Arrays hinzu.


sprachen;
    `,
    correct_answer: 'HTML,CSS,JS'
  },
  {
    id: 16,
    exampleCode: `// Entferne das letzte Element aus dem Array.
// Tipp: Es gibt eine Funktion, die das letzte Element aus einem Array entfernt. Schaue hier nach, wie das funktioniert: https://www.w3schools.com/jsref/jsref_pop.asp

const zahlen = [1, 2, 3, 4];

// Hier musst du das letzte Element aus dem Array entfernen. Dazu musst du die Funktion pop() auf das Array anwenden.

zahlen;
    `,
    correct_answer: '1,2,3'
  },
  {
    id: 17,
    exampleCode: `// Rechner die differenz zweier Werte aus

function getDifference(a, b) {
    return Math.abs(a - b);
}

// Beschreibe hier in einem Kommentar kurz was "Math" sein könnte.
// Kommentare sind Texte, die nicht ausgeführt werden. Sie sind dazu da, um den Code zu erklären. 
// Einen Kommentar kann man mit "//" beginnen.

getDifference(3, 16);
    `,
    correct_answer: '13'
  },
  {
    id: 18,
    exampleCode: `// Erstelle eine Funktion, die das längste Wort in einem Array findet.
// Tipp: Um die Länge eines Wortes zu bestimmen, kann wort.length verwendet werden.

// Hier musst du das längste Wort in einem Array finden. Dazu musst du die Länge jedes Wortes bestimmen und das längste Wort zurückgeben.
function <Funktionsname>(<Parameter>) { // Ein Parameter ist ein Wert, der einer Funktion übergeben wird. In diesem Fall ist der Parameter ["Apfel", "Banane", "Kirsche"].
  return <Ergebnis>;
}

laengstesWort(["Apfel", "Banane", "Kirsche"]);
    `,
    correct_answer: 'Kirsche'
  },
  {
    id: 19,
    exampleCode: `// Erstelle eine Funktion, die überprüft, ob ein Wort mit "A" beginnt.

// Mache daraus eine Funktion namens "startetMit", die zwei Parameter annimmt: ein Wort und einen Buchstaben.
// Denk daran, es kann auch klein geschrieben sein! Bei JavaScript ist es wichtig, dass Groß- und Kleinschreibung beachtet wird.
// Tipp: Gross-/Kleinschreibung kann man mit toLowerCase() oder toUpperCase() ändern. Schaue hier nach, wie das funktioniert: https://www.w3schools.com/jsref/jsref_tolowercase.asp
function startetMitA(wort) {
  return wort[0] === "A";
}

startetMitA("Apfel");
    `,
    correct_answer: 'true'
  },
  {
    id: 20,
    exampleCode: `// Erstelle eine Funktion, die die ersten Buchstaben eines Namens großschreibt.
// Tipp: Der erste Buchstabe des Namens kann mit name[0] angesprochen werden.

// Mache daraus eine Funktion namens "kapitalisieren", die einen Namen annimmt und den ersten Buchstaben großschreibt.
function <Funktionsname>(<Parameter>) {
  return <Ergebnis>;
}

kapitalisieren("anna");
    `,
    correct_answer: 'Anna'
  }
])

const currentTask = ref(null)

onMounted(() => {
  const task = tasks.value.find((i) => i.id == route.params.id)
  currentTask.value = task ? { ...task } : null
})
</script>

<template>
  <div v-if="currentTask != null" class="bg-white w-full h-full p-5 rounded-lg shadow-md">
    <Editor :task="currentTask" :next-url="`/task/${currentTask.id + 1}`" />
  </div>
  <div v-else-if="currentTask === null" class="min-h-screen flex flex-col items-center">
    <!-- Header -->
    <Header />

    <!-- Content Wrapper -->
    <div
      class="relative min-w-96 max-w-full md:max-w-[80%] lg:max-w-[50%] bg-white rounded-xl shadow-xl p-8 mt-12 md:mt-6 text-center"
    >
      <p class="text-gray-800 text-2xl font-bold leading-relaxed">
        Glückwunsch! 
      </p>
      <p class="text-gray-800 text-2xl leading-relaxed">
        Du hasst alle Aufgaben erledigt!
      </p>

      <!-- Button Section -->
      <button
        @click="$router.push('/')"
        class="mt-6 bg-blue-600 hover:bg-blue-700 text-white font-semibold py-3 px-6 rounded-lg flex items-center shadow-md transition-all mx-auto"
      >
        <svg
          class="w-6 h-6 mr-2"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M5 13l4 4L19 7"
          ></path>
        </svg>
        Weiter
      </button>
    </div>
  </div>
  <div v-else class="flex items-center justify-center h-screen">
    <div class="border-gray-300 h-20 w-20 animate-spin rounded-full border-8 border-t-blue-600" />
  </div>
</template>
