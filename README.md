# OPENEINSTEIN-
openEinstein est une plateforme numérique libre et collaborative destinée aux chercheurs, étudiants et innovateurs. Elle combine une bibliothèque ouverte de publications scientifiques (PDF), un système de résumés intelligents avec mots-clés, et un espace de dépôt de projets logiciels et codes open-source. 
<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>OpenEinstein – La science pour tous</title>
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@700&family=Roboto&display=swap" rel="stylesheet">
<style>
body { font-family: 'Roboto', sans-serif; margin:0; padding:0; background:#f4f4f4; color:#333; }
header { background:#1E90FF; color:white; padding:20px 0; text-align:center; }
header h1 { margin:0; font-family: 'Montserrat', sans-serif; font-size:2.5em; }
nav { display:flex; justify-content:center; background:#104E8B; flex-wrap: wrap; }
nav a { color:white; padding:15px 20px; text-decoration:none; }
nav a:hover { background:#1C86EE; }
main { padding:20px; max-width:1000px; margin:auto; }
.article, .article-detail { background:white; padding:15px; margin-bottom:15px; border-radius:12px; box-shadow:0 4px 8px rgba(0,0,0,0.1); transition: transform 0.2s; }
.article:hover { transform: scale(1.02); }
.article h3, .article-detail h3 { color:#1E90FF; }
.article p, .article-detail p { margin:5px 0; }
.btn { display:inline-block; padding:8px 15px; margin-right:10px; background:#FFD700; color:#104E8B; text-decoration:none; border-radius:5px; cursor:pointer; font-weight:bold; }
.btn:hover { background:#e6c200; }
footer { text-align:center; padding:15px; background:#ddd; margin-top:20px; border-top:1px solid #ccc; }
form input, form select, form textarea { width:100%; padding:10px; margin-bottom:10px; border-radius:5px; border:1px solid #ccc; }
form button { background:#FFD700; color:#104E8B; border:none; padding:10px 15px; border-radius:5px; cursor:pointer; font-weight:bold; }
form button:hover { background:#e6c200; }
.hidden { display:none; }
#searchInput { width:100%; padding:10px; margin-bottom:15px; border-radius:5px; border:1px solid #ccc; }
iframe { width:100%; height:400px; border:1px solid #ccc; border-radius:5px; margin-top:10px; }
@media (max-width: 768px) {
    nav { flex-direction: column; align-items: center; display:none; }
    nav.active { display:flex; }
    #menuButton { display:block; background:#104E8B; color:white; border:none; padding:10px 15px; margin:10px; border-radius:5px; cursor:pointer; font-weight:bold; }
}
</style>
</head>
<body>

<header>
<h1>🧪 OpenEinstein</h1>
<p>“La science pour tous – Étudiants et chercheurs”</p>
<button id="menuButton" onclick="toggleMenu()">☰ Menu</button>
</header>

<nav id="mainNav">
<a href="#home">Accueil</a>
<a href="#publish">Publier</a>
<a href="#articles">Articles</a>
<a href="#profile">Profil</a>
<a href="#about">À propos</a>
</nav>

<main id="home">
<h2>Derniers articles publiés</h2>
<input type="text" id="searchInput" placeholder="🔍 Rechercher par titre, auteur, ORCID, DOI ou mots-clés" onkeyup="filterArticles()">
<div id="articleContainer"></div>
</main>

<main id="publish">
<h2>Publier un article</h2>
<form id="publishForm">
<input type="text" placeholder="Nom" id="firstName" required>
<input type="text" placeholder="Prénom" id="lastName" required>
<input type="email" placeholder="Email académique" id="email" required>
<input type="text" placeholder="Titre de l’article" id="title" required>
<input type="text" placeholder="ORCID (ex : 0000-0002-1825-0097)" id="orcid" required>
<input type="text" placeholder="DOI (ex : 10.1234/openeinstein.2025.001)" id="doi" required>
<input type="text" placeholder="Mots-clés (séparés par virgule)" id="keywords" required>
<select id="category" required>
<option value="">Catégorie</option>
<option>Biologie</option>
<option>Chimie</option>
<option>Physique</option>
<option>Énergie</option>
<option>Médecine</option>
</select>
<textarea placeholder="Résumé de l’article" id="summary" rows="5" required></textarea>
<input type="file" id="pdfUpload" accept=".pdf" required>
<button type="submit">Publier</button>
</form>
<p id="successMsg" class="hidden" style="color:green; font-weight:bold;">Article publié avec succès ✅</p>
</main>

<main id="profile">
<h2>Profil Auteur</h2>
<p><strong>Nom complet :</strong> <span id="fullName">–</span></p>
<p><strong>Email :</strong> <span id="emailProfile">–</span></p>
<p><strong>ORCID :</strong> <span id="orcidProfile">–</span></p>
<p><strong>Articles publiés :</strong></p>
<ul id="profileArticles"></ul>
<p><strong>Gains cumulés :</strong> <span id="gains">0</span>$</p>
</main>

<main id="about">
<h2>À propos</h2>
<p>OpenEinstein libère la science :</p>
<ul>
<li>Accès gratuit pour tous</li>
<li>Système de récompense pour les auteurs</li>
<li>Contenus vérifiés et authentifiés</li>
<li>Articles avec Nom, Prénom, ORCID, DOI et mots-clés</li>
<li>Mission : “La science pour tous”</li>
</ul>
</main>

<footer>
&copy; 2025 OpenEinstein – Tous droits réservés
</footer>

<script>
const publishForm = document.getElementById('publishForm');
const successMsg = document.getElementById('successMsg');
const articleContainer = document.getElementById('articleContainer');
const profileArticles = document.getElementById('profileArticles');
const gainsDisplay = document.getElementById('gains');
const fullNameSpan = document.getElementById('fullName');
const emailProfile = document.getElementById('emailProfile');
const orcidProfile = document.getElementById('orcidProfile');

let totalGains = 0;
let articles = [];

function toggleMenu(){
    document.getElementById('mainNav').classList.toggle('active');
}

publishForm.addEventListener('submit', function(e){
    e.preventDefault();
    const firstName = document.getElementById('firstName').value;
    const lastName = document.getElementById('lastName').value;
    const email = document.getElementById('email').value;
    const title = document.getElementById('title').value;
    const orcid = document.getElementById('orcid').value;
    const doi = document.getElementById('doi').value;
    const keywords = document.getElementById('keywords').value;
    const category = document.getElementById('category').value;
    const summary = document.getElementById('summary').value;
    const pdfFile = document.getElementById('pdfUpload').files[0];

    if(!pdfFile){ alert("Veuillez uploader un PDF"); return; }

    const article = {firstName,lastName,email,title,orcid,doi,keywords,category,summary,pdfURL:URL.createObjectURL(pdfFile),views:0,gains:0};
    articles.push(article);
    renderArticles();
    updateProfile(firstName,lastName,email,orcid);
    successMsg.classList.remove('hidden');
    setTimeout(()=>{ successMsg.classList.add('hidden'); },3000);
    publishForm.reset();
});

function renderArticles(){
    articleContainer.innerHTML='';
    articles.forEach((art,index)=>{
        const div = document.createElement('div');
        div.className='article';
        div.innerHTML=`
        <h3>${art.title}</h3>
        <p><strong>Auteur :</strong> ${art.firstName} ${art.lastName} | <strong>Catégorie :</strong> ${art.category}</p>
        <p><strong>ORCID :</strong> ${art.orcid} | <strong>DOI :</strong> ${art.doi}</p>
        <p><strong>Mots-clés :</strong> ${art.keywords}</p>
        <p><strong>Résumé :</strong> ${art.summary}</p>
        <iframe src="${art.pdfURL}" type="application/pdf"></iframe>
        <p><strong>Vues :</strong> ${art.views} | <strong>Soutiens :</strong> ${art.gains}$</p>
        <button class="btn" onclick="downloadArticle(${index})">📄 Télécharger</button>
        <button class="btn" onclick="donAuteur(${index},5)">💰 Soutenir l’auteur</button>
        `;
        articleContainer.appendChild(div);
    });
}

function downloadArticle(index){
    articles[index].views += 1;
    renderArticles();
    window.open(articles[index].pdfURL, "_blank");
}

function donAuteur(index,amount){
    articles[index].gains += amount;
    totalGains += amount;
    gainsDisplay.textContent = totalGains;
    renderArticles();
    alert(`Vous avez soutenu ${articles[index].firstName} ${articles[index].lastName} avec ${amount}$ 💰`);
}

function updateProfile(firstName,lastName,email,orcid){
    fullNameSpan.textContent = `${firstName} ${lastName}`;
    emailProfile.textContent = email;
    orcidProfile.textContent = orcid;

    profileArticles.innerHTML='';
    articles.forEach(art => {
        const li = document.createElement('li');
        li.textContent = `${art.title} – ${art.views} vues – ${art.gains}$ soutiens`;
        profileArticles.appendChild(li);
    });
}

function filterArticles(){
    const query = document.getElementById('searchInput').value.toLowerCase();
    const filtered = articles.filter(a =>
        a.title.toLowerCase().includes(query) ||
        a.firstName.toLowerCase().includes(query) ||
        a.lastName.toLowerCase().includes(query) ||
        a.orcid.toLowerCase().includes(query) ||
        a.doi.toLowerCase().includes(query)
