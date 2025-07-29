# 🎯 W.I.S.E. - Windows & Linux Intelligent Situational Examiner

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux-lightgrey.svg)](https://github.com/your-username/wise)
[![DFIR](https://img.shields.io/badge/DFIR-Tool-orange.svg)](https://github.com/your-username/wise)

> **Outil DFIR nouvelle génération** - Collecte, analyse IA et synthétise les incidents de sécurité Windows et Linux

![WISE Logo](wise.png)

---

## 📋 Table des matières

- [🎯 Présentation](#-présentation)
- [✨ Fonctionnalités](#-fonctionnalités)
- [🚀 Installation](#-installation)
- [💻 Utilisation](#-utilisation)
- [⚙️ Configuration](#️-configuration)
- [🧪 Tests](#-tests)
- [📦 Packaging](#-packaging)
- [🏗️ Architecture](#️-architecture)
- [🔧 Dépannage](#-dépannage)
- [❓ FAQ](#-faq)
- [🤝 Contribution](#-contribution)
- [🔒 Sécurité](#-sécurité)
- [📄 Licence](#-licence)

---

## 🎯 Présentation

**W.I.S.E.** (Windows & Linux Intelligent Situational Examiner) est un outil DFIR révolutionnaire qui combine collecte d'artefacts, analyse IA locale et génération de rapports professionnels pour Windows et Linux.

### 🌟 Points forts

- **🔍 Multi-plateforme** : Windows et Linux dans un seul outil
- **🤖 IA Locale** : Analyse intelligente avec modèle Phi-3 ONNX
- **📊 Rapports Pro** : HTML/PDF avec narratif automatique
- **⚡ Performance** : Traitement streaming et scalable
- **🛡️ Sécurité** : Validation intégrée et audit automatique

---

## ✨ Fonctionnalités

### 🔍 Collecte avancée
- **Windows** : Logs EVTX, Registre, Persistance, Tâches planifiées
- **Linux** : Logs système, Shell history, Cron, Services
- **Navigateurs** : Historique Chrome, Firefox, Edge
- **Mémoire** : Analyse Volatility intégrée

### 🤖 Analyse IA locale
- **Scoring intelligent** (0-10) basé sur des patterns d'attaque
- **Mapping MITRE ATT&CK®** automatique
- **Justification détaillée** pour chaque événement
- **Modèle Phi-3 ONNX** léger et efficace

### 📊 Rapports professionnels
- **HTML moderne** avec design responsive
- **Export PDF** automatique
- **Narratif automatique** en français
- **Enrichissement Threat Intel** (VirusTotal)

### 🛠️ Outils intégrés
- **Logging professionnel** : Console + fichier
- **Configuration externe** : Tout modifiable dans `config.yaml`
- **Tests automatisés** : Pytest, non-régression garantie
- **Self-check** : Diagnostic complet de l'environnement

---

## 🚀 Installation

### Option 1 : Installation automatique (Recommandée)

```bash
# 1. Cloner le repository
git clone https://github.com/your-username/wise.git
cd wise

# 2. Installer les dépendances
pip install -r requirements.txt

# 3. Finaliser l'installation (crée tout, vérifie tout)
python finalize_setup.py

# 4. Télécharger le modèle Phi-3 automatiquement
python download_model.py
```

### Option 2 : Installation manuelle

```bash
# 1. Installer les dépendances
pip install -r requirements.txt

# 2. Télécharger le modèle IA manuellement
# Aller sur https://huggingface.co/microsoft/Phi-3-mini-4k-instruct-onnx
# Télécharger tous les fichiers dans le dossier model/

# 3. Configurer l'outil
# Modifier config.yaml selon vos besoins
```

### ✅ Vérification de l'installation

```bash
# Diagnostic complet de l'environnement
python scripts/self_check.py

# Test avec la démo
python wise.py analyze demo_attack.jsonl
```

---

## 💻 Utilisation

### 🔍 Collecte d'artefacts

```bash
# Collecte complète Windows/Linux
python wise.py collect

# Génère: wise_collection_YYYY-MM-DD_HH-MM-SS.jsonl
```

### 🤖 Analyse avec IA

```bash
# Analyser un fichier de collecte
python wise.py analyze <fichier_collecte.jsonl>

# Génère: report_<fichier>_<timestamp>.html
```

### 🧠 Analyse mémoire (avec Volatility)

```bash
# Analyser un dump mémoire
python wise.py memory-scan memdump.mem

# Intègre l'analyse mémoire à l'IA
```

### 🎯 Test rapide avec la démo

```bash
# Analyser un scénario d'attaque simulée
python wise.py analyze demo_attack.jsonl
```

### 📊 Exemples de commandes

```bash
# Collecte + Analyse en une commande
python wise.py collect && python wise.py analyze wise_collection_*.jsonl

# Analyse avec export PDF
python wise.py analyze data.jsonl --pdf

# Collecte avec logging détaillé
python wise.py collect --verbose
```

---

## ⚙️ Configuration

Le fichier `config.yaml` permet de personnaliser tous les aspects :

```yaml
# Configuration de l'analyseur IA
analyzer:
  model_path: "./model"
  export_pdf: false
  max_tokens: 2048

# Configuration du logging
logging:
  console_level: "INFO"
  file_level: "DEBUG"
  log_file: "wise.log"

# Configuration Threat Intelligence
threat_intel:
  virustotal_api_key: ""  # Optionnel
  enable_enrichment: true

# Configuration analyse mémoire
memory_analysis:
  volatility_path: "C:/chemin/vers/volatility3.exe"
  enable_plugins: ["pslist", "cmdline", "filescan"]

# Configuration des collecteurs
collectors:
  windows:
    enable_evtx: true
    enable_registry: true
    enable_chrome: true
  linux:
    enable_syslog: true
    enable_shell_history: true
    enable_cron: true
```

---

## 🧪 Tests

### Tests automatisés

```bash
# Lancer tous les tests
pytest

# Tests avec couverture
pytest --cov=.

# Tests spécifiques
pytest tests/test_collector.py
pytest tests/test_analyzer.py
```

### Tests manuels

```bash
# Test de collecte Windows
python wise.py collect --platform windows

# Test de collecte Linux
python wise.py collect --platform linux

# Test d'analyse avec démo
python wise.py analyze demo_attack.jsonl
```

---

## 📦 Packaging

### Créer un exécutable standalone

```bash
# Installation de PyInstaller
pip install pyinstaller

# Créer l'exécutable
pyinstaller --onefile --name wise wise.py

# L'exécutable sera dans dist/
./dist/wise.exe collect
./dist/wise.exe analyze data.jsonl
```

### Distribution

```bash
# Créer un package distributable
python setup.py sdist bdist_wheel

# Installer en mode développement
pip install -e .
```

---

## 🏗️ Architecture

```
WISE/
├── 📄 wise.py                 # Script principal
├── ⚙️ config.yaml             # Configuration
├── 🎯 demo_attack.jsonl       # Démo d'attaque simulée
├── 📥 download_model.py       # Téléchargement automatique du modèle
├── ✅ finalize_setup.py       # Script de finalisation
├── 📋 requirements.txt        # Dépendances Python
├── 📁 collector/              # Modules de collecte
│   ├── 🪟 windows.py          # Collecteur Windows
│   └── 🐧 linux.py            # Collecteur Linux
├── 🤖 analyzer/               # Modules d'analyse
│   ├── 🧠 ai.py               # Moteur IA (Phi-3)
│   ├── 🕵️ threat_intel.py     # Threat Intelligence
│   ├── 🧠 memory_analyzer.py  # Analyse mémoire
│   └── 📚 playbooks.py        # Scénarios d'attaque
├── 🧪 tests/                  # Tests automatisés
├── 🔧 scripts/                # Scripts utilitaires
│   └── 🔍 self_check.py       # Diagnostic système
└── 🤖 model/                  # Modèle Phi-3 (à télécharger)
```

---

## 🔧 Dépannage

### ❌ Le modèle ne se charge pas

```bash
# Vérifier la présence du modèle
python finalize_setup.py

# Télécharger le modèle automatiquement
python download_model.py

# Vérifier les permissions
ls -la model/
```

### ❌ Erreur de dépendances

```bash
# Réinstaller toutes les dépendances
pip install -r requirements.txt --force-reinstall

# Vérifier la version Python
python --version  # Doit être 3.8+

# Mettre à jour pip
pip install --upgrade pip
```

### ❌ Permission refusée (Windows)

```bash
# Lancer en tant qu'administrateur
# Ouvrir PowerShell en tant qu'administrateur
# Puis exécuter les commandes
```

### ✅ Test de fonctionnement

```bash
# Diagnostic complet
python scripts/self_check.py

# Test avec la démo
python wise.py analyze demo_attack.jsonl

# Vérifier les logs
tail -f wise.log
```

---

## ❓ FAQ

### 🤔 Comment changer le modèle IA ?
Modifiez `model_path` dans `config.yaml` vers un autre modèle ONNX compatible.

### 🤔 Comment enrichir avec VirusTotal ?
Ajoutez votre clé API dans `threat_intel.virustotal_api_key` dans `config.yaml`.

### 🤔 Comment ajouter un artefact ?
1. Ajoutez une fonction dans `collector/windows.py` ou `collector/linux.py`
2. Suivez le format JSONL unifié pour la normalisation
3. Ajoutez des tests dans `tests/`

### 🤔 Comment générer un PDF ?
1. Installez `wkhtmltopdf` sur votre système
2. Activez `analyzer.export_pdf: true` dans `config.yaml`

### 🤔 Comment contribuer ?
Voir la section [Contribution](#-contribution) ci-dessous.

---

## 🤝 Contribution

Nous accueillons toutes les contributions ! Voici comment participer :

### 🐛 Signaler un bug
1. Vérifiez que le bug n'a pas déjà été signalé
2. Créez une issue avec un titre descriptif
3. Incluez les étapes pour reproduire le bug
4. Ajoutez les logs d'erreur si disponibles

### 💡 Proposer une fonctionnalité
1. Créez une issue avec le label "enhancement"
2. Décrivez la fonctionnalité souhaitée
3. Expliquez pourquoi cette fonctionnalité serait utile

### 🔧 Contribuer au code
1. Fork le repository
2. Créez une branche pour votre fonctionnalité
3. Committez vos changements
4. Créez une Pull Request

### 📝 Guidelines de développement
- Suivez les conventions PEP 8
- Ajoutez des tests pour les nouvelles fonctionnalités
- Documentez les nouvelles fonctions
- Mettez à jour le README si nécessaire

---

## 🔒 Sécurité

### Politique de sécurité
- Signalez les vulnérabilités à [security@your-domain.com](mailto:security@your-domain.com)
- Ne créez pas d'issue publique pour les problèmes de sécurité
- Nous nous engageons à répondre dans les 48h

### Bonnes pratiques
- W.I.S.E. ne collecte que des données locales
- Aucune donnée n'est envoyée à des serveurs externes (sauf VirusTotal si configuré)
- Les logs peuvent contenir des informations sensibles
- Utilisez W.I.S.E. uniquement sur des systèmes autorisés

---

## 📄 Licence

Ce projet est sous licence MIT. Voir le fichier [LICENSE](LICENSE) pour plus de détails.

```
MIT License

Copyright (c) 2024 W.I.S.E. Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 🙏 Remerciements

- **Microsoft** pour le modèle Phi-3
- **MITRE** pour le framework ATT&CK
- **VirusTotal** pour l'API Threat Intelligence
- **La communauté DFIR** pour les retours et suggestions

---

## 📞 Support

- 📧 **Email** : [support@your-domain.com](mailto:support@your-domain.com)
- 💬 **Discussions** : [GitHub Discussions](https://github.com/your-username/wise/discussions)
- 🐛 **Issues** : [GitHub Issues](https://github.com/your-username/wise/issues)
- 📖 **Documentation** : [Wiki](https://github.com/your-username/wise/wiki)

---

<div align="center">

**⭐ Si W.I.S.E. vous aide, n'oubliez pas de mettre une étoile ! ⭐**

</div>
