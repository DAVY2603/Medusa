# Déploiement Gratuit Medusa - Comparatif des Plateformes

## 🎯 Résumé Rapide

| Plateforme | Gratuit | Base de Données | Facilité | Idéal pour |
|-----------|---------|-----------------|---------|-----------|
| **Render** | ✅ Oui | PostgreSQL | ⭐⭐⭐⭐⭐ | Medusa Backend |
| **Railway** | ✅ Oui (crédit) | PostgreSQL | ⭐⭐⭐⭐⭐ | Déploiement rapide |
| **Fly.io** | ✅ Oui (crédit) | Non inclus | ⭐⭐⭐⭐ | Edge computing |
| **Heroku** | ❌ Non | ❌ Payant | ⭐⭐⭐⭐ | Production simple |
| **Vercel** | ✅ Oui | Non inclus | ⭐⭐⭐⭐⭐ | Frontend Next.js |
| **Netlify** | ✅ Oui | Non inclus | ⭐⭐⭐⭐⭐ | Frontend JAMstack |

---

## 🚀 Architecture Recommandée (100% Gratuit)

```
┌─────────────────────────────────────────┐
│    Frontend (Vercel) - GRATUIT           │
│    https://shop.yourdomain.com           │
└──────────────────┬──────────────────────┘
                   │
┌──────────────────▼──────────────────────┐
│    API Medusa (Render) - GRATUIT         │
│    https://api.yourdomain.com            │
└──────────────────┬──────────────────────┘
                   │
┌──────────────────▼──────────────────────┐
│  Base de Données (Render PostgreSQL)     │
│           - GRATUIT -                    │
└─────────────────────────────────────────┘
```

---

## 📋 Option 1: RENDER (⭐ RECOMMANDÉ)

### Avantages
✅ PostgreSQL gratuit inclus  
✅ Déploiement ultra-simple depuis GitHub  
✅ SSL/HTTPS automatique  
✅ Support Node.js natif  
✅ Interface intuitive  

### Inconvénients
❌ Mise en veille après 15 min sans activité (plan gratuit)  
❌ Ressources limitées (0.5 GB RAM)  

### 🔧 Déploiement en 5 Min

**1. Créer un compte**: https://render.com/register

**2. Créer PostgreSQL**:
- Dashboard > New + > PostgreSQL
- Copier DATABASE_URL

**3. Créer Redis** (optionnel):
- Dashboard > New + > Redis
- Copier REDIS_URL

**4. Créer Web Service**:
- Dashboard > New + > Web Service
- Connecter votre repo GitHub
- Build: `npm install && npm run build`
- Start: `npm start`

**5. Ajouter variables d'env**:
```env
DATABASE_URL=your_render_postgres_url
JWT_SECRET=your_secret
NODE_ENV=production
```

**6. Déployer** ✅

---

## 📋 Option 2: RAILWAY (⭐⭐ TRÈS SIMPLE)

### Avantages
✅ Interface graphique très intuitive  
✅ PostgreSQL + Redis gratuits  
✅ Crédit gratuit $5/mois  
✅ Déploiement avec 1 clic  

### Inconvénients
❌ Crédit épuisable  
❌ Payant après épuisement du crédit  

### 🔧 Déploiement

**1. Aller sur**: https://railway.app/register

**2. Connecter GitHub**

**3. Créer New Project > Deploy from GitHub**

**4. Railway crée automatiquement**:
- Service Node.js
- PostgreSQL
- Redis (optionnel)
- Variables d'environnement

**5. C'est tout!** ✅ L'app se déploie automatiquement

---

## 📋 Option 3: FLY.IO (⭐⭐⭐ EDGE COMPUTING)

### Avantages
✅ Hébergement dans le monde entier (edge)  
✅ Crédit gratuit $25/mois  
✅ Très rapide  
✅ Support Docker natif  

### Inconvénients
❌ Pas de PostgreSQL gratuit (à ajouter)  
❌ Plus technique  

### 🔧 Déploiement

```bash
# 1. Installer Fly CLI
curl -L https://fly.io/install.sh | sh

# 2. Se connecter
fly auth login

# 3. Lancer l'app
fly launch

# 4. Déployer
fly deploy
```

---

## 🌐 Frontend Gratuit (Vercel ou Netlify)

### VERCEL (Recommandé pour Next.js)

```bash
# 1. Connecter GitHub
# 2. Sélectionner repo
# 3. Vercel déploie automatiquement

# Votre site: https://yourproject.vercel.app
```

### NETLIFY (Recommandé pour Static Sites)

