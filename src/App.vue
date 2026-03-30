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
          Löse die ersten Tasks direkt in der Oberfläche. Dein Profil soll wachsen, schöner werden und am
          Ende helfen dir zwei kleine Code-Aufgaben, noch mehr Glanz reinzubringen.
        </p>
      </div>
    </header>

    <section class="content-grid">
      <section class="profile-preview section-card">
        <div class="profile-top">
          <div class="avatar">A</div>
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
          Du arbeitest direkt hier in der Seite. Jede Aufgabe verändert dein Profil sofort.
          Am Ende lernst du, wie du im Code selbst Verbesserungen machst.
        </p>

        <div class="challenge-list">
          <article class="challenge-card" v-for="challenge in uiChallenges" :key="challenge.id">
            <div class="challenge-header">
              <strong>{{ challenge.id }}. {{ challenge.title }}</strong>
              <span>{{ challengeStatus(challenge) }}</span>
            </div>
            <p>{{ challenge.description }}</p>
            <div class="challenge-input" v-if="challenge.type === 'text'">
              <label>
                {{ challenge.label }}
                <input
                  :value="challenge.value"
                  @input="updateChallenge(challenge.id, $event.target.value)"
                  type="text"
                />
              </label>
            </div>
            <div class="challenge-input" v-if="challenge.type === 'textarea'">
              <label>
                {{ challenge.label }}
                <textarea
                  :value="challenge.value"
                  @input="updateChallenge(challenge.id, $event.target.value)"
                  rows="3"
                />
              </label>
            </div>
            <div class="challenge-input" v-if="challenge.type === 'hobby'">
              <label>
                {{ challenge.label }}
                <div class="hobby-row">
                  <input v-model="newHobby" type="text" placeholder="Neues Hobby eingeben" />
                  <button type="button" @click="addHobby">Hinzufügen</button>
                </div>
              </label>
            </div>
            <div class="challenge-input" v-if="challenge.type === 'color'">
              <label>{{ challenge.label }}</label>
              <div class="color-pills">
                <button
                  v-for="scheme in colorOptions"
                  :key="scheme.name"
                  type="button"
                  :class="['color-pill', { active: profile.accent === scheme.accent } ]"
                  :style="{ background: scheme.accent }"
                  @click="setAccent(scheme.accent)">
                  {{ scheme.name }}
                </button>
              </div>
            </div>
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
        Jetzt geht es in den Code. Zwei kleine Dateien brauchen deine Hilfe. Schau dir die Hinweise an
        und öffne die Datei direkt im Editor.
      </p>
      <div class="code-list">
        <article class="code-card">
          <h3>7. Button-Hover verbessern</h3>
          <p>
            Der Button im Profil sieht noch nicht richtig interaktiv aus. Öffne <code>src/App.vue</code>
            und ergänze einen Hover-Effekt für <code>.action-button</code>.
          </p>
          <p class="hint">Tipp: ein sanfter Schatten oder Farbwechsel reicht schon.</p>
        </article>
        <article class="code-card">
          <h3>8. Profilkarten-Abstand verbessern</h3>
          <p>
            Die Profilkarte und die Challenge-Box haben einen kleinen Abstandsfaktor, der noch nicht
            gemütlich wirkt. Öffne <code>src/styles.css</code> oder <code>src/App.vue</code> und passe
            den Innenabstand oder das Layout an.</p>
          </article>
      </div>
    </section>
  </div>
</template>

<script>
import { reactive, ref, computed } from 'vue'

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

    const colorOptions = [
      { name: 'Blau', accent: '#5c7cfa' },
      { name: 'Grün', accent: '#37b24d' },
      { name: 'Lila', accent: '#845ef7' }
    ]

    const uiChallenges = [
      {
        id: 1,
        title: 'Name anpassen',
        description: 'Trage deinen eigenen Namen ein und sieh zu, wie die Karte lebendig wird.',
        type: 'text',
        label: 'Neuer Name',
        value: profile.name
      },
      {
        id: 2,
        title: 'Titel ändern',
        description: 'Gib einen eigenen Titel ein, der zeigt, was dich interessiert.',
        type: 'text',
        label: 'Neuer Titel',
        value: profile.title
      },
      {
        id: 3,
        title: 'Gruss-Text bearbeiten',
        description: 'Schreibe eine freundliche Begrüssung, die deine Persönlichkeit zeigt.',
        type: 'textarea',
        label: 'Begrüssungstext',
        value: profile.greeting
      },
      {
        id: 4,
        title: 'Hobbys ergänzen',
        description: 'Füge ein neues Hobby hinzu und erweitere deine Profilseite.',
        type: 'hobby',
        label: 'Neues Hobby',
        value: ''
      },
      {
        id: 5,
        title: 'Akzentfarbe wählen',
        description: 'Wähle ein Farbschema, das zu deiner Seite passt.',
        type: 'color',
        label: 'Akzentfarbe',
        value: profile.accent
      },
      {
        id: 6,
        title: 'Button-Text oder Fun Fact',
        description: 'Mach den Profilbutton spannender oder ergänze einen persönlichen Fun Fact.',
        type: 'text',
        label: 'Button-Text / Fun Fact',
        value: profile.buttonText
      }
    ]

    const newHobby = ref('')

    const updateChallenge = (id, value) => {
      const challenge = uiChallenges.find((item) => item.id === id)
      if (!challenge) return

      if (id === 1) profile.name = value
      if (id === 2) profile.title = value
      if (id === 3) profile.greeting = value
      if (id === 6) profile.buttonText = value
      challenge.value = value
    }

    const addHobby = () => {
      const hobby = newHobby.value.trim()
      if (hobby && !profile.hobbies.includes(hobby)) {
        profile.hobbies.push(hobby)
      }
      newHobby.value = ''
    }

    const setAccent = (accent) => {
      profile.accent = accent
      document.documentElement.style.setProperty('--accent', accent)
    }

    const challengeComplete = (challenge) => {
      if (challenge.id === 1) return profile.name.trim().length > 2
      if (challenge.id === 2) return profile.title.trim().length > 5
      if (challenge.id === 3) return profile.greeting.trim().length > 15
      if (challenge.id === 4) return profile.hobbies.length >= 4
      if (challenge.id === 5) return profile.accent !== '#5c7cfa'
      if (challenge.id === 6) return profile.buttonText.trim().length > 3 || profile.funFact.trim().length > 10
      return false
    }

    const challengeStatus = (challenge) => {
      return challengeComplete(challenge) ? 'Erledigt' : 'in Arbeit'
    }

    const completedCount = computed(() => {
      return uiChallenges.filter((challenge) => challengeComplete(challenge)).length
    })

    return {
      profile,
      uiChallenges,
      colorOptions,
      newHobby,
      addHobby,
      setAccent,
      updateChallenge,
      completedCount,
      challengeStatus
    }
  }
}
</script>
