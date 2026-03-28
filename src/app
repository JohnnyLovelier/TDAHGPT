import React, { useEffect, useMemo, useState } from "react";

const STORAGE_KEY = "diva2-fr-vercel-app-v1";

const symptomSections = [
  {
    id: "A",
    title: "Inattention",
    shortTitle: "Critère A1",
    description:
      "Les symptômes à l’âge adulte doivent être présents depuis au moins 6 mois. Les symptômes dans l’enfance se rapportent à la période entre 5 et 12 ans. Pour qu’un symptôme soit attribué au TDAH, il doit être chronique et non épisodique.",
    supplementaryLabel:
      "Parmi les symptômes attentionnels précédents, en avez-vous présenté davantage ou plus fréquemment que les autres adultes ou enfants du même âge ?",
    items: [
      {
        code: "A1",
        question:
          "Avez-vous souvent du mal à prêter attention aux détails, ou faites-vous souvent des erreurs d’étourderie dans votre travail ou dans d’autres activités ?",
        adultExamples: [
          "Fait des erreurs d’étourderie",
          "Travaille lentement pour éviter les erreurs",
          "Ne lit pas les instructions avec soin",
          "Du mal à travailler de façon minutieuse",
          "Besoin de trop de temps pour mener à leur terme des tâches complexes",
          "Facilement empêtré par les détails",
          "Travaille trop rapidement et commet ainsi des erreurs",
        ],
        childExamples: [
          "Erreurs d’étourderie lors du travail scolaire",
          "Erreurs parce qu’il ne lisait pas les questions correctement",
          "Ne répondait pas à des questions parce qu’il ne les lisait pas correctement",
          "Ne répondait pas aux questions posées au verso d’un examen",
          "Les autres faisaient remarquer que le travail n’était pas soigné",
          "Ne vérifiait pas ses réponses dans les devoirs scolaires",
          "Besoin de trop de temps pour mener à leur terme des tâches minutieuses ou comportant de nombreux détails",
        ],
      },
      {
        code: "A2",
        question: "Trouvez-vous souvent difficile de soutenir votre attention sur une tâche ?",
        adultExamples: [
          "Incapable de maintenir son attention sur des tâches pendant longtemps",
          "Facilement distrait par ses propres pensées ou associations d’idées",
          "Difficile de suivre un film jusqu’à la fin, ou de lire un livre",
          "Rapidement ennuyé par les choses",
          "Pose des questions sur des sujets déjà discutés",
        ],
        childExamples: [
          "Du mal à maintenir l’attention lors du travail scolaire",
          "Du mal à maintenir l’attention sur un jeu",
          "Facilement distrait",
          "Du mal à se concentrer",
          "Besoin d’un environnement structuré pour ne pas être distrait",
          "Rapidement ennuyé dans des activités",
        ],
      },
      {
        code: "A3",
        question: "Donnez-vous souvent l’impression de ne pas écouter lorsqu’on vous parle directement ?",
        adultExamples: [
          "Rêveur ou préoccupé",
          "Du mal à se concentrer pendant une conversation",
          "Après-coup, ne se rappelle pas du sujet d’une conversation",
          "Change souvent de sujet dans une conversation",
          "D’autres personnes disent que vos pensées sont ailleurs",
        ],
        childExamples: [
          "Ne sait plus ce que les parents ou enseignants ont dit",
          "Rêveur ou préoccupé",
          "N’écoute qu’avec un contact visuel ou lorsque le ton est élevé",
          "Doit souvent être interpelé",
          "Les questions doivent être répétées",
        ],
      },
      {
        code: "A4",
        question:
          "Avez-vous souvent du mal à vous conformer aux consignes et à mener à terme vos tâches domestiques ou vos obligations professionnelles ?",
        adultExamples: [
          "Fait plusieurs tâches en même temps sans les terminer",
          "Du mal à finir les tâches une fois que la nouveauté a diminué",
          "Besoin de fixer un délai pour terminer les tâches",
          "Du mal à terminer les tâches administratives",
          "Du mal à suivre les instructions dans un manuel",
        ],
        childExamples: [
          "Du mal à suivre les instructions",
          "En difficulté lorsque les tâches comprennent plusieurs étapes successives",
          "Ne termine pas les choses",
          "Ne termine pas les devoirs ou ne les rend pas",
          "Besoin d’un environnement structuré pour pouvoir terminer les tâches",
        ],
      },
      {
        code: "A5",
        question: "Trouvez-vous souvent difficile d’organiser les tâches ou les activités ?",
        adultExamples: [
          "Du mal à planifier les activités de la vie quotidienne",
          "La maison ou l’espace de travail est en désordre",
          "Planifie trop de tâches ou planification inefficace",
          "Prévoit régulièrement de faire plusieurs choses au même moment",
          "Arrive en retard",
          "Incapable d’utiliser un agenda ou un journal de manière efficace",
          "Rigide par nécessité de coller au programme",
          "Faible conscience du temps",
          "Établit des listes sans les utiliser",
          "Besoin qu’un tiers structure les choses",
        ],
        childExamples: [
          "Du mal à être prêt à temps",
          "Chambre ou bureau en désordre",
          "Du mal à jouer seul",
          "Du mal à planifier des tâches ou ses devoirs",
          "Fait les choses de manière confuse",
          "Arrive en retard",
          "Faible conscience du temps",
          "Du mal à s’occuper seul",
        ],
      },
      {
        code: "A6",
        question:
          "Évitez-vous souvent, ou faites-vous à contrecœur, les tâches qui nécessitent un effort mental soutenu ?",
        adultExamples: [
          "Fait en premier les choses les plus faciles ou les plus agréables",
          "Remet à plus tard les tâches ennuyeuses ou difficiles",
          "Remet à plus tard les choses jusqu’à dépasser les délais",
          "Évite les tâches monotones, comme les tâches administratives",
          "N’aime pas lire à cause de l’effort mental",
          "Évite des tâches qui demandent beaucoup de concentration",
        ],
        childExamples: [
          "Évite des devoirs ou aversion pour les devoirs",
          "Lit peu de livres ou n’aime pas lire à cause de l’effort mental",
          "Évite des tâches qui demandent beaucoup de concentration",
          "Déteste les sujets scolaires qui demandent beaucoup de concentration",
          "Remet à plus tard les tâches ennuyeuses ou difficiles",
        ],
      },
      {
        code: "A7",
        question: "Perdez-vous souvent les objets nécessaires à votre travail ou vos activités ?",
        adultExamples: [
          "Égare portefeuille, clés ou agenda",
          "Oublie des choses en quittant un lieu",
          "Perd des papiers pour son travail",
          "Perd beaucoup de temps à chercher des choses",
          "Panique si des gens ont changé des choses de place",
          "Range les choses au mauvais endroit",
          "Perd des notes, listes ou numéros de téléphone",
        ],
        childExamples: [
          "Perd l’agenda, les stylos, les affaires de gymnastique ou d’autres choses",
          "Égare des jouets, habits ou devoirs scolaires",
          "Perd beaucoup de temps à chercher des choses",
          "Panique si des gens ont changé des choses de place",
          "Les parents ou enseignants font remarquer qu’il a perdu des choses",
        ],
      },
      {
        code: "A8",
        question: "Vous laissez-vous facilement distraire par des stimuli externes ?",
        adultExamples: [
          "Du mal à ignorer des stimuli externes",
          "Du mal à reprendre les choses après avoir été distrait",
          "Facilement distrait par des bruits ou des événements",
          "Facilement distrait par une conversation entre d’autres personnes",
          "Du mal à filtrer ou sélectionner des informations",
        ],
        childExamples: [
          "En classe, regarde souvent dehors",
          "Facilement distrait par des bruits ou des événements",
          "Du mal à reprendre les choses après avoir été distrait",
        ],
      },
      {
        code: "A9",
        question: "Avez-vous des oublis fréquents dans la vie quotidienne ?",
        adultExamples: [
          "Oublie des rendez-vous ou des obligations",
          "Oublie les clés, l’agenda, etc.",
          "A besoin de rappels fréquents concernant les rendez-vous",
          "Retourne sur ses pas pour prendre des choses oubliées",
          "Utilise des programmes rigides pour être sûr de ne rien oublier",
          "Ne tient pas à jour son agenda ou oublie de consulter son agenda",
        ],
        childExamples: [
          "Oublie des rendez-vous ou des consignes",
          "On doit souvent lui rappeler les choses",
          "S’arrête en chemin parce qu’il a oublié ce qu’il devait faire",
          "Oublie d’apporter des affaires scolaires",
          "Oublie des choses à l’école ou chez des amis",
        ],
      },
    ],
  },
  {
    id: "HI",
    title: "Hyperactivité et impulsivité",
    shortTitle: "Critère A2",
    description:
      "Les symptômes à l’âge adulte doivent être présents depuis au moins 6 mois. Les symptômes dans l’enfance se rapportent à la période entre 5 et 12 ans. Pour qu’un symptôme soit attribué au TDAH, il doit être chronique et non épisodique.",
    supplementaryLabel:
      "Parmi les symptômes d’hyperactivité ou d’impulsivité précédents, en avez-vous présenté davantage ou plus fréquemment que les autres adultes ou enfants du même âge ?",
    items: [
      {
        code: "HI1",
        label: "H/I 1",
        question: "Remuez-vous souvent les mains ou les pieds, ou vous tortillez-vous souvent sur votre siège ?",
        adultExamples: [
          "Du mal à rester assis immobile",
          "Remue les jambes",
          "Tape avec un stylo ou joue avec un objet",
          "Tortille les cheveux ou ronge les ongles",
          "Capable de contrôler l’agitation mais cela vous stresse",
        ],
        childExamples: [
          "Les parents disent souvent “tiens-toi tranquille”",
          "Remue les jambes",
          "Tape avec un stylo ou joue avec un objet",
          "Tortille les cheveux ou ronge les ongles",
          "Incapable de rester assis de façon relaxée",
          "Capable de contrôler l’agitation mais cela vous stressait",
        ],
      },
      {
        code: "HI2",
        label: "H/I 2",
        question: "Vous levez-vous souvent dans des situations où vous êtes supposé rester assis ?",
        adultExamples: [
          "Évite les réunions, conférences, cérémonies religieuses, etc.",
          "Préfère marcher plutôt que rester assis",
          "Ne reste jamais longtemps assis tranquille, bouge sans cesse",
          "Stressé par l’obligation de rester assis",
          "Trouve une excuse pour pouvoir marcher",
        ],
        childExamples: [
          "Se lève souvent pendant les repas ou en classe",
          "Trouve très difficile de rester assis en classe ou pendant les repas",
          "On lui dit souvent de rester assis",
          "Trouve une excuse pour pouvoir marcher",
        ],
      },
      {
        code: "HI3",
        label: "H/I 3",
        question: "Vous sentez-vous souvent agité ?",
        adultExamples: [
          "Se sent agité ou nerveux à l’intérieur",
          "Ressent constamment le sentiment d’avoir quelque chose à faire",
          "Trouve difficile de se relaxer",
        ],
        childExamples: [
          "Court toujours",
          "Grimpe sur les meubles ou saute sur les fauteuils",
          "Monte aux arbres",
          "Se sent agité à l’intérieur",
        ],
      },
      {
        code: "HI4",
        label: "H/I 4",
        question: "Trouvez-vous souvent difficile de profiter d’un moment de détente ?",
        adultExamples: [
          "Parle lorsque cela n’est pas approprié",
          "Se met rapidement en avant en public",
          "Bruyant dans tout type de situations",
          "Du mal à faire des activités tranquillement",
          "Du mal à parler doucement",
        ],
        childExamples: [
          "Fait du bruit en jouant ou en classe",
          "Incapable de regarder la TV ou un film tranquillement",
          "On lui demande souvent de se calmer ou d’être plus tranquille",
          "Se met rapidement en avant en public",
        ],
      },
      {
        code: "HI5",
        label: "H/I 5",
        question: "Êtes-vous souvent sur la brèche, ou comme si vous étiez dirigé par un moteur ?",
        adultExamples: [
          "Toujours occupé à faire quelque chose",
          "Déborde d’énergie, toujours en mouvement",
          "Franchit ses propres limites",
          "Lâche difficilement prise, excessivement insistant",
        ],
        childExamples: [
          "Constamment occupé",
          "Remarqué par son activité en classe ou à la maison",
          "Déborde d’énergie",
          "Toujours sur la brèche, monté sur ressorts",
        ],
      },
      {
        code: "HI6",
        label: "H/I 6",
        question: "Parlez-vous souvent trop ?",
        adultExamples: [
          "Parle tellement que les gens trouvent cela fatiguant",
          "Connu pour parler de manière incessante",
          "Trouve difficile d’arrêter de parler",
          "Tendance à trop parler",
          "Ne laisse pas l’occasion aux autres d’intervenir dans une conversation",
          "Besoin de beaucoup de mots pour dire quelque chose",
        ],
        childExamples: [
          "Connu comme une boîte à paroles",
          "Les enfants ou les enseignants demandent souvent le silence",
          "Les fiches scolaires mentionnent souvent des bavardages",
          "Puni pour avoir trop parlé",
          "Gêne le travail scolaire des autres en parlant trop",
          "Ne laisse pas les autres parler dans une conversation",
        ],
      },
      {
        code: "HI7",
        label: "H/I 7",
        question: "Laissez-vous souvent échapper la réponse à une question qui n’est pas encore entièrement posée ?",
        adultExamples: [
          "Dit ce qu’il pense",
          "Dit les choses sans réfléchir",
          "Donne des réponses avant que les gens aient fini de parler",
          "Finit les phrases des autres",
          "Manque de tact",
        ],
        childExamples: [
          "Dit les choses sans réfléchir",
          "Veut être le premier à répondre aux questions en classe",
          "Donne la première réponse qui lui vient à l’esprit",
          "Interrompt les autres avant que les phrases soient finies",
          "Blesse verbalement par manque de tact",
        ],
      },
      {
        code: "HI8",
        label: "H/I 8",
        question: "Trouvez-vous souvent difficile d’attendre votre tour ?",
        adultExamples: [
          "Difficulté à attendre dans une file, veut doubler dans une file d’attente",
          "Du mal à attendre patiemment dans la circulation ou les embouteillages",
          "Du mal à attendre son tour dans les conversations",
          "Impatient",
          "Commence ou met fin rapidement à des relations ou emplois par impatience",
        ],
        childExamples: [
          "Du mal à attendre son tour dans les sports ou les jeux",
          "Du mal à attendre son tour en classe",
          "Toujours le premier à parler ou agir",
          "Rapidement impatient",
          "Traverse la route sans regarder",
        ],
      },
      {
        code: "HI9",
        label: "H/I 9",
        question: "Interrompez-vous souvent les autres ou imposez-vous votre présence ?",
        adultExamples: [
          "Rapide à interférer avec les autres",
          "Interrompt les autres",
          "Dérange sans qu’on lui ait rien demandé",
          "Les autres font remarquer qu’il est intrusif",
          "Du mal à respecter les limites des autres",
          "A une opinion sur tout et la donne immédiatement",
        ],
        childExamples: [
          "S’immisce dans les jeux des autres",
          "Interrompt les conversations des autres",
          "Réagit sur tout",
          "Incapable d’attendre",
        ],
      },
    ],
  },
];

