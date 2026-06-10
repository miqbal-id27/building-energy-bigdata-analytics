# Step-by-Step GitHub Portfolio Setup

## 1. Create repository

- Repository name: `building-energy-realtime-portfolio`
- Visibility: Public
- Initialize: leave empty if pushing this prepared package from local machine

## 2. MIT License

The package includes `LICENSE` with MIT License.

## 3. Structure

Use the prepared folder structure. Keep source notebooks in `notebooks/` and website pages in `docs/`.

## 4. Gitignore

The `.gitignore` excludes raw data, models, Spark checkpoints, virtual environments, and temporary files.

## 5. Convert notebooks

```bash
jupyter nbconvert --to html notebooks/*.ipynb --output-dir docs/notebooks
```

## 6. Push repository

```bash
git init
git branch -M main
git add .
git commit -m "Initial portfolio commit"
git remote add origin https://github.com/<your-github-username>/building-energy-realtime-portfolio.git
git push -u origin main
```

## 7. Enable Pages

GitHub repository → Settings → Pages → Deploy from a branch → `main` → `/docs`.
