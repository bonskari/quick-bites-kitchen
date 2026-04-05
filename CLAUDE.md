# Neat Bites Kitchen

Reseptisivusto — kitchen.neatbites.com. S3-hosted.

## Konsepti
Joka päivä yksi uusi resepti. AI generoi reseptin, kuvan ja sivun automaattisesti. Adsense-mainokset.

## Nykytila
- 60+ staattista HTML-reseptisivua
- S3:ssä kitchen.neatbites.com
- Cloudflare Web Analytics (token: ca751ef6b3ff457996e47820f2d45920)
- Kuvat mukana (375 MB)

## Tavoite: Data-driven Astro-sivusto (kuten reviewofareview.com)

### Vaihe 1: Migraatio Astroon
- Konvertoi nykyiset 60+ reseptit JSON-tiedostoiksi `src/content/recipes/`
- Astro content collections, glob loader
- Yksi layout, yksi reseptisivu-template
- Etusivu: grid-näkymä resepteistä kuvilla
- Kategoriat: quick meals, air fryer, desserts, soups, bowls, pasta
- GitHub Actions deploy → S3

### Resepti-dataformaatti
```json
{
  "title": "Creamy Tuscan Salmon",
  "slug": "creamy-tuscan-salmon",
  "date": "2026-04-06",
  "category": "quick-meals",
  "prep_time": 5,
  "cook_time": 15,
  "servings": 2,
  "difficulty": "easy",
  "image": "creamy-tuscan-salmon.jpg",
  "description": "Restaurant-quality salmon in 15 minutes...",
  "ingredients": ["2 salmon fillets", "1 cup sun-dried tomatoes", ...],
  "steps": ["Season salmon...", "Sear in hot pan...", ...],
  "nutrition": {"calories": 450, "protein": 35, ...},
  "tags": ["salmon", "15-minute", "high-protein", "keto"]
}
```

### Vaihe 2: Automaattinen reseptigenerointi
- Project-manager scraper: `scrapers/kitchen-content/run.sh`
- AI generoi reseptin (Claude/Ollama)
- Kuva generoidaan ComfyUI:lla serverillä (FLUX 2 Klein)
- Committaa JSON + kuva repoon → GitHub Actions deploy
- 1 uusi resepti/päivä

### Vaihe 3: Markkinointi
- Project-managerissa `kitchen-marketing` projekti
- Reddit: r/cooking, r/recipes, r/mealprep, r/EatCheapAndHealthy
- Mastodon, Pinterest (visuaalinen — reseptikuvat)
- SEO: recipe structured data (schema.org/Recipe)

### Vaihe 4: Monetisointi
- Google Adsense (lisätty jo)
- Affiliate-linkit keittiövälineisiin (Amazon)
- Recipe schema.org → Google Rich Results

## Tekniikka
- Astro v5 (SSG)
- S3 hosting (kitchen.neatbites.com bucket)
- GitHub Actions deploy joka pushilla
- ComfyUI (FLUX 2 Klein) kuvageneraatio serverillä
- Cloudflare Web Analytics

## Säännöt
- Reseptien PITÄÄ olla oikeita ja toimivia
- Kuvat generoidaan AI:lla — ei varastettuja kuvia
- ÄLÄ julkaise ilman kuvaa
- Adsense-koodi jokaisella sivulla
- Brändi: Neat Bites Kitchen (neatbites.com subdomain)
