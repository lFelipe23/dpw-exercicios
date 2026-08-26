# Evidência E00.2 — Arqueologia de histórico

**1. Quantos commits o repositório tem?**
*Adicionei o `HEAD` ao comando para indicar que a contagem deve considerar todo o histórico começando do ponto atual*
```bash
Felipe@Monarca01 MINGW64 /tmp/nest (master)
$ git rev-list --count HEAD
21672
```
**2. Qual foi o primeiro commit, e em que data?**
```bash
Felipe@Monarca01 MINGW64 /tmp/nest (master)
$ git log --reverse
commit f7c8d10fb20943bc7102c73d5ecbe49e6c0b5ea1
Author: kamil.mysliwiec <kamil.mysliwiec@frogriot.com>
Date:   Sun Jan 8 15:09:41 2017 +0100

    Initial commit
```
**3. Quem mais modificou packages/core/injector/injector.ts?**
*Adicionei o caminho packages/core/injector/injector.ts no final para forçar o shortlog a filtrar e contar apenas os autores deste arquivo específico*
```bash
Felipe@Monarca01 MINGW64 /tmp/nest (master)
$ git shortlog -sn -- packages/core/injector/injector.ts
    90  Kamil Myśliwiec
```
**4. O que mudou no último commit que tocou esse arquivo?**
*Para chegar nesse resultado, primeiramente rodei `git log -1 --oneline -- e o caminho` (adicionando `-1` para limitar a busca a apenas um resultado) para descobrir o hash do último commit. Com o hash em mãos, rodei o `git show` abaixo, adicionando esse hash e o caminho do arquivo para exibir o diff.*
```bash
Felipe@Monarca01 MINGW64 /tmp/nest (master)
$ git show 45485b542 -- packages/core/injector/injector.ts
commit 45485b54210e06a517c1ebf86b42b1ea99fc3fe2
Author: Kamil Myśliwiec <mail@kamilmysliwiec.com>
Date:   Tue Aug 25 12:48:22 2026 +0200

    fix(core): circular durable providers issue #17562
@@ -589,6 +589,20 @@ export class Injector {
           .catch(err => {
             instanceWrapper.settlementSignal?.error(err);
           });
+      } else {
+        /**
+         * No load has ever been scheduled for this context (e.g., request-scoped
+         * providers are no longer instantiated during static bootstrap, so a fresh
+         * durable/request sub-tree host has no inherited `donePromise`).
+         * Load it now; if a circular dependency is truly in-flight, the nested
+         * lookup will find this host pending and defer through its `donePromise`.
+         */
+        await this.loadProvider(
+          instanceWrapper,
+          instanceWrapper.host ?? moduleRef,
+          resolutionContext,
+        );
+      }

```
**5. Quantos commits foram feitos nos últimos 90 dias?**
*Adicionei o valor "90 days ago" no parâmetro --since exigido para estipular o corte de tempo, e o HEAD para iniciar a contagem do momento atual.*
```bash
Felipe@Monarca01 MINGW64 /tmp/nest (master)
$ git rev-list --count --since="90 days ago" HEAD
697

Felipe@Monarca01 MINGW64 /tmp/nest (master)
$
```