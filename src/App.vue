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
          Löse die ersten Aufgaben direkt hier auf der Seite. Wähle aus mehreren Antworten und teste,
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
          Diese Aufgaben sind jetzt deine Mission: Entscheide dich für Optionen und achte darauf,
          wie dein Profil reagiert.
        </p>

        <div class="challenge-list">
          <article class="challenge-card" v-for="challenge in uiChallenges" :key="challenge.id">
            <div class="challenge-header">
              <strong>{{ challenge.id }}. {{ challenge.title }}</strong>
              <span>{{ challengeStatus(challenge) }}</span>
            </div>
            <p>{{ challenge.description }}</p>

            <div class="challenge-input" v-if="challenge.type === 'choices'">
              <p class="small-label">{{ challenge.label }}</p>
              <div class="choice-buttons">
                <button
                  v-for="option in challenge.options"
                  :key="option.label"
                  type="button"
                  :class="['option-button', { active: isOptionActive(challenge, option) } ]"
                  @click="applyOption(challenge, option)">
                  {{ option.label }}
                </button>
              </div>
            </div>

            <div class="challenge-input" v-if="challenge.type === 'hobby'">
              <p class="small-label">{{ challenge.label }}</p>
              <div class="choice-buttons">
                <button
                  v-for="option in challenge.options"
                  :key="option.label"
                  type="button"
                  class="option-button"
                  @click="addHobby(option.value)">
                  {{ option.label }}
                </button>
              </div>
            </div>

            <div class="challenge-input" v-if="challenge.type === 'funfact'">
              <p class="small-label">Button-Text auswählen</p>
              <div class="choice-buttons">
                <button
                  v-for="option in challenge.buttonOptions"
                  :key="option.label"
                  type="button"
                  :class="['option-button', { active: profile.buttonText === option.value } ]"
                  @click="applyOption(challenge, option)">
                  {{ option.label }}
                </button>
              </div>

              <p class="small-label">Fun Fact auswählen</p>
              <div class="choice-buttons">
                <button
                  v-for="option in challenge.funFactOptions"
                  :key="option.label"
                  type="button"
                  :class="['option-button', { active: profile.funFact === option.value } ]"
                  @click="applyOption(challenge, option)">
                  {{ option.label }}
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
        Jetzt geht es in den Code. Zwei sichtbare Dinge sind noch nicht fertig: der Hauptbutton braucht
        einen Hover-Effekt und das Layout darf etwas luftiger werden.
      </p>
      <div class="code-list">
        <article class="code-card">
          <h3>7. Button-Hover verbessern</h3>
          <p>
            Öffne <code>src/styles.css</code> und ergänze einen Hover-Effekt für den Hauptbutton.
            So fühlt sich die Seite lebendiger an.
          </p>
          <p class="hint">Tipp: Schatten, leichte Bewegung oder andere Farbakzente helfen.</p>
        </article>
        <article class="code-card">
          <h3>8. Layout-Abstände verbessern</h3>
          <p>
            Öffne <code>src/styles.css</code> und mach die Karte oder die Abstände etwas angenehmer.
            Das Profil und die Challenge-Box sollen nicht zu dicht aussehen.
          </p>
          <p class="hint">Tipp: Passe Padding, Gap oder Kartengrössen an.</p>
        </article>
      </div>
    </section>
  </div>
</template>

