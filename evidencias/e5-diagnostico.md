# Evidência E00.5 — Roteiro de diagnóstico

**Problema:** "Instalei o pacote, mas o import fala que não existe."

## Roteiro de Diagnóstico (Exemplo genérico / Node.js)

| # | Comando | Se a saída for X | Então |
|---|---|---|---|
| 1 | `ls package.json` | `No such file or directory` (Você não está na pasta do projeto). | Dê `cd` até a pasta raiz correta onde o projeto foi criado. |
| 2 | `cat package.json` | O nome do pacote não aparecer na seção `dependencies`. | O pacote não foi salvo. Rode a instalação novamente. |
| 3 | `ls node_modules` | `No such file or directory` (A pasta física foi deletada ou não baixou). | Rode o comando de instalação raiz para restaurar os arquivos. |
| 4 | `grep "nome-do-pacote" index.js` | O nome do pacote estiver com erro de digitação no código fonte. | Corrija a sintaxe diretamente na linha do `import`. |

## Prova de Execução

**Simulação:** Entrando em um subdiretório por engano e aplicando o Passo 1 do diagnóstico.

```bash
Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ echo "{}" > package.json

Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios (main)
$ cd evidencias

Felipe@Monarca01 MINGW64 ~/dev/dpw-exercicios/evidencias (main)
$ ls package.json
ls: cannot access 'package.json': No such file or directory
```