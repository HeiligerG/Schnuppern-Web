<template>
  <div class="app-shell">
    <header class="hero-section">
      <div class="hero-copy">
        <p class="eyebrow">Schnuppern im Beruf Applikationsentwicklung</p>
        <h1>Willkommen bei deiner Profil-Mission</h1>
        <p class="hero-text">
          Diese App führt dich Schritt für Schritt: zuerst mit kleinen Aufgaben direkt auf der Website,
          später mit zwei letzten Challenges im Code.
        </p>
        <div class="hero-labels">
          <span>Einfach</span>
          <span>Modern</span>
          <span>Motivierend</span>
        </div>
      </div>
      <div class="hero-card">
        <strong>Deine Mission</strong>
        <p>
          Löse die ersten Aufgaben direkt hier auf der Seite als kleine Code-Rätsel. Wähle die richtige Zeile und teste,
          wie sich das Profil verändert. Am Ende kannst du zwei Dinge direkt im Code verbessern.
        </p>
      </div>
    </header>

    <section class="content-grid">
      <section class="profile-preview section-card">
        <div class="profile-top">
          <div class="avatar">{{ profile.name ? profile.name.charAt(0).toUpperCase() : 'A' }}</div>
          <div>
            <p class="small-label">Name</p>
            <h2>{{ profile.name }}</h2>
            <p class="subtitle">{{ profile.title }}</p>
          </div>
        </div>

        <p class="greeting">{{ profile.greeting }}</p>

        <div class="hobby-box">
          <p class="small-label">Hobbys</p>
          <ul>
            <li v-for="(hobby, index) in profile.hobbies" :key="index">{{ hobby }}</li>
          </ul>
        </div>

        <button class="action-button" type="button">{{ profile.buttonText }}</button>

        <div class="fun-fact">
          <span>Fun Fact</span>
          <p>{{ profile.funFact }}</p>
        </div>
      </section>

      <section class="challenge-panel section-card">
        <h2>Deine Challenges</h2>
        <p class="panel-intro">
          Diese Aufgaben sind kleine Coding-Rätsel: Wähle die richtige Code-Zeile aus und sieh,
          wie dein Profil direkt auf die Lösung reagiert.
        </p>

        <div class="challenge-list">
          <article class="challenge-card" v-for="challenge in uiChallenges" :key="challenge.id">
            <div class="challenge-header">
              <strong>{{ challenge.id }}. {{ challenge.title }}</strong>
              <span>{{ challengeStatus(challenge) }}</span>
            </div>
            <p>{{ challenge.description }}</p>
            <pre class="code-snippet" v-if="challenge.snippet">{{ challenge.snippet }}</pre>

            <div class="challenge-input">
              <p class="small-label">{{ challenge.label }}</p>
              <div class="choice-buttons">
                <button
                  v-for="option in challenge.options"
                  :key="option.label"
                  type="button"
                  :class="['option-button', { active: challenge.solved && option.correct } ]"
                  @click="solveUiChallenge(challenge, option)">
                  <code>{{ option.label }}</code>
                </button>
              </div>
            </div>
            <p v-if="challenge.feedback" class="feedback">{{ challenge.feedback }}</p>
          </article>
        </div>

        <div class="progress-panel">
          <p>Erledigte Aufgaben: {{ completedCount }} / {{ uiChallenges.length }}</p>
          <progress :value="completedCount" :max="uiChallenges.length"></progress>
        </div>
      </section>
    </section>

    <section class="code-challenge section-card">
      <h2>Code-Challenges</h2>
      <p>
        Jetzt löst du zwei Coding-Aufgaben direkt im virtuellen Editor. Schreibe oder ergänze den Code und klicke auf "Teste Code".
      </p>
      <div class="code-list">
        <article class="code-card" v-for="challenge in codeChallenges" :key="challenge.id">
          <div class="challenge-header">
            <strong>{{ challenge.id }}. {{ challenge.title }}</strong>
            <span>{{ codeStatus(challenge) }}</span>
          </div>
          <p>{{ challenge.description }}</p>
          <textarea class="code-editor" v-model="challenge.code" rows="10"></textarea>
          <div class="editor-actions">
            <button type="button" @click="applyChallengeCode(challenge)">Teste Code</button>
            <span class="hint">{{ challenge.hint }}</span>
          </div>
          <p v-if="challenge.feedback" class="feedback">{{ challenge.feedback }}</p>
        </article>
      </div>
    </section>
  </div>