const impactDomains = {
  adult: [
    {
      key: "travailEducation",
      label: "Travail / éducation",
      items: [
        "N’a pas atteint le niveau d’étude pour le travail voulu",
        "Travaille en deçà du niveau d’étude",
        "Rapidement fatigué d’un lieu de travail",
        "Succession de plusieurs emplois à court terme",
        "Difficulté avec le travail administratif ou la planification",
        "N’obtient pas de promotions",
        "Sous-performant au travail",
        "A quitté un emploi ou a été renvoyé après une dispute",
        "Arrêts de travail ou invalidité liés aux symptômes",
        "Retentissement limité par compensation par un fort niveau intellectuel",
        "Retentissement limité par compensation par la structure externe",
      ],
    },
    {
      key: "relationsFamille",
      label: "Relations et ou famille",
      items: [
        "Rapidement fatigué par les relations",
        "Débute ou termine impulsivement les relations",
        "Compensation nécessaire des symptômes par le conjoint",
        "Problèmes relationnels, nombreuses disputes, manque d’intimité",
        "Divorce à cause des symptômes",
        "Problèmes sexuels à cause des symptômes",
        "Problèmes avec l’éducation à cause des symptômes",
        "Difficultés ménagères ou administratives",
        "Problèmes financiers ou jeux d’argent",
        "N’ose pas commencer une relation",
      ],
    },
    {
      key: "contactsSociaux",
      label: "Contacts sociaux",
      items: [
        "Rapidement fatigué par les contacts sociaux",
        "Difficulté à maintenir des contacts sociaux",
        "Conflits résultant de problèmes de communication",
        "Difficulté à initier des contacts sociaux",
        "Faible auto-affirmation de soi conséquence des expériences négatives",
        "Inattention, par exemple oubli d’envoyer une carte, d’être empathique, d’appeler au téléphone",
      ],
    },
    {
      key: "tempsLibre",
      label: "Temps libre / hobby",
      items: [
        "Incapable de se relaxer complètement pendant le temps libre",
        "Obligé de pratiquer beaucoup de sport pour se relaxer",
        "Blessures à la suite d’une pratique excessive du sport",
        "Incapable de terminer un livre ou de regarder un film jusqu’au bout",
        "Fatigué parce qu’affairé en permanence",
        "Rapidement lassé par les hobbies",
        "Accidents ou suspension de permis suite à un comportement dangereux",
        "Recherche de sensations ou prise trop fréquente de risques",
        "Problèmes avec la police ou la justice",
        "Hyperphagie",
      ],
    },
    {
      key: "imageDeSoi",
      label: "Confiance en soi / image de soi",
      items: [
        "Doute de lui-même suite aux remarques négatives des autres",
        "Image de soi négative à cause des échecs du passé",
        "Peur de l’échec en commençant de nouvelles choses",
        "Réaction excessive aux critiques",
        "Perfectionnisme",
        "Affecté par les symptômes du TDAH",
      ],
    },
  ],
  child: [
    {
      key: "education",
      label: "Éducation",
      items: [
        "Niveau d’études inférieur à celui prédit par le QI",
        "Redoublement à cause de problèmes de concentration",
        "Études inachevées ou renvoi d’un établissement scolaire",
        "Plus d’années pour terminer les études que nécessaire",
        "A obtenu un niveau d’étude conforme au QI mais avec beaucoup de difficultés",
        "Difficulté à faire les devoirs",
        "Éducation spéciale à cause des symptômes",
        "Commentaires des enseignants sur le comportement ou la concentration",
        "Retentissement limité par compensation par un fort niveau intellectuel",
        "Retentissement limité par compensation par la structure externe",
      ],
    },
    {
      key: "famille",
      label: "Famille",
      items: [
        "Disputes fréquentes avec frères et sœurs",
        "Punitions ou corrections fréquentes",
        "Peu de contacts avec la famille à cause des conflits",
        "A nécessité le soutien des parents plus longtemps que la normale",
      ],
    },
    {
      key: "contactsSociaux",
      label: "Contacts sociaux",
      items: [
        "Difficulté à maintenir des contacts sociaux",
        "Conflits résultant de problèmes de communication",
        "Difficulté à initier des contacts sociaux",
        "Faible auto-affirmation de soi conséquence des expériences négatives",
        "Peu d’amis",
        "Taquiné par les autres",
        "Exclu du groupe ou non invité à participer aux activités du groupe",
        "Joue les petits durs",
      ],
    },
    {
      key: "tempsLibre",
      label: "Temps libre / hobby",
      items: [
        "Incapable de se relaxer correctement pendant le temps libre",
        "Obligé de pratiquer beaucoup de sport pour se relaxer",
        "Blessures à la suite d’une pratique excessive du sport",
        "Incapable de terminer un livre ou de regarder un film jusqu’au bout",
        "Fatigué parce qu’affairé en permanence",
        "Rapidement lassé par les hobbies",
        "Recherche de sensations ou prise trop fréquente de risques",
        "Problèmes avec la police ou la justice",
        "Nombre augmenté d’accidents",
      ],
    },
    {
      key: "imageDeSoi",
      label: "Confiance en soi / image de soi",
      items: [
        "Doute de lui-même suite aux remarques négatives des autres",
        "Image de soi négative à cause des échecs du passé",
        "Peur de l’échec avant de démarrer de nouvelles choses",
        "Réaction excessive aux critiques",
        "Perfectionnisme",
      ],
    },
  ],
};

