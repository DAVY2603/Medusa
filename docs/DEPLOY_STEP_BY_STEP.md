# Guide Étape par Étape - Déploiement Render (15 minutes)

## 🚀 DÉPLOIEMENT EN 15 MINUTES

### ÉTAPE 1: Préparation GitHub (5 min)

#### 1.1 Pousser le code sur GitHub

```bash
cd medusa-b2b
git add .
git commit -m "Initial Medusa B2B setup"
git push origin main
```

#### 1.2 Vérifier que tout est sur GitHub

Aller sur: `https://github.com/DAVY2603/Medusa`

Vérifier les fichiers:
- ✅ `render.yaml`
- ✅ `package.json`
- ✅ `.env.example`
- ✅ `Dockerfile`

---

### ÉTAPE 2: Créer Compte Render (2 min)

#### 2.1 S'inscrire

1. Aller sur: https://render.com/register
2. Cliquer "Sign up with GitHub"
3. Autoriser Render
4. Confirmer l'email

#### 2.2 Créer un nouveau projet

Dashboard > New + > Web Service

---

### ÉTAPE 3: Créer la Base de Données PostgreSQL (3 min)

#### 3.1 Créer PostgreSQL

1. Render Dashboard > New +
2. Sélectionner **PostgreSQL**
3. Configuration:
   ```
   Name: medusa-postgres
   Database: medusa_b2b
   User: medusa_user
   Region: Frankfurt (Europe)
   Plan: Free
   ```
4. Cliquer **Create Database**
5. **COPIER** le `Database URL` (ressemble à):
   ```
   postgresql://medusa_user:xxxxx@xxx.onrender.com/medusa_b2b
   ```

---

### ÉTAPE 4: Créer Redis (2 min)

#### 4.1 Créer Redis

1. Render Dashboard > New +
2. Sélectionner **Redis**
3. Configuration:
   ```
   Name: medusa-redis
   Region: Frankfurt (Europe)
   Plan: Free
   ```
4. Cliquer **Create Redis**
5. **COPIER** la `Redis URL` (ressemble à):
   ```
   redis://xxxxx:xxxxx@xxx.onrender.com:xxxxx
   ```

---

### ÉTAPE 5: Créer le Service Web API (3 min)

#### 5.1 Connecter GitHub

1. Render Dashboard > New +
2. Sélectionner **Web Service**
3. Cliquer **Connect a repository**
4. Sélectionner votre repo: `DAVY2603/Medusa`
5. Cliquer **Connect**

#### 5.2 Configurer le Service

```
Name: medusa-api
Environment: Node
Region: Frankfurt (Europe)
Branch: main
Build Command: npm install && npm run build
Start Command: npm start
Plan: Free (IMPORTANT!)
```

#### 5.3 Ajouter les Variables d'Environnement

1. Aller à **Environment** dans le service
2. Ajouter les variables (copier/coller):

```env
DATABASE_URL=postgresql://medusa_user:PASSWORD@HOSTNAME/medusa_b2b
REDIS_URL=redis://USERNAME:PASSWORD@HOSTNAME:PORT
JWT_SECRET=medusa_jwt_secret_key_change_this_in_production_123456
NODE_ENV=production
PORT=10000
MEDUSA_ADMIN_BACKEND_URL=https://medusa-api-xxxxx.onrender.com
SENDGRID_FROM=support@medusa-b2b.com
LOG_LEVEL=info
```

**Remplacer les valeurs**:
- `DATABASE_URL` → Coller la PostgreSQL URL de l'étape 3.2
- `REDIS_URL` → Coller la Redis URL de l'étape 4.1
- `JWT_SECRET` → Générer une clé aléatoire (au moins 32 caractères)
- `medusa-api-xxxxx` → Remplacer par votre nom de service

#### 5.4 Cliquer **Deploy**

Le déploiement commence! ⏳ (Attend 2-3 min)

---

### ÉTAPE 6: Initialiser la Base de Données (2 min)

#### 6.1 Ouvrir le Shell Render

1. Sur la page du service `medusa-api`
2. Cliquer l'onglet **Shell**

#### 6.2 Exécuter les commandes d'initialisation

Copier/coller dans le Shell:

```bash
npm run build
npx medusa db:migrate
```

Attendre que ce soit terminé ✅

#### 6.3 Créer l'Utilisateur Admin

```bash
npx medusa user:create
```

Entrer:
- **Email**: `admin@medusa-b2b.com`
- **Password**: `VotreMotDePasse123!`

(Garder ces identifiants!)

---

### ÉTAPE 7: Vérifier le Déploiement (1 min)

#### 7.1 Tester l'API

Ouvrir dans le navigateur:
```
https://medusa-api-xxxxx.onrender.com/admin/health
```

