# 📖 Guide Complet de Déploiement Medusa B2B sur Vercel (GRATUIT)

## 🎯 Objectif
Déployer votre plateforme e-commerce B2B Medusa sur Vercel avec une base de données PostgreSQL gratuite en 15 minutes.

---

## 📋 Checklist Pré-déploiement

- [ ] Compte Vercel créé (https://vercel.com)
- [ ] Compte Neon créé (https://console.neon.tech)
- [ ] Git et Node.js installés
- [ ] Repository DAVY2603/Medusa cloné localement

---

## 🔧 ÉTAPE 1 : Configurer la Base de Données Gratuite (Neon PostgreSQL)

### 1.1 Créer un compte Neon
1. Allez sur https://console.neon.tech
2. Inscrivez-vous avec votre email ou GitHub
3. Créez un projet (nom : `medusa-b2b`)

### 1.2 Obtenir l'URL de connexion
```
postgres://neondb_owner:PASSWORD@ep-XXXX.neon.tech/neondb?sslmode=require
```

Copier cette URL complète → vous la besoin plus tard !

---

## 💻 ÉTAPE 2 : Configuration Locale et Test

### 2.1 Cloner et installer
```bash
git clone https://github.com/DAVY2603/Medusa.git
cd Medusa
npm install
```

### 2.2 Configurer les variables d'environnement
```bash
# Copier le fichier exemple
cp .env.example .env.local

# Éditer .env.local avec votre éditeur
# Remplacer DATABASE_URL par l'URL Neon
# Remplacer DATABASE_URL=postgresql://...
```

**Exemple de .env.local :**
```env
DATABASE_URL=postgresql://neondb_owner:myPassword@ep-abc123.neon.tech/neondb?sslmode=require
NODE_ENV=development
JWT_SECRET=super_secret_key_12345
MEDUSA_ADMIN_SECRET=admin_secret_67890
STORE_URL=http://localhost:3000
ADMIN_URL=http://localhost:3000/admin
```

### 2.3 Tester en local
```bash
# Lancer les migrations de BD
npm run migrate

# Démarrer le serveur de développement
npm run dev

# Vérifier : http://localhost:3000
```

Si tout fonctionne ✅ → Vous pouvez déployer !

---

## 🚀 ÉTAPE 3 : Déployer sur Vercel

### Option A : Déploiement via Interface Vercel (Recommandé)

1. **Aller sur** https://vercel.com/new
2. **Cliquer** "Import Git Repository"
3. **Chercher** et sélectionner `DAVY2603/Medusa`
4. **Configurer le projet :**
   - Framework Preset : `Other` (Medusa n'est pas dans les presets)
   - Build Command : `npm run build`
   - Output Directory : `.medusa/server`
   - Install Command : `npm install`

5. **Ajouter les variables d'environnement** (cliquer "Environment Variables") :
   ```
   DATABASE_URL = postgresql://...
   JWT_SECRET = votre_clé_secrète
   MEDUSA_ADMIN_SECRET = votre_secret_admin
   NODE_ENV = production
   MEDUSA_ADMIN_ONBOARDING_DISABLED = true
   ```

6. **Cliquer "Deploy"** et attendre 3-5 minutes

✅ Votre site est en ligne ! URL : `https://medusa-XXX.vercel.app`

---

### Option B : Déploiement via Vercel CLI

```bash
# 1. Installer Vercel CLI
npm i -g vercel

# 2. Se connecter à Vercel
vercel login

# 3. Déployer en production
vercel --prod

# 4. Ajouter les env vars quand demandé
```

---

## 🔐 ÉTAPE 4 : Sécurité et Variables d'Environnement

⚠️ **IMPORTANT** : Ne JAMAIS commiter `.env.local` sur GitHub !

Vérifiez que `.env.local` est dans `.gitignore` :
```bash
echo ".env.local" >> .gitignore
```

Les variables d'env doivent être ajoutées **UNIQUEMENT** dans Vercel Dashboard :
1. Projet → Settings → Environment Variables
2. Ajouter chaque variable

---

## 🧪 ÉTAPE 5 : Tests Post-Déploiement

### 5.1 Vérifier que le serveur fonctionne
```bash
curl https://votre-app.vercel.app/health
```

### 5.2 Accéder à Medusa Admin
```
https://votre-app.vercel.app/admin
```

### 5.3 Consulter les logs
```bash
vercel logs https://votre-app.vercel.app --tail
```

---

## 📊 Coûts (GRATUIT pour tester)

| Service | Plan Gratuit | Prix |
|---------|-------------|------|
| **Vercel** | Illimité | GRATUIT |
| **Neon PostgreSQL** | 0.5 compute credits + 3 GB | GRATUIT |
| **Bandwidth** | 100 GB/mois | GRATUIT |
| **Uptime** | 99.9% | GRATUIT |

**Total = 0€ pour tester ! 🎉**

---

## 🆘 Troubleshooting Courant

### ❌ Erreur : "Database connection failed"
```bash
# Vérifier DATABASE_URL dans Vercel Settings
# Assurez-vous que Neon IP est whitelisted
```

### ❌ Erreur : "Build failed"
```bash
# Vérifier les logs
vercel logs https://votre-app.vercel.app --tail

# Relancer la build
vercel redeploy
```

### ❌ Admin ne s'affiche pas
```bash
# Vérifier que MEDUSA_ADMIN_ONBOARDING_DISABLED = true
# Attendre 5min après le déploiement
```

### ❌ Timeout sur migration
```bash
# Augmenter le timeout dans Vercel settings
# Functions → Max Duration : 60 secondes
```

---

## 📈 Prochaines Étapes Après Déploiement

1. **Domaine personnalisé**
   - Vercel → Settings → Domains
   - Ajouter `votresite.com`

2. **SSL/HTTPS**
   - Automatique avec Vercel ✅

3. **Analytics**
   - Vercel Dashboard → Analytics

4. **Sauvegardes BD**
   - Neon Console → Backups

5. **Ajouter des produits**
   - Admin → Products → Create

---

## 🔗 Liens Utiles

- **Medusa Docs** : https://docs.medusajs.com
- **Vercel Docs** : https://vercel.com/docs
- **Neon Docs** : https://neon.tech/docs
- **Support Medusa** : https://discord.gg/medusa

---

## ✅ Vous êtes Prêt !

Suivez les étapes ci-dessus et votre B2B Medusa sera en ligne en 15 minutes !

**Questions ?** Consultez les logs ou relancez le processus.

Bonne chance ! 🚀
