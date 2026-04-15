Create a repo using GH cli: 
( verified that it is possible) 

gh api \
  --method POST \
  -H "Accept: application/vnd.github+json" \
  -H "X-GitHub-Api-Version: 2026-03-10" \
  /user/repos \
   -f 'name=infrastructure-ai-agent' -f 'description=ai agent to manage and create infrastructure' -f 'homepage=https://github.com' -F "private=false" -F 
"is_template=true"

Create a staging and production environment locally and push to environment can be done using well known CLI commands. 

Git checkout -b staging 
Git add example.py
Git commit -m “this is an example commit “ 
Git push -u origin staging 

Merging remote branches into staging or main:

Feature branch workflow (feature -> staging -> main)

1) Create a feature branch from staging

```bash
git checkout staging
git pull origin staging
git checkout -b feature/<short-feature-name>
```

2) Make changes and push the feature branch

```bash
git add .
git commit -m "feat: <describe the feature>"
git push -u origin feature/<short-feature-name>
```

3) Open a pull request from feature to staging

```bash
gh pr create \
  --base staging \
  --head feature/<short-feature-name> \
  --title "feat: <describe the feature>" \
  --body "Implements <feature details>."
```

4) Merge feature into staging after user approval

```bash
gh pr merge --merge --delete-branch
```

5) Open a pull request from staging to main

```bash
git checkout staging
git pull origin staging
git push origin staging

gh pr create \
  --base main \
  --head staging \
  --title "promote: staging to main" \
  --body "Promoting approved changes from staging to main."
```

6) Merge staging into main after final user approval

```bash
gh pr merge --merge
git checkout main
git pull origin main
```