<script>
import { reactive, computed } from 'vue'

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
        title: 'Name anpassen',
        description: 'Wähle einen neuen Profilnamen aus. Jeder Name verändert das Profil direkt.',
        type: 'choices',
        label: 'Name wechseln',
        field: 'name',
        options: [
          { label: 'Lena', value: 'Lena' },
          { label: 'Noah', value: 'Noah' },
          { label: 'Mia', value: 'Mia' }
        ]
      },
      {
        id: 2,
        title: 'Titel ändern',
        description: 'Wähle einen neuen Titel für dein Profil aus.',
        type: 'choices',
        label: 'Passender Titel',
        field: 'title',
        options: [
          { label: 'Web-Entdecker*in', value: 'Web-Entdecker*in' },
          { label: 'App-Entdecker*in', value: 'App-Entdecker*in' },
          { label: 'Code-Neugierige*r', value: 'Code-Neugierige*r' }
        ]
      },
      {
        id: 3,
        title: 'Gruss-Text wählen',
        description: 'Wähle einen Begrüssungstext aus, der gut zu dir passt.',
        type: 'choices',
        label: 'Begrüssungsstil',
        field: 'greeting',
        options: [
          { label: 'Hallo! Ich entdecke Web-Apps.', value: 'Hallo! Ich entdecke Web-Apps.' },
          { label: 'Hi! Ich bin neugierig auf Apps.', value: 'Hi! Ich bin neugierig auf Apps.' },
          { label: 'Guten Tag! Ich gestalte meine Seite.', value: 'Guten Tag! Ich gestalte meine Seite.' }
        ]
      },
      {
        id: 4,
        title: 'Hobby hinzufügen',
        description: 'Füge ein Hobby aus der Vorschlagsliste hinzu.',
        type: 'hobby',
        label: 'Hobby wählen',
        options: [
          { label: 'Lesen', value: 'Lesen' },
          { label: 'Gamen', value: 'Gamen' },
          { label: 'Fotografieren', value: 'Fotografieren' }
        ]
      },
      {
        id: 5,
        title: 'Akzentfarbe wählen',
        description: 'Wähle eine neue Farbe für die Seite.',
        type: 'choices',
        label: 'Farbwelt',
        field: 'accent',
        options: [
          { label: 'Blau', value: '#5c7cfa' },
          { label: 'Grün', value: '#37b24d' },
          { label: 'Lila', value: '#845ef7' }
        ]
      },
      {
        id: 6,
        title: 'Button und Fun Fact',
        description: 'Wähle einen neuen Button-Text und einen spannenden Fun Fact.',
        type: 'funfact',
        label: 'Profil lebendiger machen',
        buttonOptions: [
          { label: 'Mehr erfahren', value: 'Mehr erfahren' },
          { label: 'Lass uns starten', value: 'Lass uns starten' },
          { label: 'Profil ansehen', value: 'Profil ansehen' }
        ],
        funFactOptions: [
          { label: 'Ich mag Code-Rätsel.', value: 'Ich mag Code-Rätsel.' },
          { label: 'Ich entdecke gerne neue Apps.', value: 'Ich entdecke gerne neue Apps.' },
          { label: 'Ich programmiere noch nicht, aber ich lerne.', value: 'Ich programmiere noch nicht, aber ich lerne.' }
        ]
      }
    ]

    const applyOption = (challenge, option) => {
      if (challenge.field) {
        profile[challenge.field] = option.value
        if (challenge.field === 'accent') {
          document.documentElement.style.setProperty('--accent', option.value)
        }
      }
      if (challenge.type === 'funfact') {
        if (challenge.buttonOptions.some((item) => item.value === option.value)) {
          profile.buttonText = option.value
        }
        if (challenge.funFactOptions.some((item) => item.value === option.value)) {
          profile.funFact = option.value
        }
      }
    }

    const addHobby = (hobby) => {
      if (!profile.hobbies.includes(hobby)) {
        profile.hobbies.push(hobby)
      }
    }

    const isOptionActive = (challenge, option) => {
      if (challenge.type === 'choices') {
        return profile[challenge.field] === option.value
      }
      if (challenge.type === 'funfact') {
        return profile.buttonText === option.value || profile.funFact === option.value
      }
      return false
    }

    const challengeComplete = (challenge) => {
      if (challenge.id === 1) return profile.name !== 'Alex'
      if (challenge.id === 2) return profile.title !== 'Schnupperlernende/r Applikationsentwicklung'
      if (challenge.id === 3) return profile.greeting !== 'Hi! Ich bin Alex und entdecke gerade die Welt der Web-Apps.'
      if (challenge.id === 4) return profile.hobbies.length >= 4
      if (challenge.id === 5) return profile.accent !== '#5c7cfa'
      if (challenge.id === 6) return (
        profile.buttonText !== 'Mehr über mich' ||
        profile.funFact !== 'Ich finde es spannend, wie Webseiten auf Klick reagieren.'
      )
      return false
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
      applyOption,
      addHobby,
      isOptionActive,
      challengeStatus,
      completedCount
    }
  }
}
</script>
