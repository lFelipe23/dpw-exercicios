# Evidência E00.4 — Desfazer sem pânico

| # | Cenário | Comando |
|---|---|---|
| 1 | Editei um arquivo e quero descartar a alteração (ainda não fiz `add`) | `git restore <arquivo>` |
| 2 | Fiz `git add` do arquivo errado e quero tirá-lo do stage | `git restore --staged <arquivo>` |
| 3 | A mensagem do último commit está errada (ainda não fiz push) | `git commit --amend -m "<nova mensagem>"` |
| 4 | Quero desfazer o último commit, mas manter as alterações no working directory | `git reset --soft HEAD~1` |
| 5 | Quero reverter um commit já enviado para o remoto | `git revert HEAD --no-edit` |
---

## Provas de Execução

### Caso 1: Descartar alteração não adicionada

**Antes:**
```bash
Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        evidencias/e4-desfazer.md

no changes added to commit (use "git add" and/or "git commit -a")
```
**Depois de rodar git restore README.md:**
```bash
Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        evidencias/e4-desfazer.md

nothing added to commit but untracked files present (use "git add" to track)
```

### Caso 2: Tirar do "Stage" (Desfazer o git add)

**Antes:**
```bash
Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        evidencias/e4-desfazer.md
```
**Depois de rodar git restore --staged README.md:**
```bash
Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        evidencias/e4-desfazer.md

no changes added to commit (use "git add" and/or "git commit -a")
```

### Caso 3: A mensagem do último commit está errada

**Antes:**
```bash
Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ git log --oneline -3
76f4f54 (HEAD -> main) docs: alterando o readme de forma erada
ec137e3 (origin/main) docs: preenche links permanentes no E00.1 e E00.3
5556826 docs: adiciona evidencia de conflito de merge (E00.3)
```

**Depois de rodar `git commit --amend -m "docs: altera o readme corretamente"`:**
```bash
Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ git log --oneline -3
1d76a0e (HEAD -> main) docs: altera o readme corretamente
ec137e3 (origin/main) docs: preenche links permanentes no E00.1 e E00.3
5556826 docs: adiciona evidencia de conflito de merge (E00.3)
```

### Caso 4: Desfazer o último commit mantendo as alterações

**Antes:**
```bash
Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ git log --oneline -2
1d76a0e (HEAD -> main) docs: altera o readme corretamente
ec137e3 (origin/main) docs: preenche links permanentes no E00.1 e E00.3
```

**Depois de rodar `git reset --soft HEAD~1`:**
```bash
Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ git log --oneline -2
ec137e3 (HEAD -> main, origin/main) docs: preenche links permanentes no E00.1 e E00.3
5556826 docs: adiciona evidencia de conflito de merge (E00.3)

Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        evidencias/e4-desfazer.md
```

### Caso 5: Reverter um commit já enviado para o remoto

**Antes:**
```bash
Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ git log --oneline -2
1b73566 (HEAD -> main, origin/main) commit que sera revertido
ec137e3 docs: preenche links permanentes no E00.1 e E00.3
```

**Depois de rodar `git revert HEAD --no-edit`:**
```bash
Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ git log --oneline -2
7afe5b6 (HEAD -> main) Revert "commit que sera revertido"
1b73566 (origin/main) commit que sera revertido
```