```bash
# 1. Connecter GitHub
# 2. Sélectionner repo
# 3. Netlify déploie automatiquement

# Votre site: https://yourproject.netlify.app
```

---

## 💾 Base de Données Gratuite

### Render PostgreSQL (Gratuit)
```
- 5 GB storage
- Parfait pour dev/test
- Inclus avec le plan gratuit Render
```

### Railway PostgreSQL (Gratuit)
```
- Crédit $5/mois
- Bases de données illimitées
- Très généreux
```

### Supabase (Gratuit)
```
- 500 MB storage
- PostgreSQL + Auth
- Parfait pour prototypage
```

---

## 🎯 Étapes de Déploiement Complet

### ÉTAPE 1: Préparer le Repo (Local)

```bash
# 1. Initialiser Medusa
medusa new medusa-b2b --seed

# 2. Ajouter fichier render.yaml
cat > render.yaml << 'EOF'
services:
  - type: web
    name: medusa-api
    env: node
    plan: free
    buildCommand: npm install && npm run build
    startCommand: npm start
    envVars:
      - key: NODE_ENV
        value: production
EOF

# 3. Pousser sur GitHub
git add .
git commit -m "Initial Medusa setup"
git push origin main
```

### ÉTAPE 2: Créer les Services (Render)

```bash
# 1. Aller sur render.com
# 2. Créer PostgreSQL
# 3. Créer Redis (optionnel)
# 4. Créer Web Service (connecter GitHub)
# 5. Ajouter les variables d'env
```

### ÉTAPE 3: Initialiser la BD

```bash
# Dans le Shell Render:
npm run build
npx medusa db:migrate
npx medusa user:create
```

### ÉTAPE 4: Vérifier

```bash
# Tester l'API
curl https://medusa-api-xxxx.onrender.com/admin/health

# Accéder à l'admin
https://medusa-api-xxxx.onrender.com/admin
```

---

## ⚙️ Garder le Service Actif (Render)

Le plan gratuit Render met le service en veille après 15 min.

### Solution 1: Cron Job (EasyCron)

1. Aller sur https://www.easycron.com
2. Créer cron:
   - URL: `https://medusa-api-xxx.onrender.com/admin/health`
   - Fréquence: Toutes les 10 min

### Solution 2: GitHub Actions

```yaml
name: Keep Render Alive
on:
  schedule:
    - cron: '*/10 * * * *'
jobs:
  ping:
    runs-on: ubuntu-latest
    steps:
      - run: curl https://medusa-api-xxx.onrender.com/admin/health
```

---

## 💰 Coûts

### 100% Gratuit
- Render Web (0.5 GB) - Gratuit
- Render PostgreSQL (5 GB) - Gratuit
- Vercel/Netlify Frontend - Gratuit
- **Total: 0€/mois** ✅

### Petit Budget (~$10/mois)
- Railway Starter + PostgreSQL - $10
- Vercel Pro - $20 (optionnel)
- **Total: ~$10-30/mois**

### Production (~$30-50/mois)
- Render Starter - $7
- Railway Standard - $20
- CDN (Cloudflare) - Gratuit
- **Total: ~$27-50/mois**

---

## ✅ Checklist Déploiement

- [ ] Créer compte Render/Railway
- [ ] Créer PostgreSQL
- [ ] Créer Redis (optionnel)
- [ ] Créer Web Service
- [ ] Configurer variables d'env
- [ ] Initialiser base de données
- [ ] Créer utilisateur admin
- [ ] Tester l'API
- [ ] Déployer frontend
- [ ] Configurer domaine personnalisé
- [ ] Ajouter SSL/HTTPS
- [ ] Configurer cron job (keep-alive)
- [ ] Sauvegardes activées

---

## 🚨 Passer de Gratuit à Production

Quand vous aurez besoin de fiabilité:

1. **Render Starter** (~$7/mois)
   - Pas de mise en veille
   - 0.5 vCPU, 1 GB RAM
   - 10 GB SSD

2. **Dedicated PostgreSQL** (~$15/mois)
   - Base de données performante
   - Backups automatiques
   - 1 vCPU, 1 GB RAM

3. **Domaine personnalisé**
   - https://yourdomain.com (payant)
   - SSL/HTTPS gratuit (Let's Encrypt)

---

## 📞 Support

- **Render**: https://render.com/docs
- **Railway**: https://docs.railway.app
- **Fly.io**: https://fly.io/docs
- **Medusa**: https://docs.medusajs.com/deployment

---

**Prêt à déployer?** Choisissez **Render** pour commencer! 🚀
