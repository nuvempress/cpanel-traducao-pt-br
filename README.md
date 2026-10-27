# cPanel — Tradução pt-BR

Tradução para o português do Brasil (`pt_br`) da interface do **cPanel**, **WHM** e **Webmail**, distribuída como um arquivo XML de locale pronto para importação no WHM.

> Projeto independente e não oficial. cPanel® e WHM® são marcas registradas de cPanel, L.L.C.

## Conteúdo do repositório

| Arquivo | Descrição |
|---|---|
| `pt_br_traduzida.xml` | Exportação de locale do cPanel (formato `perldata`, `struct_version` 1, locale `pt_br`), gerada em 21/10/2026. |
| `LICENSE` | Licença MIT. |

O XML reúne as traduções do locale base do cPanel, as personalizações locais do servidor e as strings dos plugins.

## Cobertura da tradução

**100% das 19.732 strings-fonte em inglês** (`/usr/local/cpanel/locale/en.yaml`) possuem tradução em pt-BR. Ao todo são **27.923 chaves únicas traduzidas** — as 8.191 adicionais correspondem a chaves legadas (`__legacy_*`) e a strings de plugins.

| Origem no XML | Chaves | Traduzidas | Cobertura |
|---|---:|---:|---:|
| `/usr/local/cpanel/locale/pt_br.yaml` (locale base) | 24.480 | 24.480 | 100% |
| `/var/cpanel/locale.local/pt_br.yaml` (personalizações locais) | 13.548 | 13.548 | 100% |
| Plugin `comet-backup` | 62 | 62 | 100% |
| Plugin `meridian` | 88 | 88 | 100% |
| Plugin `monitoring` | 62 | 62 | 100% |
| Plugin `sitejet` | 141 | 141 | 100% |
| Plugin `webapp` | 77 | 77 | 100% |
| Plugin `xovi` | 11 | 11 | 100% |
| `queue/pending/machine/pt_br.yaml` | 3 | 3 | 100% |

O XML também contém as listas de referência `en.yaml` (strings-fonte) e `queue/pending.yaml` (fila de pendências, sem valores), que não são traduções.

## ⚠️ Antes de importar

**Teste primeiro em um servidor de homologação / sandbox / testes.** Não importe diretamente em produção. Depois da importação no ambiente de testes, navegue pelas principais telas do cPanel, WHM e Webmail com o idioma pt-BR e confirme que textos, variáveis (`[_1]`, `[numf,_1]` etc.) e formatação aparecem corretamente.

**Faça backup dos arquivos originais antes da importação**, tanto no ambiente de testes quanto em produção:

1. No WHM, acesse **Localization » Locale XML Download**, escolha `pt_br` e salve o XML atual do servidor.
2. Como `root`, copie os arquivos de locale existentes:

   ```bash
   cp -a /usr/local/cpanel/locale/pt_br.yaml /usr/local/cpanel/locale/pt_br.yaml.bak-$(date +%F)
   cp -a /var/cpanel/locale.local/pt_br.yaml /var/cpanel/locale.local/pt_br.yaml.bak-$(date +%F)
   ```

   (Se algum dos arquivos não existir, o comando apenas informará isso.)
3. Se possível, crie também um snapshot/backup completo do servidor.

**Para restaurar**, reimporte o XML salvo no passo 1 (pelo mesmo procedimento de importação abaixo) ou recoloque os arquivos `.yaml` copiados e reconstrua o cache de locale.

## Como usar o XML

### Pelo WHM (recomendado)

1. Baixe `pt_br_traduzida.xml` deste repositório.
2. No WHM, acesse **Localization » Locale XML Upload**.
3. Selecione o arquivo e envie. O WHM importa as traduções e reconstrói o locale.
4. Confira em **Localization » View Available Locales** que o `pt_br` está disponível.
5. Para usar o idioma:
   - **Padrão do servidor:** em **Server Configuration » Basic WebHost Manager® Setup**, defina o idioma padrão como Português (Brasil).
   - **Por usuário:** o usuário pode escolher o idioma em **Preferences » Change Language** no cPanel.

### Pela linha de comando (root)

```bash
# Envie o arquivo para o servidor
scp pt_br_traduzida.xml root@servidor:/root/

# No servidor: importe o locale e reconstrua o cache
/usr/local/cpanel/scripts/locale_import --locale=pt_br /root/pt_br_traduzida.xml
/usr/local/cpanel/bin/build_locale_databases --locale=pt_br
```

> Os nomes e as opções desses scripts podem variar entre versões do cPanel. Confira com `--help` antes de executar no seu servidor.

## Contribuindo

- Ajuste as traduções no WHM em **Localization » Edit a Locale** (no servidor de testes), exporte novamente via **Locale XML Download** e abra um pull request substituindo `pt_br_traduzida.xml`.
- Para correções pontuais, abra uma issue indicando a string original em inglês e a tradução sugerida.

## Licença

Distribuído sob a licença MIT. Veja [`LICENSE`](LICENSE).