const steps = [
  { id: "intro", label: "Introduction" },
  { id: "A", label: "Inattention" },
  { id: "HI", label: "Hyperactivité / impulsivité" },
  { id: "impact", label: "Retentissement" },
  { id: "summary", label: "Résumé" },
];

const collateralOptions = ["N/A", "0", "1", "2"];
const yesNoOptions = [
  { value: null, label: "Non défini" },
  { value: true, label: "Oui" },
  { value: false, label: "Non" },
];

function buildInitialState() {
  const symptoms = {};
  symptomSections.forEach((section) => {
    section.items.forEach((item) => {
      symptoms[item.code] = {
        adultExamples: [],
        adultOther: "",
        adultPresent: null,
        childExamples: [],
        childOther: "",
        childPresent: null,
        notes: "",
      };
    });
  });

  const impact = { adult: {}, child: {} };
  impactDomains.adult.forEach((domain) => {
    impact.adult[domain.key] = { checks: [], other: "" };
  });
  impactDomains.child.forEach((domain) => {
    impact.child[domain.key] = { checks: [], other: "" };
  });

  return {
    patient: {
      nom: "",
      dateNaissance: "",
      dateEntretien: "",
      sexe: "",
      evaluateur: "",
      dossier: "",
    },
    symptoms,
    supplementary: {
      A: { adult: null, child: null },
      HI: { adult: null, child: null },
    },
    onset: {
      lifelong: null,
      onsetAge: "",
      notes: "",
    },
    impact,
    criteria: {
      adultImpactTwoDomains: null,
      childImpactTwoDomains: null,
      alternativeExplanation: null,
      alternativeExplanationDetails: "",
    },
    collateral: {
      parent: "N/A",
      partner: "N/A",
      school: "N/A",
      details: "",
    },
  };
}

