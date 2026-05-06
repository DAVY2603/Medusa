# Medusa B2B E-Commerce Platform

Une plateforme e-commerce B2B moderne construite avec **Medusa**, dédiée à la vente de produits en ligne aux entreprises.

## 🎯 Objectifs

- Catalogue de produits B2B complet
- Gestion des clients professionnels
- Système de commande professionnel
- Intégration logistique
- Dashboard d'administration
- API REST complète

## 🛠️ Stack Technologique

- **Backend:** Medusa.js (Node.js)
- **Frontend:** React/Next.js (à configurer)
- **Base de données:** PostgreSQL
- **Cache:** Redis
- **Hébergement:** À définir

## 📦 Structure du Projet

```
medusa-b2b/
├── backend/          # API Medusa
├── admin/            # Dashboard d'administration (Medusa Admin)
├── storefront/       # Vitrine client (Next.js)
├── docs/             # Documentation
└── docker-compose.yml
```

## 🚀 Installation Rapide

```bash
# Installation de Medusa CLI
npm install -g @medusajs/medusa-cli

# Créer un nouveau projet Medusa
medusa new medusa-b2b --seed

# Installer les dépendances
cd medusa-b2b
npm install

# Démarrer le serveur de développement
npm run dev
```

## 📋 Prérequis

- Node.js 14+
- PostgreSQL 10+
- Redis (optionnel mais recommandé)
- npm ou yarn

## 🔧 Configuration Initiale

À faire :
- [ ] Configurer la base de données PostgreSQL
- [ ] Configurer les variables d'environnement (.env)
- [ ] Mettre en place l'authentification B2B
- [ ] Configurer les catégories de produits
- [ ] Ajouter des plugins personnalisés
- [ ] Configurer les paiements (Stripe, etc.)
- [ ] Mise en place du système de tarification B2B

## 📚 Documentation Utile

- [Documentation Medusa](https://docs.medusajs.com/)
- [API Reference](https://docs.medusajs.com/api)
- [Plugins](https://github.com/medusajs/medusa/tree/master/packages/plugins)

## 👨‍💻 Développement

```bash
# Démarrer le projet en mode développement
npm run dev

# Accéder à l'admin
http://localhost:9000/admin

# API disponible à
http://localhost:9000
```

## 📞 Support

Pour toute question sur Medusa, consultez la [documentation officielle](https://docs.medusajs.com/) ou le [forum communautaire](https://discord.gg/medusajs).

## 📄 Licence

À définir

---

**Maintenu par:** DAVY2603