</template>

<script>
import { reactive, computed, ref, watch } from 'vue'

export default {
  setup() {
    const profile = reactive({
      name: 'Alex',
      title: 'Schnupperlernende/r Applikationsentwicklung',
      greeting: 'Hi! Ich bin Alex und entdecke gerade die Welt der Web-Apps.',
      hobbies: ['Zeichnen', 'Fussball', 'Musik'],
      buttonText: 'Mehr über mich',
      funFact: 'Ich finde es spannend, wie Webseiten auf Klick reagieren.',
      accent: '#5c7cfa'
    })

    const uiChallenges = [
      {
        id: 1,
        title: 'Name im Code setzen',
        description: 'Finde die richtige Code-Zeile, die den Namen auf der Profilkarte ändert.',
        snippet: `// Setze den Namen im Profil\n// Wähle den richtigen Code`,
        label: 'Richtige Code-Zeile',
        solved: false,
        feedback: '',
        options: [
          { label: "profile.name = 'Lena';", correct: true, result: { field: 'name', value: 'Lena' } },
          { label: "profile.name == 'Lena';", correct: false },
          { label: "profile.name === 'Lena';", correct: false }
        ]
      },
      {
        id: 2,
        title: 'Titel im Code festlegen',
        description: 'Wähle die richtige Zeile, die den Profil-Titel ändert.',
        snippet: `// Setze den Titel im Profil\n// Wähle den richtigen Code`,
        label: 'Richtige Code-Zeile',
        solved: false,
        feedback: '',
        options: [
          { label: "profile.title = 'Web-Entdecker*in';", correct: true, result: { field: 'title', value: 'Web-Entdecker*in' } },
          { label: "profile.title == 'Web-Entdecker*in';", correct: false },
          { label: "profile.title += 'Web-Entdecker*in';", correct: false }
        ]
      },
      {
        id: 3,
        title: 'Begrüssung per Code',
        description: 'Wähle den richtigen Code, damit die Begrüssung in der App angezeigt wird.',
        snippet: `// Ändere den Begrüssungstext\n// Wähle den richtigen Code`,
        label: 'Richtige Code-Zeile',
        solved: false,
        feedback: '',
        options: [
          { label: "profile.greeting = 'Hi! Ich entdecke Web-Apps.';", correct: true, result: { field: 'greeting', value: 'Hi! Ich entdecke Web-Apps.' } },
          { label: "profile.greeting += 'Hi! Ich entdecke Web-Apps.';", correct: false },
          { label: "profile.greeting == 'Hi! Ich entdecke Web-Apps.';", correct: false }
        ]
      },
      {
        id: 4,
        title: 'Hobby per Code hinzufügen',
        description: 'Finde den korrekten Code, um ein Hobby zur Liste hinzuzufügen.',
        snippet: `// Füge ein neues Hobby zur Liste hinzu\n// Wähle den richtigen Code`,
        label: 'Richtige Code-Zeile',
        solved: false,
        feedback: '',
        options: [
          { label: "profile.hobbies.push('Gamen');", correct: true, result: { field: 'hobbies', value: 'Gamen' } },
          { label: "profile.hobbies[0] = 'Gamen';", correct: false },
          { label: "profile.hobbies.pop('Gamen');", correct: false }
        ]
      },
      {
        id: 5,
        title: 'Accent-Farbe per Code ändern',
        description: 'Wähle die richtige Code-Zeile, die die Accent-Farbe der Seite setzt.',
        snippet: `// Ändere die Farbe der Seite\n// Wähle den richtigen Code`,
        label: 'Richtige Code-Zeile',
        solved: false,
        feedback: '',
        options: [
          { label: "profile.accent = '#37b24d';", correct: true, result: { field: 'accent', value: '#37b24d' } },
          { label: "profile.accent = 'grün';", correct: false },
          { label: "setAccent('#37b24d');", correct: false }
        ]
      },
      {
        id: 6,
        title: 'Profiltext per Code',
        description: 'Wähle die richtige Code-Zeile, die Button-Text und Fun Fact zusammen ändert.',
        snippet: `// Ändere Text und Fun Fact\n// Wähle den richtigen Code`,
        label: 'Richtige Code-Zeile',
        solved: false,
        feedback: '',
        options: [
          { label: "profile.buttonText = 'Mehr erfahren'; profile.funFact = 'Ich mag Code-Rätsel.';", correct: true, result: { field: 'both', values: { buttonText: 'Mehr erfahren', funFact: 'Ich mag Code-Rätsel.' } } },
          { label: "profile.buttonText += 'Mehr erfahren';", correct: false },
          { label: "profile.funFact == 'Ich mag Code-Rätsel.';", correct: false }
        ]
      }
    ]

    const dynamicCss = ref('')
    const codeChallenges = reactive([
      {
        id: 7,
        title: 'Button-Hover verbessern',
        description: 'Bearbeite den CSS-Code im Editor und ergänze einen Hover-Effekt für den Button.',
        starterCode: `.action-button {
  width: fit-content;
  padding: 14px 22px;
  border: none;
  border-radius: 999px;
  background: var(--accent);
  color: white;
  cursor: pointer;
}

/* TODO: Ergänze hier den Hover-Effekt für den Button */`,
        code: '',
        solved: false,
        feedback: '',
        hint: 'Tipp: Schreibe eine Regel für .action-button:hover und nutze z. B. box-shadow oder background.'
      },
      {
        id: 8,
        title: 'Layout-Abstände verbessern',
        description: 'Verbessere den Code, damit die Karten mehr Platz und eine freundlichere Optik bekommen.',
        starterCode: `.section-card {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid var(--border);
  border-radius: 24px;
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 18px;
}

/* TODO: Mache die Karten noch gemütlicher mit mehr Abstand oder Schatten */`,
        code: '',
        solved: false,
        feedback: '',
        hint: 'Tipp: Ergänze padding, gap oder box-shadow, damit die Karten leicht und aufgeräumt wirken.'
      }
    ])

    codeChallenges.forEach((item) => {
      item.code = item.starterCode
    })

    const styleElement = document.getElementById('challenge-dynamic-style') || document.head.appendChild(document.createElement('style'))
    styleElement.id = 'challenge-dynamic-style'

    watch(dynamicCss, (value) => {
      styleElement.textContent = value
    })

    const applyChallengeCode = (challenge) => {
      dynamicCss.value = challenge.code
      if (challenge.id === 7) {
        const hoverPresent = /\.action-button\s*:\s*hover/.test(challenge.code)
        const effectPresent = /box-shadow|background|transform/.test(challenge.code)
        challenge.solved = hoverPresent && effectPresent
        challenge.feedback = challenge.solved
          ? 'Gut gemacht! Der Hover-Effekt ist jetzt in deinem Code.'
          : 'Der Hover-Effekt fehlt noch. Ergänze .action-button:hover und einen Stil.'
      }
      if (challenge.id === 8) {
        const sectionCardUpdated = /\.section-card/.test(challenge.code)
        const spacingAdded = /padding|gap|box-shadow/.test(challenge.code)
        challenge.solved = sectionCardUpdated && spacingAdded
        challenge.feedback = challenge.solved
          ? 'Super! Die Layout-Regel ist angepasst.'
          : 'Noch nicht ganz. Ergänze padding, gap oder box-shadow für .section-card.'
      }
    }

    const solveUiChallenge = (challenge, option) => {
      if (!option.correct) {
        challenge.feedback = 'Nicht ganz. Versuch es noch einmal.'
        return
      }

      challenge.solved = true
      challenge.feedback = 'Richtig! Der Code wurde übernommen.'

      if (option.result) {
        if (option.result.field === 'both') {
          Object.assign(profile, option.result.values)
        } else if (option.result.field === 'hobbies') {
          if (!profile.hobbies.includes(option.result.value)) {
            profile.hobbies.push(option.result.value)
          }
        } else {
          profile[option.result.field] = option.result.value
          if (option.result.field === 'accent') {
            document.documentElement.style.setProperty('--accent', option.result.value)
          }
        }
      }
    }

    const addHobby = (hobby) => {
      if (!profile.hobbies.includes(hobby)) {
        profile.hobbies.push(hobby)
      }
    }

    const challengeComplete = (challenge) => {
      return challenge.solved === true
    }

    const challengeStatus = (challenge) => {
      return challengeComplete(challenge) ? 'Erledigt' : 'Offen'
    }

    const completedCount = computed(() => {
      return uiChallenges.filter((challenge) => challengeComplete(challenge)).length
    })

    return {
      profile,
      uiChallenges,
      codeChallenges,
      applyChallengeCode,
      challengeStatus,
      codeStatus,
      completedCount
    }
  }
}
</script>