function toggleInArray(array, value) {
  return array.includes(value) ? array.filter((x) => x !== value) : [...array, value];
}

function countPresent(items, symptoms, key) {
  return items.filter((item) => symptoms[item.code]?.[key] === true).length;
}

function countImpactDomains(ageImpact) {
  return Object.values(ageImpact).filter((domain) => domain.checks.length > 0 || domain.other.trim()).length;
}

function getSubtype(aCount, hiCount) {
  if (aCount >= 6 && hiCount >= 6) return "Type combiné";
  if (aCount >= 6 && hiCount < 6) return "Type inattentif prédominant";
  if (aCount < 6 && hiCount >= 6) return "Type hyperactif / impulsif prédominant";
  return "Aucun sous-type retenu sur le seul critère A";
}

function statusLabel(value) {
  if (value === true) return "Oui";
  if (value === false) return "Non";
  return "Non défini";
}

function Pill({ active, children }) {
  return <span className={`pill ${active ? "pill-ok" : "pill-neutral"}`}>{children}</span>;
}

function YesNo({ value, onChange }) {
  return (
    <div className="segment">
      {yesNoOptions.map((option) => {
        const selected = value === option.value;
        return (
          <button
            key={option.label}
            type="button"
            className={`segment-btn ${selected ? "segment-btn-active" : ""}`}
            onClick={() => onChange(option.value)}
          >
            {option.label}
          </button>
        );
      })}
    </div>
  );
}

function Checklist({ items, selected, onToggle }) {
  return (
    <div className="checklist">
      {items.map((item) => {
        const checked = selected.includes(item);
        return (
          <button
            key={item}
            type="button"
            className={`check-item ${checked ? "check-item-active" : ""}`}
            onClick={() => onToggle(item)}
          >
            <span className={`check-box ${checked ? "check-box-active" : ""}`}>{checked ? "✓" : ""}</span>
            <span>{item}</span>
          </button>
        );
      })}
    </div>
  );
}

