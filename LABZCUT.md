# LabzCut

LabzCut é o editor de vídeo da OrbeLabz. É um **fork do [Concat](https://github.com/jub0t/Concat)**, de Jareer Abdullah e colaboradores, feito a partir da versão **v0.2.9** (commit `784021e7`).

## O que mudou em relação ao Concat

Modificado pela OrbeLabz a partir de 10/11/2026:

- **Nome:** LabzCut em vez de Concat em todos os textos da interface, nas 26 línguas, na janela, no executável (`labzcut.exe`) e no instalador.
- **Ícone:** tesoura cortando uma fita de filme (`assets/labzcut/labzcut-icon.svg`, PNGs e `.ico` em `assets/icons/labzcut_*`).
- **Cores:** tema escuro com a escada de superfícies azul-marinho da OrbeLabz (`#0B0F19`, `#111827`) e destaque padrão ciano `#00F2FE`; tema claro com destaque azul `#2563EB`. Arquivos: `src/crates/concat/ui/theme/`.
- **Atualizador:** procura versões em `OrbeLabz/LabzCut`, nunca nas do Concat.
- **Pastas de dados:** `com.orbelabz.labzcut`, separadas das do Concat; o LabzCut não adota as pastas de um Concat instalado.
- **Instalador:** `assets/windows/labzcut.iss`, com AppId próprio, para não substituir um Concat instalado.

Continuam vindo do projeto Concat, com o nome dele: o espelho de modelos de IA (`jub0t/Concat`, release `models-v1`), a biblioteca de sons (`concatapp/assets`) e os guias do site do Concat.

## Licença

O código continua sob a **GNU AGPL-3.0-or-later** ([LICENSE](LICENSE)), como o original. Quem distribuir o LabzCut precisa oferecer o código-fonte completo sob a mesma licença. Os avisos de copyright dos arquivos (`SPDX-FileCopyrightText`) foram mantidos. Componentes de terceiros: [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

O nome e a logo do Concat não fazem parte da licença ([TRADEMARK.md](TRADEMARK.md)). Por isso o fork usa nome e ícone próprios e não se apresenta como versão oficial do Concat.

Os nomes internos dos crates (`concat-*`) foram mantidos de propósito, para facilitar trazer atualizações do projeto original.