Vous devriez voir:
```json
{"status":"ok"}
```

#### 7.2 Accéder à l'Admin Medusa

1. Aller à: `https://medusa-api-xxxxx.onrender.com/admin`
2. Se connecter avec:
   - Email: `admin@medusa-b2b.com`
   - Password: `VotreMotDePasse123!`

3. Vous voyez le dashboard Medusa ✅

---

## 📋 CONFIGURATION APRÈS DÉPLOIEMENT

### 1️⃣ Configurer les Paramètres du Magasin

Dans l'Admin Medusa:
1. **Paramètres > Magasin**
2. Remplir:
   ```
   Nom: Medusa B2B
   Support Email: support@medusa-b2b.com
   Devise: EUR
   Fuseau horaire: Europe/Paris
   ```
3. Sauvegarder

### 2️⃣ Ajouter une Région (France)

1. **Paramètres > Régions > Ajouter Région**
2. Configurer:
   ```
   Nom: France
   Pays: France
   Devise: EUR
   ```
3. Sauvegarder

### 3️⃣ Ajouter des Catégories de Produits

1. **Catalogue > Catégories > Créer**
2. Ajouter catégories:
   - Électronique
   - Fournitures
   - Services

### 4️⃣ Ajouter un Premier Produit

1. **Catalogue > Produits > Ajouter**
2. Remplir:
   ```
   Titre: Produit Test
   Description: Description test
   Catégorie: Électronique
   Prix: 99.99 EUR
   Stock: 100
   ```
3. Publier

---

## 🔧 GARDER LE SERVICE ACTIF

Le plan gratuit met le service en veille après 15 min sans trafic.

### Option 1: Cron Job (Recommandé)

#### A. Utiliser EasyCron (Gratuit)

1. Aller sur: https://www.easycron.com/register
2. S'inscrire
3. Créer un cron job:
   ```
   HTTP Method: GET
   URL: https://medusa-api-xxxxx.onrender.com/admin/health
   Cron Expression: */10 * * * *  (toutes les 10 min)
   Timezone: Europe/Paris
   ```
4. Sauvegarder

### Option 2: GitHub Actions (Automatique)

Les fichiers `.github/workflows/keep-alive.yml` est déjà créé.

Activer:
1. Aller sur votre repo GitHub
2. Onglet **Actions**
3. Le workflow `Keep Render API Alive` doit être actif ✅

---

## 🌐 DÉPLOYER LE FRONTEND (Vercel)

### Étape 1: Créer un Repo Frontend

```bash
# Créer un nouveau projet Next.js Medusa
npx create-next-app@latest medusa-storefront --typescript

cd medusa-storefront

# Installer Medusa SDK
npm install @medusajs/medusa-js
```

### Étape 2: Configurer l'API

Créer `.env.local`:

```env
NEXT_PUBLIC_MEDUSA_BACKEND_URL=https://medusa-api-xxxxx.onrender.com
```

### Étape 3: Déployer sur Vercel

1. Pousser le code sur GitHub:
   ```bash
   git add .
   git commit -m "Initial storefront"
   git push origin main
   ```

2. Aller sur: https://vercel.com/new
3. Connecter le repo frontend
4. Vercel déploie automatiquement ✅

Votre site: `https://medusa-storefront.vercel.app`

---

## ✅ CHECKLIST FINAL

- [ ] Compte Render créé
- [ ] PostgreSQL déployé
- [ ] Redis déployé
- [ ] Web Service déployé
- [ ] Variables d'env configurées
- [ ] BD initialisée
- [ ] Admin accessible
- [ ] Produit test créé
- [ ] Cron job configuré
- [ ] Frontend déployé (optionnel)

---

## 🎉 VOUS AVEZ UNE PLATEFORME B2B EN LIGNE!

**API Médusa**: https://medusa-api-xxxxx.onrender.com  
**Admin Panel**: https://medusa-api-xxxxx.onrender.com/admin  
**Frontend**: https://medusa-storefront.vercel.app (optionnel)  

---

## 🆘 DÉPANNAGE

### Q: "Application Error - H13"
**R**: Le service démarre. Attendre 1-2 min et rafraîchir.

### Q: "Database connection error"
**R**: Vérifier DATABASE_URL dans les variables d'env.

### Q: "Cannot find module"
**R**: Exécuter dans le Shell Render:
```bash
npm install
npm run build
```

### Q: Le service s'arrête après 15 min
**R**: C'est normal (plan gratuit). Ajouter le cron job EasyCron.

---

## 📞 SUPPORT

- **Render Docs**: https://render.com/docs
- **Medusa Docs**: https://docs.medusajs.com
- **Discord Medusa**: https://discord.gg/medusajs

---

**🎊 Félicitations! Votre plateforme B2B est en ligne!**