function SymptomCard({ item, value, onChange }) {
  return (
    <article className="card symptom-card">
      <div className="card-head">
        <div>
          <div className="eyebrow">{item.label || item.code}</div>
          <h3>{item.question}</h3>
        </div>
        <div className="pill-stack">
          <Pill active={value.adultPresent === true}>Adulte: {value.adultPresent === true ? "présent" : value.adultPresent === false ? "absent" : "non défini"}</Pill>
          <Pill active={value.childPresent === true}>Enfance: {value.childPresent === true ? "présent" : value.childPresent === false ? "absent" : "non défini"}</Pill>
        </div>
      </div>

      <div className="two-col">
        <section className="panel-muted">
          <div className="panel-title">Âge adulte</div>
          <div className="panel-help">Les exemples aident la décision, mais ne valident pas automatiquement le symptôme.</div>
          <Checklist
            items={item.adultExamples}
            selected={value.adultExamples}
            onToggle={(example) => onChange({ ...value, adultExamples: toggleInArray(value.adultExamples, example) })}
          />
          <textarea
            className="field textarea"
            placeholder="Autre exemple à l’âge adulte"
            value={value.adultOther}
            onChange={(e) => onChange({ ...value, adultOther: e.target.value })}
          />
          <div className="field-group">
            <label>Symptôme présent à l’âge adulte</label>
            <YesNo value={value.adultPresent} onChange={(next) => onChange({ ...value, adultPresent: next })} />
          </div>
        </section>

        <section className="panel-muted">
          <div className="panel-title">Enfance</div>
          <div className="panel-help">Période de référence: 5 à 12 ans.</div>
          <Checklist
            items={item.childExamples}
            selected={value.childExamples}
            onToggle={(example) => onChange({ ...value, childExamples: toggleInArray(value.childExamples, example) })}
          />
          <textarea
            className="field textarea"
            placeholder="Autre exemple pendant l’enfance"
            value={value.childOther}
            onChange={(e) => onChange({ ...value, childOther: e.target.value })}
          />
          <div className="field-group">
            <label>Symptôme présent pendant l’enfance</label>
            <YesNo value={value.childPresent} onChange={(next) => onChange({ ...value, childPresent: next })} />
          </div>
        </section>
      </div>

      <textarea
        className="field textarea"
        placeholder="Notes cliniques ou contexte"
        value={value.notes}
        onChange={(e) => onChange({ ...value, notes: e.target.value })}
      />
    </article>
  );
}

function ImpactCard({ title, help, value, options, onChange }) {
  return (
    <article className="card">
      <div className="eyebrow">{help}</div>
      <h3>{title}</h3>
      <Checklist items={options} selected={value.checks} onToggle={(item) => onChange({ ...value, checks: toggleInArray(value.checks, item) })} />
      <textarea
        className="field textarea"
        placeholder="Autre élément de retentissement"
        value={value.other}
        onChange={(e) => onChange({ ...value, other: e.target.value })}
      />
    </article>
  );
}

