# 🎯 Vue.js & Nuxt — Questions d'Entretien (FR)

> La référence francophone pour préparer vos entretiens techniques **Vue.js 3** et **Nuxt.js** — des fondamentaux jusqu'aux sujets avancés, avec réponses claires et exemples de code.

<p align="center">
  <img alt="Vue.js" src="https://img.shields.io/badge/Vue.js-3.x-42b883?logo=vue.js&logoColor=white">
  <img alt="Nuxt" src="https://img.shields.io/badge/Nuxt-3.x-00DC82?logo=nuxt.js&logoColor=white">
  <img alt="Pinia" src="https://img.shields.io/badge/Pinia-2.x-ffd859?logo=pinia&logoColor=black">
  <img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-5.x-3178c6?logo=typescript&logoColor=white">
  <img alt="Langue" src="https://img.shields.io/badge/Langue-Fran%C3%A7ais-blue">
  <img alt="Questions" src="https://img.shields.io/badge/Questions-90%2B-orange">
  <img alt="Niveau" src="https://img.shields.io/badge/Niveau-D%C3%A9butant%20%E2%86%92%20Avanc%C3%A9-red">
  <img alt="PRs Welcome" src="https://img.shields.io/badge/PRs-bienvenues-brightgreen">
  <img alt="Licence" src="https://img.shields.io/badge/Licence-MIT-yellow">
</p>

---

## 📖 À propos

Ce dépôt rassemble **plus de 90 questions d'entretien Vue.js 3 & Nuxt** fréquemment posées, organisées par thème et par niveau de difficulté. Chaque question est accompagnée d'une **réponse concise**, d'**exemples de code** et, quand c'est utile, d'un **conseil pratique** pour l'entretien.

Que vous soyez **junior**, **mid-level** ou **senior**, ce guide vous aide à :

- 🧠 Réviser efficacement les concepts clés de Vue 3 et Nuxt 3
- 💬 Préparer des réponses claires et structurées
- 💻 Anticiper les exercices de **coding en direct**
- 🚀 Gagner en confiance avant le jour J

> 💡 **Astuce** : ne mémorisez pas mot pour mot. Comprenez la logique, puis reformulez avec vos propres mots — c'est ce que les recruteurs recherchent.

---

## 🗂️ Table des matières

