# Evidência E00.1 — Ambiente reprodutível

## Prova de reprodutibilidade

```bash
Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ rm -rf node_modules

Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ pnpm install --frozen-lockfile
✓ Lockfile passes supply-chain policies (verified 1h ago)
Lockfile is up to date, resolution step is skipped
Packages: +1
+
Packages are hard linked from the content-addressable store to the virtual store.
  Content-addressable store is at: C:\Users\Felipe\AppData\Local\pnpm\store\v11
  Virtual store is at:             node_modules/.pnpm
Progress: resolved 1, reused 1, downloaded 0, added 1, done

devDependencies:
+ prettier 3.9.6

Done in 517ms using pnpm v11.23.0

Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ git status --short
?? evidencias/

Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$


```

## Link permanente para o .gitignore
[Colocaremos o link aqui no próximo passo]

## Por que o pnpm-lock.yaml é versionado e o node_modules/ não?
O `pnpm-lock.yaml` é versionado porque ele trava as versões exatas de cada dependência, garantindo que o ambiente seja 100% reprodutível em qualquer máquina (evitando bugs de versões diferentes). Já a pasta `node_modules/` não é versionada porque é extremamente pesada (milhares de arquivos), contém binários específicos do sistema operacional de quem instalou e pode ser facilmente gerada a partir do lockfile.