export default function App() {
  const [data, setData] = useState(buildInitialState());
  const [step, setStep] = useState(0);
  const [flash, setFlash] = useState("");

  useEffect(() => {
    try {
      const raw = localStorage.getItem(STORAGE_KEY);
      if (raw) setData(JSON.parse(raw));
    } catch {
      // ignore corrupted local storage
    }
  }, []);

  useEffect(() => {
    try {
      localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
      setFlash("Sauvegarde automatique OK");
      const timer = window.setTimeout(() => setFlash(""), 1500);
      return () => window.clearTimeout(timer);
    } catch {
      // ignore storage errors
    }
  }, [data]);

  const counts = useMemo(() => {
    const aAdult = countPresent(symptomSections[0].items, data.symptoms, "adultPresent");
    const aChild = countPresent(symptomSections[0].items, data.symptoms, "childPresent");
    const hiAdult = countPresent(symptomSections[1].items, data.symptoms, "adultPresent");
    const hiChild = countPresent(symptomSections[1].items, data.symptoms, "childPresent");
    const adultImpactDomains = countImpactDomains(data.impact.adult);
    const childImpactDomains = countImpactDomains(data.impact.child);
    return { aAdult, aChild, hiAdult, hiChild, adultImpactDomains, childImpactDomains };
  }, [data]);

  const summary = useMemo(() => {
    const aAdultOk = counts.aAdult >= 6;
    const aChildOk = counts.aChild >= 6;
    const hiAdultOk = counts.hiAdult >= 6;
    const hiChildOk = counts.hiChild >= 6;
    const adultImpactOk = data.criteria.adultImpactTwoDomains ?? (counts.adultImpactDomains >= 2 ? true : null);
    const childImpactOk = data.criteria.childImpactTwoDomains ?? (counts.childImpactDomains >= 2 ? true : null);
    const possibleAdhd =
      (aAdultOk || hiAdultOk) &&
      (aChildOk || hiChildOk) &&
      data.onset.lifelong === true &&
      adultImpactOk === true &&
      childImpactOk === true &&
      data.criteria.alternativeExplanation === false;

    return {
      aAdultOk,
      aChildOk,
      hiAdultOk,
      hiChildOk,
      adultImpactOk,
      childImpactOk,
      adultSubtype: getSubtype(counts.aAdult, counts.hiAdult),
      childSubtype: getSubtype(counts.aChild, counts.hiChild),
      possibleAdhd,
    };
  }, [counts, data]);

  function updatePatient(key, value) {
    setData((prev) => ({ ...prev, patient: { ...prev.patient, [key]: value } }));
  }

  function updateSymptom(code, value) {
    setData((prev) => ({ ...prev, symptoms: { ...prev.symptoms, [code]: value } }));
  }

  function updateImpact(age, key, value) {
    setData((prev) => ({
      ...prev,
      impact: {
        ...prev.impact,
        [age]: { ...prev.impact[age], [key]: value },
      },
    }));
  }

  function resetAll() {
    if (!window.confirm("Réinitialiser tout le formulaire ?")) return;
    const next = buildInitialState();
    setData(next);
    localStorage.removeItem(STORAGE_KEY);
  }

  async function copySummary() {
    const text = [
      `Patient: ${data.patient.nom || "Non renseigné"}`,
      `Critère A adulte: ${counts.aAdult}/9 (${summary.aAdultOk ? ">= 6" : "< 6"})`,
      `Critère A enfance: ${counts.aChild}/9 (${summary.aChildOk ? ">= 6" : "< 6"})`,
      `Critère H/I adulte: ${counts.hiAdult}/9 (${summary.hiAdultOk ? ">= 6" : "< 6"})`,
      `Critère H/I enfance: ${counts.hiChild}/9 (${summary.hiChildOk ? ">= 6" : "< 6"})`,
      `Persistance avant 7 ans: ${statusLabel(data.onset.lifelong)}`,
      `Retentissement adulte >= 2 domaines: ${statusLabel(summary.adultImpactOk)}`,
      `Retentissement enfance >= 2 domaines: ${statusLabel(summary.childImpactOk)}`,
      `Autre explication psychiatrique meilleure: ${statusLabel(data.criteria.alternativeExplanation)}`,
      `Sous-type adulte: ${summary.adultSubtype}`,
      `Sous-type enfance: ${summary.childSubtype}`,
      `Conclusion structurée: ${summary.possibleAdhd ? "Compatible avec la logique DIVA 2.0" : "Conditions non réunies ou dossier incomplet"}`,
    ].join("\n");

    try {
      await navigator.clipboard.writeText(text);
      setFlash("Résumé copié");
      window.setTimeout(() => setFlash(""), 1500);
    } catch {
      setFlash("Copie impossible");
      window.setTimeout(() => setFlash(""), 1500);
    }
  }

  return (
    <div className="app-shell">
      <header className="hero card">
        <div className="hero-top">Assistant d’entretien structuré inspiré du DIVA 2.0 FR</div>
        <h1>Site prêt à déployer sur Vercel, avec logique fidèle au PDF et UX simplifiée</h1>
        <p className="hero-text">
          Les exemples servent d’aide à la réflexion. La validation d’un symptôme se fait toujours via un choix explicite “présent / absent” pour l’âge adulte et pour l’enfance.
        </p>
        <div className="warning-box">
          Cet outil structure un entretien. Il ne remplace pas un diagnostic médical ou psychiatrique.
        </div>
      </header>

      <div className="main-grid">
        <main className="content-col">
          <nav className="step-nav card">
            {steps.map((item, index) => (
              <button
                key={item.id}
                type="button"
                className={`step-btn ${index === step ? "step-btn-active" : ""}`}
                onClick={() => setStep(index)}
              >
                <span className="step-index">Étape {index + 1}</span>
                <span>{item.label}</span>
              </button>
            ))}
          </nav>

          {step === 0 && (
            <section className="stack">
              <article className="card">
                <h2>Cadre de passation</h2>
                <p>
                  Le document interroge les symptômes à l’âge adulte, au cours des 6 derniers mois ou plus, puis pendant l’enfance entre 5 et 12 ans. Pour chaque item, on coche des exemples reconnus, puis on décide si le symptôme est présent ou absent.
                </p>
                <div className="form-grid">
                  <label>
                    <span>Nom du patient</span>
                    <input className="field" value={data.patient.nom} onChange={(e) => updatePatient("nom", e.target.value)} />
                  </label>
                  <label>
                    <span>Date de naissance</span>
                    <input className="field" type="date" value={data.patient.dateNaissance} onChange={(e) => updatePatient("dateNaissance", e.target.value)} />
                  </label>
                  <label>
                    <span>Date de l’entretien</span>
                    <input className="field" type="date" value={data.patient.dateEntretien} onChange={(e) => updatePatient("dateEntretien", e.target.value)} />
                  </label>
                  <label>
                    <span>Sexe</span>
                    <select className="field" value={data.patient.sexe} onChange={(e) => updatePatient("sexe", e.target.value)}>
                      <option value="">Non renseigné</option>
                      <option value="M">M</option>
                      <option value="F">F</option>
                    </select>
                  </label>
                  <label>
                    <span>Évaluateur</span>
                    <input className="field" value={data.patient.evaluateur} onChange={(e) => updatePatient("evaluateur", e.target.value)} />
                  </label>
                  <label>
                    <span>Numéro de dossier</span>
                    <input className="field" value={data.patient.dossier} onChange={(e) => updatePatient("dossier", e.target.value)} />
                  </label>
                </div>
              </article>

              <article className="card">
                <h2>Règle UX essentielle</h2>
                <p>
                  Les cases d’exemples sont là pour documenter le vécu. Elles ne déclenchent jamais automatiquement la validation d’un item. Le vrai point de décision est le sélecteur “Symptôme présent”.
                </p>
              </article>
            </section>
          )}

          {step === 1 && (
            <section className="stack">
              <article className="card">
                <div className="eyebrow">{symptomSections[0].shortTitle}</div>
                <h2>{symptomSections[0].title}</h2>
                <p>{symptomSections[0].description}</p>
              </article>

              {symptomSections[0].items.map((item) => (
                <SymptomCard key={item.code} item={item} value={data.symptoms[item.code]} onChange={(value) => updateSymptom(item.code, value)} />
              ))}

              <article className="card">
                <h2>Supplément au critère A</h2>
                <p>{symptomSections[0].supplementaryLabel}</p>
                <div className="two-col compact">
                  <div className="field-group">
                    <label>Âge adulte</label>
                    <YesNo value={data.supplementary.A.adult} onChange={(next) => setData((prev) => ({ ...prev, supplementary: { ...prev.supplementary, A: { ...prev.supplementary.A, adult: next } } }))} />
                  </div>
                  <div className="field-group">
                    <label>Enfance</label>
                    <YesNo value={data.supplementary.A.child} onChange={(next) => setData((prev) => ({ ...prev, supplementary: { ...prev.supplementary, A: { ...prev.supplementary.A, child: next } } }))} />
                  </div>
                </div>
              </article>
            </section>
          )}

          {step === 2 && (
            <section className="stack">
              <article className="card">
                <div className="eyebrow">{symptomSections[1].shortTitle}</div>
                <h2>{symptomSections[1].title}</h2>
                <p>{symptomSections[1].description}</p>
              </article>

              {symptomSections[1].items.map((item) => (
                <SymptomCard key={item.code} item={item} value={data.symptoms[item.code]} onChange={(value) => updateSymptom(item.code, value)} />
              ))}

              <article className="card">
                <h2>Supplément au critère H/I</h2>
                <p>{symptomSections[1].supplementaryLabel}</p>
                <div className="two-col compact">
                  <div className="field-group">
                    <label>Âge adulte</label>
                    <YesNo value={data.supplementary.HI.adult} onChange={(next) => setData((prev) => ({ ...prev, supplementary: { ...prev.supplementary, HI: { ...prev.supplementary.HI, adult: next } } }))} />
                  </div>
                  <div className="field-group">
                    <label>Enfance</label>
                    <YesNo value={data.supplementary.HI.child} onChange={(next) => setData((prev) => ({ ...prev, supplementary: { ...prev.supplementary, HI: { ...prev.supplementary.HI, child: next } } }))} />
                  </div>
                </div>
              </article>
            </section>
          )}

          {step === 3 && (
            <section className="stack">
              <article className="card">
                <h2>Âge de début</h2>
                <div className="field-group">
                  <label>Quelques symptômes étaient-ils présents avant 7 ans ?</label>
                  <YesNo value={data.onset.lifelong} onChange={(next) => setData((prev) => ({ ...prev, onset: { ...prev.onset, lifelong: next } }))} />
                </div>
                <label>
                  <span>Si non, âge de début</span>
                  <input className="field" value={data.onset.onsetAge} onChange={(e) => setData((prev) => ({ ...prev, onset: { ...prev.onset, onsetAge: e.target.value } }))} />
                </label>
                <textarea className="field textarea" placeholder="Notes sur l’évolution des symptômes" value={data.onset.notes} onChange={(e) => setData((prev) => ({ ...prev, onset: { ...prev.onset, notes: e.target.value } }))} />
              </article>

              <article className="card">
                <h2>Retentissement à l’âge adulte</h2>
                <p>Le trouble doit avoir un retentissement dans au moins deux domaines.</p>
              </article>
              <div className="impact-grid">
                {impactDomains.adult.map((domain) => (
                  <ImpactCard
                    key={domain.key}
                    title={domain.label}
                    help="Âge adulte"
                    value={data.impact.adult[domain.key]}
                    options={domain.items}
                    onChange={(value) => updateImpact("adult", domain.key, value)}
                  />
                ))}
              </div>
              <article className="card">
                <div className="result-line">
                  <span>Domaines documentés automatiquement à l’âge adulte</span>
                  <strong>{counts.adultImpactDomains}</strong>
                </div>
                <div className="field-group">
                  <label>Preuve d’une altération du fonctionnement dans 2 domaines ou plus à l’âge adulte</label>
                  <YesNo value={data.criteria.adultImpactTwoDomains} onChange={(next) => setData((prev) => ({ ...prev, criteria: { ...prev.criteria, adultImpactTwoDomains: next } }))} />
                </div>
              </article>

              <article className="card">
                <h2>Retentissement pendant l’enfance</h2>
                <p>Le trouble doit avoir un retentissement dans au moins deux domaines.</p>
              </article>
              <div className="impact-grid">
                {impactDomains.child.map((domain) => (
                  <ImpactCard
                    key={domain.key}
                    title={domain.label}
                    help="Enfance"
                    value={data.impact.child[domain.key]}
                    options={domain.items}
                    onChange={(value) => updateImpact("child", domain.key, value)}
                  />
                ))}
              </div>
              <article className="card">
                <div className="result-line">
                  <span>Domaines documentés automatiquement pendant l’enfance</span>
                  <strong>{counts.childImpactDomains}</strong>
                </div>
                <div className="field-group">
                  <label>Preuve d’une altération du fonctionnement dans 2 domaines ou plus pendant l’enfance</label>
                  <YesNo value={data.criteria.childImpactTwoDomains} onChange={(next) => setData((prev) => ({ ...prev, criteria: { ...prev.criteria, childImpactTwoDomains: next } }))} />
                </div>
              </article>

              <article className="card">
                <h2>Critère E et informations collatérales</h2>
                <div className="field-group">
                  <label>Les symptômes sont-ils mieux expliqués par un autre trouble psychiatrique ?</label>
                  <YesNo value={data.criteria.alternativeExplanation} onChange={(next) => setData((prev) => ({ ...prev, criteria: { ...prev.criteria, alternativeExplanation: next } }))} />
                </div>
                <textarea className="field textarea" placeholder="Précisions si autre diagnostic explicatif" value={data.criteria.alternativeExplanationDetails} onChange={(e) => setData((prev) => ({ ...prev, criteria: { ...prev.criteria, alternativeExplanationDetails: e.target.value } }))} />
                <div className="form-grid">
                  <label>
                    <span>Parent, fratrie, autre</span>
                    <select className="field" value={data.collateral.parent} onChange={(e) => setData((prev) => ({ ...prev, collateral: { ...prev.collateral, parent: e.target.value } }))}>
                      {collateralOptions.map((option) => <option key={option} value={option}>{option}</option>)}
                    </select>
                  </label>
                  <label>
                    <span>Partenaire, ami proche, autre</span>
                    <select className="field" value={data.collateral.partner} onChange={(e) => setData((prev) => ({ ...prev, collateral: { ...prev.collateral, partner: e.target.value } }))}>
                      {collateralOptions.map((option) => <option key={option} value={option}>{option}</option>)}
                    </select>
                  </label>
                  <label>
                    <span>Livrets scolaires</span>
                    <select className="field" value={data.collateral.school} onChange={(e) => setData((prev) => ({ ...prev, collateral: { ...prev.collateral, school: e.target.value } }))}>
                      {collateralOptions.map((option) => <option key={option} value={option}>{option}</option>)}
                    </select>
                  </label>
                </div>
                <textarea className="field textarea" placeholder="Détails sur les informations collatérales" value={data.collateral.details} onChange={(e) => setData((prev) => ({ ...prev, collateral: { ...prev.collateral, details: e.target.value } }))} />
              </article>
            </section>
          )}

          {step === 4 && (
            <section className="stack">
              <article className="card">
                <h2>Résumé des symptômes A et H/I</h2>
                <div className="table-wrap">
                  <table>
                    <thead>
                      <tr>
                        <th>Critère</th>
                        <th>Question</th>
                        <th>Adulte</th>
                        <th>Enfance</th>
                      </tr>
                    </thead>
                    <tbody>
                      {[...symptomSections[0].items, ...symptomSections[1].items].map((item) => {
                        const value = data.symptoms[item.code];
                        return (
                          <tr key={item.code}>
                            <td>{item.label || item.code}</td>
                            <td>{item.question}</td>
                            <td>{statusLabel(value.adultPresent)}</td>
                            <td>{statusLabel(value.childPresent)}</td>
                          </tr>
                        );
                      })}
                    </tbody>
                  </table>
                </div>
              </article>

              <div className="summary-grid">
                <article className="card summary-card">
                  <h2>Formulaire de cotation, critère A</h2>
                  <div className="result-list">
                    <div className="result-line"><span>Nombre de symptômes du critère A en enfance</span><strong>{counts.aChild} / 9</strong></div>
                    <div className="result-line"><span>Nombre de symptômes du critère H/I en enfance</span><strong>{counts.hiChild} / 9</strong></div>
                    <div className="result-line"><span>Nombre de symptômes du critère A à l’âge adulte</span><strong>{counts.aAdult} / 9</strong></div>
                    <div className="result-line"><span>Nombre de symptômes du critère H/I à l’âge adulte</span><strong>{counts.hiAdult} / 9</strong></div>
                  </div>
                  <div className="pill-stack big-gap">
                    <Pill active={summary.aChildOk}>Enfance, critère A ≥ 6: {summary.aChildOk ? "oui" : "non"}</Pill>
                    <Pill active={summary.hiChildOk}>Enfance, critère H/I ≥ 6: {summary.hiChildOk ? "oui" : "non"}</Pill>
                    <Pill active={summary.aAdultOk}>Âge adulte, critère A ≥ 6: {summary.aAdultOk ? "oui" : "non"}</Pill>
                    <Pill active={summary.hiAdultOk}>Âge adulte, critère H/I ≥ 6: {summary.hiAdultOk ? "oui" : "non"}</Pill>
                  </div>
                </article>

                <article className="card summary-card">
                  <h2>Critères B, C, D et E</h2>
                  <div className="pill-stack big-gap">
                    <Pill active={data.onset.lifelong === true}>Persistance depuis l’enfance: {statusLabel(data.onset.lifelong)}</Pill>
                    <Pill active={summary.childImpactOk === true}>Retentissement dans ≥ 2 domaines pendant l’enfance: {statusLabel(summary.childImpactOk)}</Pill>
                    <Pill active={summary.adultImpactOk === true}>Retentissement dans ≥ 2 domaines à l’âge adulte: {statusLabel(summary.adultImpactOk)}</Pill>
                    <Pill active={data.criteria.alternativeExplanation === false}>Autre diagnostic meilleur: {statusLabel(data.criteria.alternativeExplanation)}</Pill>
                  </div>
                  <div className="final-box">
                    <div className="eyebrow light">Conclusion structurée</div>
                    <div className="final-title">{summary.possibleAdhd ? "Compatible avec la logique DIVA 2.0" : "Conditions non réunies ou dossier incomplet"}</div>
                    <p>Cette conclusion reste un repère de structure et ne vaut pas diagnostic médical.</p>
                  </div>
                </article>
              </div>

              <div className="summary-grid">
                <article className="card">
                  <h2>Sous-type en enfance</h2>
                  <p>{summary.childSubtype}</p>
                </article>
                <article className="card">
                  <h2>Sous-type à l’âge adulte</h2>
                  <p>{summary.adultSubtype}</p>
                  <p className="small-note">Si les sous-types diffèrent entre enfance et âge adulte, le sous-type adulte prévaut dans le formulaire.</p>
                </article>
              </div>
            </section>
          )}

          <div className="footer-actions card">
            <button type="button" className="btn" onClick={() => setStep((current) => Math.max(0, current - 1))} disabled={step === 0}>
              ← Étape précédente
            </button>
            <div className="flash-text">{flash}</div>
            <button type="button" className="btn btn-primary" onClick={() => setStep((current) => Math.min(steps.length - 1, current + 1))} disabled={step === steps.length - 1}>
              Étape suivante →
            </button>
          </div>
        </main>

        <aside className="sidebar-col">
          <div className="card sidebar sticky-box">
            <h2>Résumé rapide</h2>
            <div className="sidebar-block">
              <div className="sidebar-label">Critère A</div>
              <div className="sidebar-line"><span>Adulte</span><strong>{counts.aAdult} / 9</strong></div>
              <div className="sidebar-line"><span>Enfance</span><strong>{counts.aChild} / 9</strong></div>
            </div>
            <div className="sidebar-block">
              <div className="sidebar-label">Critère H/I</div>
              <div className="sidebar-line"><span>Adulte</span><strong>{counts.hiAdult} / 9</strong></div>
              <div className="sidebar-line"><span>Enfance</span><strong>{counts.hiChild} / 9</strong></div>
            </div>
            <div className="sidebar-block">
              <div className="sidebar-label">Retentissement</div>
              <div className="sidebar-line"><span>Adulte</span><strong>{counts.adultImpactDomains} domaine(s)</strong></div>
              <div className="sidebar-line"><span>Enfance</span><strong>{counts.childImpactDomains} domaine(s)</strong></div>
            </div>
            <div className="pill-stack big-gap">
              <Pill active={summary.aAdultOk || summary.hiAdultOk}>Seuil adulte atteint: {summary.aAdultOk || summary.hiAdultOk ? "oui" : "non"}</Pill>
              <Pill active={summary.aChildOk || summary.hiChildOk}>Seuil enfance atteint: {summary.aChildOk || summary.hiChildOk ? "oui" : "non"}</Pill>
              <Pill active={summary.possibleAdhd}>Structure DIVA complète: {summary.possibleAdhd ? "oui" : "non"}</Pill>
            </div>
            <div className="sidebar-actions">
              <button type="button" className="btn btn-primary full" onClick={copySummary}>Copier le résumé</button>
              <button type="button" className="btn full" onClick={() => localStorage.setItem(STORAGE_KEY, JSON.stringify(data))}>Sauvegarder maintenant</button>
              <button type="button" className="btn full btn-danger" onClick={resetAll}>Réinitialiser</button>
            </div>
            <p className="small-note">Note: le formulaire DIVA 2.0 cote le seuil principal à 6 symptômes ou plus par domaine. Une note du document mentionne qu’une littérature a aussi discuté un seuil de 4 à l’âge adulte, mais ce site reste aligné sur le formulaire du PDF.</p>
          </div>
        </aside>
      </div>
    </div>
  );
}