| # | Section | Sujets | Questions |
|---|---------|--------|:---------:|
| 1 | [Fondamentaux](#1--fondamentaux) | DOM virtuel, directives, cycle de vie, réactivité | 12 |
| 2 | [Composants](#2--composants) | Props, emit, slots, provide/inject, Teleport | 12 |
| 3 | [Composition API](#3--composition-api) | `ref`, `reactive`, `computed`, `watch`, composables | 12 |
| 4 | [Gestion d'état](#4--gestion-détat-pinia--vuex) | Pinia, Vuex, stores, actions, getters | 8 |
| 5 | [Vue Router](#5--vue-router) | Gardes, routes dynamiques, lazy loading | 8 |
| 6 | [Performance](#6--optimisation-des-performances) | `v-memo`, listes longues, fuites mémoire | 6 |
| 7 | [Sujets avancés Vue](#7--sujets-avancés-vue) | Suspense, SSR, authentification, TypeScript | 7 |
| 8 | [Nuxt.js](#8--nuxtjs) | Rendu, routing, composables, modules, déploiement | 18 |
| 9 | [Coding en direct](#9--coding-en-direct--comment-réussir) | Méthodologie + tâches courantes | — |
| 10 | [Ressources](#-ressources-utiles) | Documentation et liens | — |

**Légende des niveaux** : 🟢 Débutant · 🟡 Moyen · 🔴 Avancé

---

## 1. 🧩 Fondamentaux

<details>
<summary><b>Q1 — Qu'est-ce que Vue.js et qu'est-ce qui le distingue de React et Angular ? 🟢</b></summary>

Vue.js est un framework JavaScript **progressif** pour créer des interfaces utilisateur. Contrairement à Angular (très opinionated, TypeScript obligatoire) et React (nécessite JSX, courbe d'apprentissage plus raide), Vue peut être intégré **progressivement** dans n'importe quel projet. Il utilise une syntaxe de template proche du HTML, dispose d'un système de réactivité puissant, et propose la Composition API depuis Vue 3.

> 💬 **En entretien** : mettez en avant le mot « progressif » et la facilité d'intégration dans des projets existants.
</details>

<details>
<summary><b>Q2 — Qu'est-ce que le DOM virtuel et comment Vue l'utilise-t-il ? 🟢</b></summary>

Le DOM virtuel est une **copie JavaScript légère** du vrai DOM. Quand les données changent, Vue recrée un nouvel arbre virtuel, le compare avec l'ancien (algorithme de *diffing*), et applique uniquement les modifications nécessaires au vrai DOM. Cela évite des re-rendus complets et coûteux. Vue 3 va plus loin : il marque les nœuds statiques à la compilation pour les ignorer lors du diffing.

> 💬 Réponse simple : « Vue met à jour uniquement ce qui a changé, pas toute la page. »
</details>

<details>
<summary><b>Q3 — Expliquez les principales directives : v-if, v-show, v-for, v-bind, v-on, v-model. 🟢</b></summary>

- **`v-if`** : crée/supprime l'élément du DOM selon la condition
- **`v-show`** : bascule la visibilité CSS (l'élément reste dans le DOM)
- **`v-for`** : boucle sur un tableau ou objet
- **`v-bind` (`:`)** : lie un attribut à une valeur dynamique
- **`v-on` (`@`)** : écoute les événements DOM
- **`v-model`** : liaison bidirectionnelle (combine `:value` et `@input`)

**Règle** : `v-show` si l'état bascule souvent, `v-if` si la condition change rarement.

```vue
<input v-model="nom" />
<!-- équivalent à : -->
<input :value="nom" @input="nom = $event.target.value" />
```
</details>

<details>
<summary><b>Q4 — Quels sont les hooks du cycle de vie et quand les utiliser ? 🟢</b></summary>

- **Création** : `beforeCreate`, `created` (données prêtes, pas de DOM — idéal pour les appels API)
- **Montage** : `beforeMount`, `mounted` (DOM prêt — manipulation DOM, libs tierces)
- **Mise à jour** : `beforeUpdate`, `updated`
- **Destruction** : `beforeUnmount`, `unmounted` (nettoyage : écouteurs, timers)

En Composition API : `onMounted`, `onUnmounted`, `onUpdated`, etc.

> 💬 Réponse clé : « `mounted` pour accéder au DOM, `unmounted` pour nettoyer. »
</details>

<details>
<summary><b>Q5 — Différence entre une propriété calculée (computed) et une méthode ? 🟢</b></summary>

Les **propriétés calculées** sont **mises en cache** selon leurs dépendances réactives — elles ne se recalculent que si une dépendance change. Les **méthodes** s'exécutent à chaque re-rendu du template. Utilisez `computed` pour des données dérivées, les méthodes pour des actions.

```js
computed: {
  nomComplet() { return this.prenom + ' ' + this.nom } // mis en cache
},
methods: {
  getNomComplet() { return this.prenom + ' ' + this.nom } // recalculé à chaque rendu
}
```
</details>

<details>
<summary><b>Q6 — Différence entre watch et watchEffect ? 🟡</b></summary>

- **`watch`** : surveille explicitement une source, donne l'ancienne et la nouvelle valeur, paresseux par défaut
- **`watchEffect`** : détecte automatiquement les dépendances, s'exécute immédiatement, pas d'accès à l'ancienne valeur

```js
// watch
watch(compteur, (nouvelleVal, ancienneVal) => {
  console.log(nouvelleVal, ancienneVal)
})

// watchEffect — s'exécute immédiatement
watchEffect(() => { console.log(compteur.value) })
```
</details>

<details>
<summary><b>Q7 — Comment fonctionne v-model en interne ? 🟡</b></summary>

`v-model` est du **sucre syntaxique** pour la liaison bidirectionnelle. Sur un input natif : lie `:value` et écoute `@input`. Sur un composant : lie la prop `:modelValue` et écoute `@update:modelValue`. Vue 3 permet plusieurs `v-model` : `v-model:titre`, `v-model:contenu`.

```vue
<!-- Parent -->
<MonInput v-model="nom" />

<!-- Enfant -->
<script setup>
const props = defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue'])
</script>
```
</details>

<details>
<summary><b>Q8 — Pourquoi l'attribut :key est-il important dans v-for ? 🟢</b></summary>

`key` donne à Vue une **identité unique** pour chaque élément, permettant à l'algorithme de diffing d'identifier ce qui a changé, été ajouté ou supprimé. Sans `key`, Vue peut produire des rendus incorrects (surtout avec des composants à état ou des champs de formulaire). Les clés doivent être **uniques et stables**.

> ⚠️ Erreur courante : utiliser l'index du tableau comme clé. Utilisez un **ID unique** venant des données.
</details>

<details>
<summary><b>Q9 — Comment fonctionne la réactivité ? Différence Vue 2 vs Vue 3 ? 🟡</b></summary>

- **Vue 2** : utilisait `Object.defineProperty()` — impossible de détecter l'ajout de propriétés ou les mutations d'index de tableaux (nécessitait `Vue.set()`)
- **Vue 3** : utilise **`Proxy`**, qui intercepte toutes les opérations (ajouts, suppressions, mutations de tableaux) sans méthodes spéciales. Plus complet, plus rapide, plus simple.
</details>

<details>
<summary><b>Q10 — Qu'est-ce qu'une directive personnalisée et quand l'utiliser ? 🟡</b></summary>

Les directives personnalisées appliquent un **comportement DOM de bas niveau** directement sur des éléments. Hooks : `created`, `mounted`, `updated`, `unmounted`. Cas d'usage : focus automatique, détection de clic extérieur, lazy loading d'images, masques de saisie.

```js
app.directive('focus', {
  mounted(el) { el.focus() }
})
// <input v-focus />
```

> 💬 Montrez que vous savez quand **ne pas** les utiliser : préférez les composants pour tout ce qui a un état.
</details>

<details>
<summary><b>Q11 — Quelle est la différence entre Options API et Composition API ? 🟢</b></summary>

- **Options API** : organisation par *type* d'option (`data`, `methods`, `computed`, `watch`). Plus accessible pour les débutants, mais la logique d'une même fonctionnalité est dispersée.
- **Composition API** : organisation par *fonctionnalité*. Tout au même endroit, réutilisable via des composables, meilleur support TypeScript.

> 💬 Les deux coexistent dans Vue 3. Pour les nouveaux projets, privilégiez la Composition API.
</details>

<details>
<summary><b>Q12 — Qu'est-ce que nextTick() et quand l'utiliser ? 🟡</b></summary>

`nextTick()` retarde l'exécution d'un callback jusqu'après la **prochaine mise à jour du DOM**. Utile quand vous modifiez des données et avez besoin d'accéder immédiatement au DOM mis à jour (ex. : calculer la hauteur d'un élément après ajout de contenu).

```js
import { nextTick } from 'vue'

async function ajouterItem() {
  liste.value.push(nouvelItem)
  await nextTick()
  // Le DOM est maintenant à jour
  conteneurRef.value.scrollTop = conteneurRef.value.scrollHeight
}
```
</details>

---

## 2. 🧱 Composants

<details>
<summary><b>Q13 — Qu'est-ce que les props et comment les valider ? 🟢</b></summary>

Les **props** passent des données du parent vers l'enfant. Elles sont en **lecture seule** — ne les mutez jamais directement. Validation : `type`, `required`, `default`, `validator`.

```js
const props = defineProps({
  titre: { type: String, required: true },
  compteur: { type: Number, default: 0 },
  statut: { validator: val => ['actif', 'inactif'].includes(val) }
})
```
</details>

<details>
<summary><b>Q14 — Communication entre composants : « props vers le bas, événements vers le haut » ? 🟢</b></summary>

Le parent transmet des données à l'enfant via les **props**. L'enfant communique en retour via **`$emit`**. Pour les composants frères : remontez l'état vers le parent commun, ou utilisez un store (Pinia) / `provide`-`inject`.

```js
// Enfant émet
const emit = defineEmits(['soumettre'])
emit('soumettre', donnees)

// Parent écoute
// <MonFormulaire @soumettre="gererSoumission" />
```
</details>

<details>
<summary><b>Q15 — Slots vs slots avec portée (scoped slots) ? 🟡</b></summary>

Un **slot** est un emplacement dans l'enfant rempli par le parent (compilé dans la portée du parent). Un **slot avec portée** permet à l'enfant d'exposer des données vers le template parent. Slots → composants de mise en page (cartes, modales). Slots avec portée → quand l'enfant a des données que le parent doit afficher.

```vue
<!-- Enfant -->
<slot :element="elementCourant">Contenu par défaut</slot>

<!-- Parent -->
<MaListe v-slot="{ element }">
  <span>{{ element.nom }}</span>
</MaListe>
```
</details>

<details>
<summary><b>Q16 — Qu'est-ce que provide/inject et quand l'utiliser ? 🟡</b></summary>

Système d'**injection de dépendances** pour passer des données en profondeur sans *prop drilling*. Un ancêtre `provide`, n'importe quel descendant `inject`. Utilisations : thème, i18n, config, état d'authentification.

```js
// Ancêtre
import { provide, ref } from 'vue'
const theme = ref('sombre')
provide('theme', theme)

// Descendant
const theme = inject('theme')
```

> 💡 Rendez la valeur réactive (`ref`/`reactive`) pour que les consommateurs réagissent aux changements.
</details>

<details>
<summary><b>Q17 — Mixins vs composables : pourquoi le changement en Vue 3 ? 🟡</b></summary>

Les **mixins** fusionnent des options dans un composant. Problèmes : conflits de noms, source peu claire, couplage implicite. Les **composables** (fonctions Composition API) sont **explicites, bien délimités et faciles à tester** — ils résolvent tous ces problèmes.
</details>

<details>
<summary><b>Q18 — defineEmits et validation des événements émis ? 🟡</b></summary>

`defineEmits` déclare les événements émis et permet le typage TypeScript + la validation à l'exécution.

```js
const emit = defineEmits({
  soumettre: (payload) => typeof payload.email === 'string',
  annuler: null // pas de validation
})
```
</details>

<details>
<summary><b>Q19 — Composants asynchrones et lazy loading ? 🟡</b></summary>

Les composants asynchrones se chargent **à la demande**, réduisant le bundle initial. Utilisez `defineAsyncComponent()` avec composants de chargement/erreur.

```js
import { defineAsyncComponent } from 'vue'

const GrosGraphique = defineAsyncComponent({
  loader: () => import('./GrosGraphique.vue'),
  loadingComponent: Chargement,
  errorComponent: ErreurMsg,
  delay: 200
})
```
</details>

<details>
<summary><b>Q20 — Différence entre v-if et keep-alive ? 🟡</b></summary>

`v-if` **détruit/recrée** complètement le composant. `keep-alive` **met en cache** son état quand il devient inactif (reste en mémoire). Utilisez `keep-alive` pour les onglets/pages où vous voulez préserver l'état des formulaires.

```vue
<keep-alive :include="['ProfilUtilisateur', 'Parametres']">
  <component :is="ongletCourant" />
</keep-alive>
```
</details>

<details>
<summary><b>Q21 — Qu'est-ce que Teleport et quand l'utiliser ? 🔴</b></summary>

`Teleport` rend le template **ailleurs dans le DOM** tout en le gardant logiquement dans l'arbre Vue. Usage typique : modales, infobulles, notifications rendues au niveau du `body` pour éviter les problèmes de `z-index` / `overflow: hidden`.

```vue
<Teleport to="body">
  <div class="modal" v-if="afficherModal">…</div>
</Teleport>
```
</details>

<details>
<summary><b>Q22 — Qu'est-ce que defineExpose et pourquoi est-il nécessaire ? 🔴</b></summary>

En `script setup`, l'état interne est **privé par défaut** — les parents ne peuvent pas y accéder via `$refs`. `defineExpose` expose explicitement une **API propre**.

```js
// Enfant
const compteur = ref(0)
function reinitialiser() { compteur.value = 0 }
defineExpose({ reinitialiser })

// Parent : enfantRef.value.reinitialiser()
```
</details>

<details>
<summary><b>Q23 — Qu'est-ce que les composants dynamiques (`<component :is>`) ? 🟡</b></summary>

Permet de **switcher dynamiquement** entre des composants en passant un composant (ou son nom) à l'attribut `is`. Très utile pour les onglets, les wizards, ou les rendus conditionnels complexes.

```vue
<script setup>
import PageProfil from './PageProfil.vue'
import PageParametres from './PageParametres.vue'

const onglets = { profil: PageProfil, parametres: PageParametres }
const ongletActif = ref('profil')
</script>

<template>
  <component :is="onglets[ongletActif]" />
</template>
```
</details>

<details>
<summary><b>Q24 — Comment implémenter un composant d'ordre supérieur (HOC) en Vue 3 ? 🔴</b></summary>

En Vue 3, les **composables** remplacent avantageusement les HOC. Mais si vous avez besoin d'un wrapper de composant (ex. : logging, error boundary), utilisez un composant fonctionnel qui accepte et transmet les props/slots.

```vue
<!-- WithLogging.vue -->
<script setup>
const props = defineProps(['component'])
onMounted(() => console.log('Monté:', props.component.__name))
</script>
<template>
  <component :is="props.component" v-bind="$attrs">
    <template v-for="(_, name) in $slots" #[name]="slotData">
      <slot :name="name" v-bind="slotData || {}" />
    </template>
  </component>
</template>
```

> 💬 Mentionnez toujours que les composables sont la solution privilégiée en Vue 3.
</details>

---

## 3. ⚡ Composition API

<details>
<summary><b>Q25 — Qu'est-ce que la Composition API et pourquoi a-t-elle été introduite ? 🟢</b></summary>

Un ensemble de fonctions (`ref`, `reactive`, `computed`, `watch`, hooks) permettant d'organiser la logique **par fonctionnalité** et non par type d'option. Avant Vue 3, le code d'une fonctionnalité était dispersé entre `data`, `methods`, `computed`, `watch`. Elle permet aussi les **composables** (logique réutilisable).

> 💬 Argument clé : réutilisation de la logique sans mixins + meilleur support TypeScript.
</details>

<details>
<summary><b>Q26 — Différence entre ref() et reactive() ? 🟢</b></summary>

- **`ref()`** : enveloppe une valeur unique (primitive ou objet), accès via `.value`
- **`reactive()`** : Proxy réactif profond d'un objet, pas de `.value`, mais la destructuration perd la réactivité (utilisez `toRefs()`)

> 💡 Préférez `ref()` pour tout — plus prévisible et composable.

```js
const compteur = ref(0)        // .value
const etat = reactive({ x: 0 }) // etat.x
const { x } = toRefs(etat)     // destructuration sûre
```
</details>

<details>
<summary><b>Q27 — Comment fonctionne computed() dans la Composition API ? 🟢</b></summary>

Retourne une **ref réactive en lecture seule** dérivée d'autres sources, **mise en cache**. Possibilité de `get` + `set`.

```js
const nomComplet = computed({
  get: () => `${prenom.value} ${nom.value}`,
  set: (val) => { [prenom.value, nom.value] = val.split(' ') }
})
```
</details>

<details>
<summary><b>Q28 — Comment faire un appel API dans setup() avec gestion chargement/erreur ? 🟢</b></summary>

Utilisez une fonction `async` dans `onMounted` ou un composable. Ne rendez jamais `setup()` lui-même `async` (sauf avec Suspense).

```js
const utilisateurs = ref([])
const chargement = ref(false)
const erreur = ref(null)

onMounted(async () => {
  chargement.value = true
  try {
    const res = await fetch('/api/utilisateurs')
    utilisateurs.value = await res.json()
  } catch (e) {
    erreur.value = e.message
  } finally {
    chargement.value = false
  }
})
```
</details>

<details>
<summary><b>Q29 — Qu'est-ce qu'un composable et comment en écrire un ? 🟡 ⭐</b></summary>

Une fonction qui utilise la Composition API pour **encapsuler et réutiliser de la logique avec état** (convention `useX`). L'équivalent des hooks React.

```js
// useFetch.js
export function useFetch(url) {
  const data = ref(null)
  const chargement = ref(true)
  const erreur = ref(null)

  fetch(url)
    .then(r => r.json())
    .then(d => { data.value = d })
    .catch(e => { erreur.value = e })
    .finally(() => { chargement.value = false })

  return { data, chargement, erreur }
}

// Utilisation
const { data, chargement } = useFetch('/api/articles')
```

> ⭐ **Question de coding en direct la plus fréquente.** Entraînez-vous à écrire `useFetch` de mémoire.
</details>

<details>
<summary><b>Q30 — Comment surveiller des objets imbriqués avec watch() ? 🟡</b></summary>

Ajoutez `{ deep: true }` pour les changements imbriqués, `{ immediate: true }` pour exécuter au démarrage.

```js
watch(() => utilisateur.adresse.ville, (nouvelleVille) => {
  console.log('Ville changée :', nouvelleVille)
})

watch(formulaire, (val) => sauvegarder(val), { deep: true })
```
</details>

<details>
<summary><b>Q31 — Qu'est-ce que toRefs() et quand en a-t-on besoin ? 🟡</b></summary>

Convertit chaque propriété d'un objet `reactive` en **ref individuelle**, préservant la réactivité lors de la destructuration.

```js
const etat = reactive({ x: 0, y: 0 })
const { x, y } = etat          // ❌ perd la réactivité
const { x, y } = toRefs(etat)  // ✅ x.value, y.value réactifs
```
</details>

<details>
<summary><b>Q32 — Hooks de cycle de vie dans la Composition API ? 🟢</b></summary>

`mounted` → `onMounted` · `updated` → `onUpdated` · `unmounted` → `onUnmounted` · `beforeMount` → `onBeforeMount` · `errorCaptured` → `onErrorCaptured`. `beforeCreate`/`created` → utilisez `setup()` directement.
</details>

<details>
<summary><b>Q33 — watchEffect() vs watch() ? 🟡</b></summary>

`watchEffect` **auto-détecte** les dépendances et s'exécute immédiatement (pas d'ancienne valeur). `watch` est **explicite** et donne les valeurs ancienne/nouvelle. `watchEffect` → chaînes de dépendances complexes. `watch` → contrôle précis.
</details>

<details>
<summary><b>Q34 — Qu'est-ce que script setup et ses avantages ? 🟢</b></summary>

Sucre syntaxique réduisant le code répétitif : imports et variables auto-exposés au template, pas de `return {}`, macros `defineProps`/`defineEmits`/`defineExpose` disponibles automatiquement, meilleure inférence TypeScript.

```vue
<script setup>
import { ref } from 'vue'
import MonBouton from './MonBouton.vue' // auto-enregistré
const compteur = ref(0) // auto-exposé
</script>
```
</details>

<details>
<summary><b>Q35 — Qu'est-ce que `effectScope()` et quand l'utiliser ? 🔴</b></summary>

`effectScope()` crée une **portée isolée** pour regrouper des effets réactifs (`computed`, `watch`, `watchEffect`) afin de les arrêter tous d'un seul coup. Indispensable dans les composables avancés ou les plugins Vue.

```js
import { effectScope, ref, watch } from 'vue'

const scope = effectScope()

scope.run(() => {
  const count = ref(0)
  watch(count, (val) => console.log(val))
})

// Plus tard : stoppe tous les effets de la portée
scope.stop()
```

> 💬 Utilisé en interne par Pinia. Montre une compréhension avancée du système réactif.
</details>

<details>
<summary><b>Q36 — Comment partager de l'état entre des composables sans store ? 🔴</b></summary>

Créez une instance réactive **au niveau module** (hors de la fonction composable). Tous les appelants partagent alors la même référence.

```js
// useTheme.js
import { ref } from 'vue'

// État partagé au niveau du module
const themeActuel = ref('clair')

export function useTheme() {
  function basculerTheme() {
    themeActuel.value = themeActuel.value === 'clair' ? 'sombre' : 'clair'
  }
  return { themeActuel, basculerTheme }
}
```

> ⚠️ Attention : cet état persiste entre les rendus côté serveur (SSR). Préférez Pinia pour les apps Nuxt.
</details>

---

## 4. 🗃️ Gestion d'état (Pinia & Vuex)

<details>
<summary><b>Q37 — Qu'est-ce que Pinia et en quoi diffère-t-il de Vuex ? 🟡</b></summary>

**Pinia** = librairie officielle pour Vue 3. **Pas de mutations** (modifications directes), stores **plats**, compatible TypeScript et Composition API, bundle léger. Vuex : `state`/`getters`/`mutations`(sync)/`actions`(async). Pinia : `state`/`getters`/`actions`(sync + async). **En 2026, Pinia est le standard.**

> 💬 « Je préfère Pinia pour Vue 3 — moins de code, meilleure DX, recommandation officielle. »
</details>

<details>
<summary><b>Q38 — Comment définir un store Pinia ? 🟡</b></summary>

```js
// Syntaxe Setup (recommandée)
export const useStoreUtilisateur = defineStore('utilisateur', () => {
  const nom = ref('')
  const estConnecte = computed(() => nom.value !== '')

  async function connexion(identifiants) {
    const data = await api.login(identifiants)
    nom.value = data.nom
  }

  return { nom, estConnecte, connexion }
})
```
</details>

<details>
<summary><b>Q39 — Comment accéder à l'état Pinia dans un composant ? 🟡</b></summary>

Utilisez `storeToRefs()` pour destructurer l'état **en gardant la réactivité**. Les actions se destructurent directement.

```js
import { storeToRefs } from 'pinia'
const store = useStoreUtilisateur()
const { nom, estConnecte } = storeToRefs(store) // réactif
const { connexion } = store // action — OK
```
</details>

<details>
<summary><b>Q40 — Store vs état local vs provide/inject : quand utiliser quoi ? 🟡</b></summary>

- **État local** (`ref`/`reactive`) : un seul composant
- **provide/inject** : sous-arbre de composants (thème, config)
- **Store** (Pinia) : composants non reliés, async complexe, cache, auth, panier

> Règle : commencez local, remontez si nécessaire, store uniquement pour l'état **vraiment global**.
</details>

<details>
<summary><b>Q41 — Comment fonctionne Vuex (state, getters, mutations, actions) ? 🟡</b></summary>

**State** : source unique. **Getters** : propriétés calculées. **Mutations** : changements **synchrones** (seule façon de modifier l'état). **Actions** : async, committent des mutations. Flux : `dispatch(action)` → `commit(mutation)` → changement d'état. Pinia supprime les mutations.
</details>

<details>
<summary><b>Q42 — Comment gérer les mises à jour optimistes ? 🔴</b></summary>

Mettez à jour l'état **immédiatement**, puis synchronisez. En cas d'échec, **annulez**.

```js
async function basculerJaime(id) {
  article.jaime = !article.jaime // optimiste
  try {
    await api.basculerJaime(id)
  } catch {
    article.jaime = !article.jaime // annulation
  }
}
```
</details>

<details>
<summary><b>Q43 — Comment persister un store Pinia après rechargement ? 🔴</b></summary>

Utilisez `pinia-plugin-persistedstate` qui sérialise l'état dans `localStorage`/`sessionStorage` et le réhydrate au chargement.

```js
export const useStoreAuth = defineStore('auth', () => {
  const token = ref('')
  return { token }
}, { persist: true })
```
</details>

<details>
<summary><b>Q44 — Comment tester un store Pinia ? 🔴</b></summary>

Créez une instance Pinia propre par test avec `createPinia()`. Vous pouvez directement modifier l'état et tester les actions.

```js
import { setActivePinia, createPinia } from 'pinia'
import { useStoreUtilisateur } from './storeUtilisateur'

beforeEach(() => setActivePinia(createPinia()))

test('connexion met à jour le nom', async () => {
  const store = useStoreUtilisateur()
  await store.connexion({ email: 'a@b.com', mdp: '1234' })
  expect(store.nom).toBe('Alice')
})
```
</details>

---

## 5. 🧭 Vue Router

<details>
<summary><b>Q45 — Que sont les gardes de navigation et comment protéger une route ? 🟡</b></summary>

Elles **interceptent** les changements de route. Global : `router.beforeEach`. Par route : `beforeEnter`. Composant : `onBeforeRouteLeave`.

```js
router.beforeEach((to, from, next) => {
  const auth = useStoreAuth()
  if (to.meta.requiresAuth && !auth.estConnecte) next({ name: 'Connexion' })
  else next()
})
```
</details>

<details>
<summary><b>Q46 — Routes dynamiques et paramètres de route ? 🟢</b></summary>

Segments avec `:`. Accès via `useRoute()`. Utilisez `props: true` pour passer les params comme props.

```js
{ path: '/utilisateur/:id', component: ProfilUtilisateur, props: true }
const route = useRoute() // route.params.id
```
</details>

<details>
<summary><b>Q47 — Comment lazy-loader les routes ? 🟡</b></summary>

Imports dynamiques → Vite/Webpack crée un chunk par route.

```js
const routes = [
  { path: '/tableau-de-bord', component: () => import('./vues/TableauDeBord.vue') }
]
```
</details>

<details>
<summary><b>Q48 — router.push() vs router.replace() ? 🟢</b></summary>

`push()` ajoute une entrée d'historique (retour possible). `replace()` remplace l'entrée courante (pas de retour). Utilisez `replace()` pour les redirections après connexion.
</details>

<details>
<summary><b>Q49 — Routes imbriquées : comment les implémenter ? 🟡</b></summary>

Le parent doit avoir un `<router-view />`. Définissez `children`.

```js
{
  path: '/parametres',
  component: ParametresLayout,
  children: [
    { path: 'profil', component: ParametresProfil },
    { path: '', redirect: 'profil' }
  ]
}
```
</details>

<details>
<summary><b>Q50 — Comment faire défiler vers le haut lors de la navigation ? 🟢</b></summary>

```js
const router = createRouter({
  history: createWebHistory(),
  routes,
  scrollBehavior(to, from, savedPosition) {
    return savedPosition || { top: 0 }
  }
})
```
</details>

<details>
<summary><b>Q51 — Différence entre `createWebHistory` et `createWebHashHistory` ? 🟡</b></summary>

- **`createWebHistory`** : URLs propres (`/utilisateurs/1`). Nécessite une configuration serveur pour rediriger toutes les routes vers `index.html`.
- **`createWebHashHistory`** : URLs avec `#` (`/#/utilisateurs/1`). Fonctionne sans config serveur, mais moins propre pour le SEO.

> 💬 Utilisez `createWebHistory` en production avec Nuxt/Nginx/Vercel configuré. Le `#` c'est pour les prototypes rapides.
</details>

<details>
<summary><b>Q52 — Qu'est-ce que les meta de route et comment les utiliser ? 🟡</b></summary>

Le champ `meta` permet d'attacher des **métadonnées arbitraires** à une route, accessibles dans les gardes de navigation et les composants via `route.meta`.

```js
const routes = [
  {
    path: '/admin',
    component: AdminPage,
    meta: { requiresAuth: true, roles: ['admin'] }
  }
]

// Dans une garde
router.beforeEach((to) => {
  if (to.meta.requiresAuth && !estConnecte.value) {
    return { name: 'Connexion' }
  }
})
```
</details>

---

## 6. 🚀 Optimisation des performances

<details>
<summary><b>Q53 — Que sont v-once et v-memo ? 🔴</b></summary>

`v-once` : rendu **une seule fois** (contenu statique). `v-memo` : mémorise un sous-arbre, re-rend seulement si le tableau de dépendances change.

```vue
<h1 v-once>{{ titreStatique }}</h1>

<div v-for="item in liste" :key="item.id"
     v-memo="[item.id, item.selectionne]">
  <ComposantLourd :item="item" />
</div>
```
</details>

<details>
<summary><b>Q54 — Comment gérer efficacement les longues listes ? 🟡</b></summary>

1. **Défilement virtuel** (`vue-virtual-scroller`) — rend uniquement les éléments visibles
2. Pagination
3. `v-memo`
4. Toujours `:key`
5. `shallowRef` pour les grands tableaux

> 💬 Exemple concret : « J'ai utilisé le défilement virtuel sur une liste de 50k+ contacts. »
</details>

<details>
<summary><b>Q55 — Qu'est-ce que le code splitting et comment Vue le gère-t-il ? 🟡</b></summary>

Divise le bundle en **chunks chargés à la demande** : lazy loading des routes, `defineAsyncComponent`, chunks automatiques Vite/Webpack. Résultat : chargement initial plus rapide.
</details>

<details>
<summary><b>Q56 — Comment éviter les fuites mémoire ? 🟡</b></summary>

Nettoyez dans `onUnmounted()` : écouteurs, timers, observers, instances tierces.

```js
onMounted(() => {
  window.addEventListener('resize', gerer)
  timer = setInterval(sonder, 5000)
})
onUnmounted(() => {
  window.removeEventListener('resize', gerer)
  clearInterval(timer)
})
```
</details>

<details>
<summary><b>Q57 — Qu'est-ce que shallowRef() et quand l'utiliser ? 🔴</b></summary>

Crée une ref qui ne suit **que `.value` au niveau racine**, pas les changements profonds. Idéal pour les grandes structures de données où la réactivité profonde est coûteuse et inutile.
</details>

<details>
<summary><b>Q58 — Comment mesurer les performances d'une app Vue ? 🔴</b></summary>

- **Vue DevTools** → onglet Performance pour visualiser les re-rendus
- **`app.config.performance = true`** → active les markers dans les DevTools navigateur
- **Lighthouse** → métriques LCP, TBT, CLS
- **`markRaw()`** : empêche Vue de rendre réactif un objet qui n'a pas besoin de l'être (ex. : instances de bibliothèques tierces comme Chart.js)

```js
import { markRaw } from 'vue'
const chart = markRaw(new Chart(ctx, config)) // non-réactif → performant
```
</details>

---

## 7. 🧠 Sujets avancés Vue

<details>
<summary><b>Q59 — Qu'est-ce que Suspense ? 🔴</b></summary>

Composant intégré gérant les **dépendances asynchrones** : affiche un fallback pendant le chargement, puis le contenu réel.

```vue
<Suspense>
  <template #default><TableauDeBordAsync /></template>
  <template #fallback><Chargement /></template>
</Suspense>
```
</details>

<details>
<summary><b>Q60 — Comment implémenter l'authentification (Vue Router + Pinia) ? 🔴 ⭐</b></summary>

Token JWT dans Pinia/cookie → garde de navigation globale → intercepteur Axios pour le token et les 401.

```js
const token = ref(localStorage.getItem('token') || '')
const estConnecte = computed(() => !!token.value)

router.beforeEach((to) => {
  if (to.meta.requiresAuth && !storeAuth.estConnecte)
    return { name: 'Connexion', query: { redirect: to.fullPath } }
})

axios.interceptors.request.use(config => {
  config.headers.Authorization = `Bearer ${token.value}`
  return config
})
```

> ⭐ Question full-stack très fréquente. Connaissez ce schéma par cœur.
</details>

<details>
<summary><b>Q61 — Comment tester un composant Vue ? 🔴</b></summary>

**Vitest** (ou Jest) + **Vue Test Utils** pour les tests unitaires de composants. **Cypress/Playwright** pour les tests E2E. **MSW** pour mocker les API au niveau réseau. Testez props, événements, interactions utilisateur.

```js
import { mount } from '@vue/test-utils'
import MonBouton from './MonBouton.vue'

test('émet "clic" quand on clique', async () => {
  const wrapper = mount(MonBouton, { props: { label: 'OK' } })
  await wrapper.trigger('click')
  expect(wrapper.emitted('clic')).toBeTruthy()
})
```
</details>

<details>
<summary><b>Q62 — Qu'est-ce que le SSR et pourquoi l'utiliser (Nuxt) ? 🔴</b></summary>

Le **SSR** (rendu côté serveur) pré-rend les pages sur le serveur → meilleur SEO et premier affichage plus rapide. L'**hydratation** attache l'app cliente au HTML serveur. **Nuxt** gère routing, hydratation et logique serveur automatiquement.
</details>

<details>
<summary><b>Q63 — Comment typer un composant avec TypeScript ? 🔴</b></summary>

```ts
// Props typées
const props = defineProps<{ titre: string; compteur?: number }>()

// Emits typés
const emit = defineEmits<{
  (e: 'soumettre', payload: { email: string }): void
}>()
```
</details>

<details>
<summary><b>Q64 — Qu'est-ce que `onErrorCaptured` et comment gérer les erreurs globalement ? 🔴</b></summary>

`onErrorCaptured` intercepte les erreurs des composants descendants. Pour une gestion globale, utilisez `app.config.errorHandler`.

```js
// Composant parent (Error Boundary)
onErrorCaptured((err, instance, info) => {
  erreur.value = err.message
  return false // empêche la propagation
})

// Global
app.config.errorHandler = (err, instance, info) => {
  monServiceAnalytics.captureException(err)
}
```
</details>

<details>
<summary><b>Q65 — Qu'est-ce que `defineModel()` en Vue 3.4+ ? 🟡</b></summary>

`defineModel()` est une macro qui simplifie la création de composants compatibles `v-model`. Elle crée automatiquement la prop et l'event correspondants.

```vue
<!-- Avant Vue 3.4 -->
<script setup>
const props = defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue'])
</script>

<!-- Avec defineModel (Vue 3.4+) -->
<script setup>
const modele = defineModel() // prop + emit auto
</script>
<template>
  <input v-model="modele" />
</template>
```
</details>

---

## 8. 🟢 Nuxt.js

> Nuxt 3 est le meta-framework Vue officiel. Il ajoute SSR, routing automatique, composables auto-importés et bien plus.

<details>
<summary><b>Q66 — Qu'est-ce que Nuxt.js et pourquoi l'utiliser plutôt que Vue seul ? 🟢</b></summary>

Nuxt est un **meta-framework** basé sur Vue qui apporte :

- 🗂️ **Routing basé sur le système de fichiers** (pas de config manuelle)
- 🖥️ **SSR / SSG / ISR / SPA** selon la page
- 📦 **Auto-imports** (composants, composables, utils — sans `import`)
- 🔌 **Modules** (image, i18n, auth, PWA…)
- 🚀 **Performance** : optimisation d'images, lazy loading, prefetch automatique
- 🛠️ **API Routes** intégrées (Nitro)

> 💬 Nuxt = Vue + configuration optimisée + conventions + server. Choisissez-le dès que vous avez besoin de SEO ou d'un fullstack léger.
</details>

<details>
<summary><b>Q67 — Comment fonctionne le routing basé sur fichiers dans Nuxt ? 🟢</b></summary>

Nuxt génère les routes automatiquement depuis le dossier `pages/`. Le nom du fichier devient l'URL.

```
pages/
├── index.vue          → /
├── about.vue          → /about
├── blog/
│   ├── index.vue      → /blog
│   └── [slug].vue     → /blog/:slug
├── [...404].vue       → route catch-all
└── [[optionnel]].vue  → paramètre optionnel
```

> 💡 Les crochets `[param]` → dynamique. Double crochet `[[param]]` → optionnel. `[...slug]` → catch-all.
</details>

<details>
<summary><b>Q68 — Quels sont les modes de rendu dans Nuxt 3 ? 🟡</b></summary>

Nuxt supporte plusieurs modes configurables **par route** :

| Mode | Config | Cas d'usage |
|------|--------|-------------|
| **SSR** (défaut) | `ssr: true` | SEO, contenu dynamique |
| **SPA** | `ssr: false` | Dashboard privé, app admin |
| **SSG** | `nuxt generate` | Blog, docs, contenu statique |
| **ISR** | `routeRules: { '/blog/**': { isr: 60 } }` | Contenu semi-statique |
| **Hybrid** | `routeRules` par route | Mix selon les besoins |

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  routeRules: {
    '/': { prerender: true },
    '/blog/**': { isr: 3600 },
    '/admin/**': { ssr: false }
  }
})
```
</details>

<details>
<summary><b>Q69 — Qu'est-ce que useFetch et useAsyncData dans Nuxt ? 🟡 ⭐</b></summary>

Ce sont les **composables de data-fetching** de Nuxt. Ils s'exécutent **côté serveur ET côté client**, évitent les doubles requêtes (hydratation correcte) et exposent état de chargement et d'erreur.

```vue
<script setup>
// useFetch — raccourci pour les appels HTTP
const { data: articles, pending, error } = await useFetch('/api/articles')

// useAsyncData — pour de la logique async plus complexe
const { data: utilisateur } = await useAsyncData('user', () =>
  $fetch(`/api/users/${route.params.id}`)
)
</script>
```

**Différence clé** : `useFetch('/url')` ≈ `useAsyncData(key, () => $fetch('/url'))`. Utilisez `useAsyncData` quand vous avez besoin d'une clé personnalisée ou d'une logique non-HTTP.

> ⭐ Très fréquent en entretien Nuxt. Comprenez la déduplication via la clé.
</details>

<details>
<summary><b>Q70 — Qu'est-ce que les auto-imports dans Nuxt ? 🟢</b></summary>

Nuxt importe automatiquement (sans `import { ref } from 'vue'`) :
- Tous les composables Vue (`ref`, `computed`, `watch`…)
- Vos composables dans `composables/`
- Vos utils dans `utils/`
- Vos composants dans `components/`

```vue
<!-- ✅ Fonctionne sans import explicite -->
<script setup>
const compteur = ref(0) // auto-importé depuis Vue
const { data } = useFetch('/api') // auto-importé depuis Nuxt
</script>
```

> ⚠️ Les auto-imports peuvent surprendre. Activez le support IDE via `@nuxt/devtools` ou le fichier `.nuxt/types/`.
</details>

<details>
<summary><b>Q71 — Comment créer des API Routes avec Nuxt (Nitro) ? 🟡</b></summary>

Les fichiers dans `server/api/` deviennent des **endpoints HTTP** gérés par Nitro (le serveur de Nuxt).

```ts
// server/api/utilisateurs/[id].get.ts
export default defineEventHandler(async (event) => {
  const id = getRouterParam(event, 'id')
  const body = await readBody(event) // pour POST

  const utilisateur = await db.users.findById(id)
  if (!utilisateur) throw createError({ statusCode: 404, message: 'Introuvable' })

  return utilisateur
})
```

Accès côté client :
```js
const { data } = await useFetch('/api/utilisateurs/42')
```

> 💡 Nuxt détecte automatiquement la méthode HTTP via le suffixe : `.get.ts`, `.post.ts`, `.delete.ts`.
</details>

<details>
<summary><b>Q72 — Qu'est-ce que les middleware Nuxt et comment les utiliser ? 🟡</b></summary>

Les **middleware de route** s'exécutent avant la navigation. Il en existe trois types :

```ts
// middleware/auth.ts — nommé, déclaré dans la page
export default defineNuxtRouteMiddleware((to, from) => {
  const { estConnecte } = useStoreAuth()
  if (!estConnecte.value) return navigateTo('/connexion')
})

// middleware/global.global.ts — suffixe .global = s'applique à toutes les routes
```

```vue
<!-- Dans une page -->
<script setup>
definePageMeta({ middleware: ['auth'] })
</script>
```

Types : **inline** (défini dans la page), **nommé** (fichier dans `middleware/`), **global** (suffixe `.global.ts`).
</details>

<details>
<summary><b>Q73 — Comment gérer les layouts dans Nuxt ? 🟢</b></summary>

Les layouts sont dans `layouts/`. Le layout par défaut est `layouts/default.vue`. Chaque page peut en choisir un différent.

```vue
<!-- layouts/admin.vue -->
<template>
  <div>
    <BarreLatéraleAdmin />
    <main><slot /></main>
  </div>
</template>
```

```vue
<!-- pages/admin/tableau-de-bord.vue -->
<script setup>
definePageMeta({ layout: 'admin' })
</script>
```

> 💡 `<NuxtLayout>` dans `app.vue` rend le layout actif. Vous pouvez changer de layout dynamiquement avec `setPageLayout('admin')`.
</details>

<details>
<summary><b>Q74 — Différence entre plugins et modules Nuxt ? 🟡</b></summary>

- **Plugin** (`plugins/`) : code exécuté au démarrage de l'app Vue. Sert à enregistrer des composants globaux, injecter des helpers, configurer des librairies tierces.
- **Module** (`modules/` ou npm) : étend la **configuration Nuxt** elle-même (Nitro, Vite, webpack, hooks de build). Plus puissant, utilisé pour `@nuxtjs/image`, `@nuxtjs/i18n`, etc.

```ts
// plugins/toast.client.ts — ".client" = client uniquement
export default defineNuxtPlugin((nuxtApp) => {
  nuxtApp.provide('toast', (msg: string) => alert(msg))
})

// Utilisation : const { $toast } = useNuxtApp()
```
</details>

<details>
<summary><b>Q75 — Qu'est-ce que useState dans Nuxt et quand l'utiliser ? 🟡</b></summary>

`useState` est un composable Nuxt qui crée un état **réactif partagé entre le serveur et le client**, évitant les désynchronisations d'hydratation. Alternative légère à Pinia pour de l'état simple.

```ts
// composables/useCompteur.ts
export const useCompteur = () => useState<number>('compteur', () => 0)

// Dans n'importe quelle page/composant
const compteur = useCompteur()
compteur.value++ // partagé entre toutes les instances
```

> ⚠️ `useState` persiste pendant toute la session SSR. Pour de l'état utilisateur complexe (auth, panier), préférez Pinia + `pinia-plugin-persistedstate`.
</details>

<details>
<summary><b>Q76 — Comment fonctionne l'hydratation dans Nuxt et qu'est-ce qu'une erreur d'hydratation ? 🔴</b></summary>

L'**hydratation** est le processus par lequel Vue "reprend" le HTML statique généré côté serveur et y attache la réactivité cliente. Une **erreur d'hydratation** survient quand le HTML serveur ne correspond pas au HTML généré par le client.

**Causes fréquentes** :
- Utilisation de `Date.now()`, `Math.random()`, ou variables navigateur (`window`, `localStorage`) directement dans le template
- Différences de timezone ou de locale entre serveur et client

**Solutions** :

```vue
<!-- ✅ Utiliser ClientOnly pour le contenu spécifique au client -->
<ClientOnly>
  <MaCartePrix :prix="prixLocalisé" />
</ClientOnly>

<!-- ✅ Ou le composable useHydration -->
<script setup>
const afficher = ref(false)
onMounted(() => { afficher.value = true })
</script>
```
</details>

<details>
<summary><b>Q77 — Comment optimiser les images avec Nuxt Image ? 🟡</b></summary>

`@nuxt/image` optimise automatiquement les images : conversion WebP/AVIF, redimensionnement, lazy loading, CDN.

```bash
npx nuxi@latest module add image
```

```vue
<NuxtImg
  src="/photo.jpg"
  width="800"
  height="600"
  format="webp"
  loading="lazy"
  sizes="100vw sm:50vw md:400px"
/>
```

> 💡 `<NuxtPicture>` génère automatiquement les sources `<picture>` pour le format adaptatif.
</details>

<details>
<summary><b>Q78 — Comment gérer le SEO dans Nuxt ? 🟡</b></summary>

Utilisez `useHead()` ou `useSeoMeta()` pour les balises `<head>` dynamiques. Configurez les défauts dans `nuxt.config.ts`.

```vue
<script setup>
useSeoMeta({
  title: () => `${article.value.titre} | Mon Blog`,
  description: article.value.extrait,
  ogImage: article.value.imageCover,
  twitterCard: 'summary_large_image'
})
</script>
```

```ts
// nuxt.config.ts — défauts globaux
export default defineNuxtConfig({
  app: {
    head: {
      htmlAttrs: { lang: 'fr' },
      meta: [{ name: 'theme-color', content: '#42b883' }]
    }
  }
})
```
</details>

<details>
<summary><b>Q79 — Comment déployer une app Nuxt en production ? 🔴</b></summary>

Nuxt peut être déployé dans plusieurs modes grâce à **Nitro** :

| Cible | Commande | Hôtes |
|-------|----------|-------|
| **Node.js** (SSR) | `nuxt build` + `node .output/server/index.mjs` | VPS, Railway, Render |
| **Edge / Serverless** | `NITRO_PRESET=vercel nuxt build` | Vercel, Netlify, Cloudflare |
| **Statique** (SSG) | `nuxt generate` | GitHub Pages, Netlify, S3 |
| **Docker** | `nuxt build` + Dockerfile | Toute infra conteneurisée |

```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY .output .output
ENV PORT=3000
CMD ["node", ".output/server/index.mjs"]
```

> 💬 En entretien, mentionnez que Nuxt détecte automatiquement la plateforme (Vercel, Netlify) via `NITRO_PRESET`.
</details>

<details>
<summary><b>Q80 — Qu'est-ce que `definePageMeta()` et quelles options accepte-t-il ? 🟡</b></summary>

`definePageMeta()` est une macro Nuxt pour configurer les métadonnées d'une page au moment de la compilation.

```vue
<script setup>
definePageMeta({
  layout: 'admin',                  // layout à utiliser
  middleware: ['auth', 'role-admin'], // middleware à exécuter
  keepalive: true,                  // garde le composant en cache
  pageTransition: { name: 'slide' }, // transition de page
  validate: async (route) => {      // validation de route
    return /^\d+$/.test(route.params.id as string)
  }
})
</script>
```
</details>

<details>
<summary><b>Q81 — Comment gérer les erreurs dans Nuxt ? 🔴</b></summary>

Nuxt offre plusieurs niveaux de gestion d'erreur :

```vue
<!-- error.vue — page d'erreur globale -->
<script setup>
const props = defineProps(['error'])
const gererErreur = () => clearError({ redirect: '/' })
</script>
<template>
  <h1>{{ error.statusCode }} — {{ error.message }}</h1>
  <button @click="gererErreur">Retour à l'accueil</button>
</template>
```

```ts
// Dans une page ou API route
throw createError({
  statusCode: 404,
  statusMessage: 'Article introuvable',
  fatal: true // affiche error.vue immédiatement
})
```

```vue
<!-- NuxtErrorBoundary — erreurs localisées -->
<NuxtErrorBoundary @error="logErreur">
  <template #error="{ error, clearError }">
    <p>Erreur : {{ error.message }}</p>
    <button @click="clearError()">Réessayer</button>
  </template>
  <ComposantRisque />
</NuxtErrorBoundary>
```
</details>

<details>
<summary><b>Q82 — Qu'est-ce que `$fetch` et en quoi diffère-t-il de `fetch` natif ? 🟡</b></summary>

`$fetch` est un utilitaire Nuxt basé sur [ofetch](https://github.com/unjs/ofetch) qui :
- **Parse automatiquement** la réponse JSON
- **Gère les erreurs** en lançant des exceptions claires
- **Fonctionne côté serveur** (résout les URLs relatives correctement)
- **Déduplique** les requêtes dans un contexte SSR

```ts
// Avec fetch natif
const res = await fetch('/api/articles')
const data = await res.json()

// Avec $fetch — plus simple et isomorphe
const data = await $fetch('/api/articles')
const user = await $fetch<User>('/api/users/1', {
  method: 'POST',
  body: { nom: 'Alice' }
})
```

> ⚠️ Dans les composants, préférez `useFetch`/`useAsyncData` (gèrent le cache et la déduplication SSR). Utilisez `$fetch` directement dans les handlers d'événements ou les actions Pinia.
</details>

<details>
<summary><b>Q83 — Comment implémenter l'internationalisation (i18n) dans Nuxt ? 🟡</b></summary>

Utilisez le module `@nuxtjs/i18n` (basé sur vue-i18n) :

```bash
npx nuxi@latest module add i18n
```

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  i18n: {
    locales: [
      { code: 'fr', file: 'fr.json' },
      { code: 'ar', file: 'ar.json', dir: 'rtl' }
    ],
    defaultLocale: 'fr',
    lazy: true,
    strategy: 'prefix_except_default'
  }
})
```

```vue
<script setup>
const { t, locale } = useI18n()
</script>
<template>
  <h1>{{ t('accueil.titre') }}</h1>
</template>
```
</details>

---

## 9. 💻 Coding en direct — comment réussir

| Principe | Détail |
|----------|--------|
| 🗣️ **Pensez à voix haute** | « Je vais créer un composable qui gère la logique du fetch… » — montrez votre raisonnement, pas seulement le résultat. |
| 🏗️ **Commencez par la structure** | Définissez props, emits, état et retour avant de coder. 30 s de planification = 5 min économisées. |
| ⚠️ **Gérez les cas limites** | Chargement ? Erreur ? Liste vide ? Mentionnez-les même sans tout coder. |
| 🏷️ **Nommez clairement** | `estEnChargement` plutôt que `c`, `listeUtilisateurs` plutôt que `data`. |
| 🤝 **Si vous bloquez, dites-le** | « Je ne me souviens pas exactement de la syntaxe, mais la logique serait… » L'honnêteté > le silence. |

### 🎯 Tâches les plus probables

**Vue.js**
1. Écrire un composable `useFetch(url)` avec état chargement/erreur
2. Créer un composant parent-enfant avec `v-model` personnalisé (`modelValue` + `emit`)
3. Construire un store Pinia simple (todo list ou panier)
4. Ajouter une garde de navigation pour protéger une route
5. Implémenter une liste filtrée avec `computed` + liaison d'input

**Nuxt.js**
6. Créer une API route `GET /api/articles` retournant des données mockées
7. Fetcher des données côté serveur avec `useFetch` et gérer les états
8. Configurer un middleware d'authentification pour une section `/admin`
9. Implémenter un layout différent pour les pages admin
10. Configurer le SEO d'une page avec `useSeoMeta`

---

## 📚 Ressources utiles

**Vue.js**
- 📘 [Documentation officielle Vue.js (FR)](https://fr.vuejs.org/)
- 🍍 [Documentation Pinia](https://pinia.vuejs.org/)
- 🧭 [Documentation Vue Router](https://router.vuejs.org/)
- 🧪 [Vue Test Utils](https://test-utils.vuejs.org/)
- ⚡ [Vite](https://vitejs.dev/)

**Nuxt.js**
- 🟢 [Documentation Nuxt 3](https://nuxt.com/docs)
- 🧩 [Modules Nuxt](https://nuxt.com/modules)
- 🚀 [Nitro (serveur Nuxt)](https://nitro.unjs.io/)
- 🖼️ [Nuxt Image](https://image.nuxt.com/)
- 🌍 [Nuxt i18n](https://i18n.nuxtjs.org/)

**Outils**
- 🔍 [Vue DevTools](https://devtools.vuejs.org/)
- 📦 [Nuxt DevTools](https://devtools.nuxt.com/)

---

## 🤝 Contribuer

Les contributions sont **les bienvenues** ! Pour ajouter ou améliorer une question :

1. **Forkez** le dépôt
2. Créez une branche : `git checkout -b ajout-question`
3. Ajoutez votre question en respectant le format (question + réponse + exemple + niveau)
4. Ouvrez une **Pull Request** avec une description claire

> Merci de garder un ton pédagogique et des exemples concis et corrects.

---

## ⭐ Soutenir le projet

Si ce dépôt vous a aidé, **laissez une étoile** ⭐ — ça aide d'autres développeurs francophones à le trouver !

---

## 📄 Licence

Distribué sous licence **MIT**. Voir le fichier `LICENSE` pour plus de détails.

---

<p align="center">
  <i>Bonne chance pour vos entretiens ! 🚀</i>
</p>