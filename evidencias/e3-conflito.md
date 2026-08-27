# Evidência E00.3 — Conflito de merge
**1. Saída do git merge que acusou o conflito:**
```bash
Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ git merge feat/titulo-b
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```
**2. Conteúdo do arquivo durante o conflito (com os marcadores):**
```markdown
# Titulo da Versao A
```
**3. Saída do `git log --graph --oneline --all`:**
```bash
Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ git log --graph --oneline --all
*   553a5d5 (HEAD -> main) docs: resolve conflito mantendo a versao A
|\  
| * 8d871d3 (feat/titulo-b) docs: altera titulo para versao B
* | 2f8a310 (feat/titulo-a) docs: altera titulo para versao A
|/  
* 2bc5786 docs: cria README na raiz
* a2358d7 docs: adiciona evidencia de arqueologia de historico (E00.2)
* a5e2b34 docs: adiciona evidencia de ambiente reprodutivel (E00.1)
* 78b9288 chore: configuracao inicial do ambiente reprodutivel
```

**4. Por que o Git não conseguiu resolver sozinho?**
O Git não conseguiu resolver o merge sozinho porque houve alterações concorrentes na mesma linha do mesmo arquivo (README.md). Como a branch atual (`main`) e a branch (`feat/titulo-b`) modificaram a linha 1 simultaneamente, o Git não sabe qual versão priorizar, pausando o processo para exigir a resolução manual do desenvolvedor (linhas alteradas em ambos os lados).

**5. Links Permanentes:**
- Link do commit de merge: 553a5d5f027f2c030571fa9a91f19dd08bde2a4b
- Link do Network: https://github.com/lFelipe23/dpw-exercicios.git/network