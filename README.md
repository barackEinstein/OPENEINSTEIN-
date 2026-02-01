
    1percent-finance/
├── README.md                    
├── LICENSE                      # Licence (MIT recommandé)
├── .github/
│   ├── FUNDING.yml             # Pour les dons/sponsors
│   └── ISSUE_TEMPLATE/         # Pour les contributions
├── docs/
│   ├── ARCHITECTURE.md         # Comment Nexus Core marche
│   ├── API_SPEC.md            # Future API (en design)
│   └── CORRIDORS.md           # Les corridors supportés
├── prototypes/
│   ├── calculator/             # Ton comparateur en ligne
│   │   ├── index.html
│   │   ├── style.css
│   │   └── script.js
│   └── routing-simulator/      # Simulateur de Nexus Core
├── research/
│   ├── fee-analysis/           # Analyse frais PayPal/Stripe
│   └── mobile-money-apis/      # Documentation API africaines
└── CONTRIBUTING.md             # Comment contribuer


# 🚀 1Percent - L'argent devrait arriver en entier

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

## 📊 Le Problème
PayPal prend 3.5%. Stripe prend 2.9% + 0.30€. Western Union prend 8-12%. 
**Pourquoi envoyer de l'argent coûte-t-il 10x plus que le nécessaire ?**

## 💡 Notre Solution
**1Percent** - Un système de paiement intelligent qui trouve systématiquement le chemin le moins cher via notre algorithme **Nexus Core**.

### Comment ça marche

## 🎯 Démo Live : Comparateur de Frais
👉 **[Tester le comparateur](https://site-tbnf2ydge.godaddysites.com)**

| Service | Frais sur 100€ | Reçu | Pourcentage |
|---------|---------------|------|------------|
| PayPal | 3.50€ | 96.50€ | 3.5% |
| Stripe | 3.20€ | 96.80€ | 2.9% + 0.30€ |
| **1Percent** | **1.00€** | **99.00€** | **1%** |

## 🏗️ Architecture Technique
```javascript
// Nexus Core - Algorithme de routage
class NexusCore {
  async findOptimalRoute(amount, from, to) {
    const corridors = await this.scanAllCorridors();
    return corridors.sort((a, b) => 
      a.totalCost - b.totalCost + (a.reliabilityScore - b.reliabilityScore)
    )[0];
  }
}
MIT License

Copyright (c) 2026 1Percent

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