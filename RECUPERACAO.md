---
tipo: dossie-recuperacao
resumo: LabzCut, fork do editor de vídeo Concat v0.2.9 com nome, ícone e cores da OrbeLabz; compilado no PC, sem repositório remoto ainda.
data: 2026-11-10
projeto: LabzCut
status: concluído
origem: Pedido de John em 10/11/2026 ("desmonte todo esse aplicativo para recriar um clone dele chamado LabzCut com as cores da orbelabz"); regra de preservação aprovada em 29/10/2026.
---
# Recuperação: LabzCut

## Identificação e continuidade
- Nome: `LabzCut`. Objetivo: editor de vídeo local da OrbeLabz (alternativa ao CapCut), sem conta, sem marca d'água.
- Origem: fork do [Concat](https://github.com/jub0t/Concat), AGPL-3.0-or-later, tag `v0.2.9`, commit `784021e7`. Detalhes e licença: [LABZCUT.md](LABZCUT.md).
- Responsável: Claude, a pedido de John (10/11/2026).
- Pasta física: `E:\Brain\OrbeLabz\Projetos\Concluídos\LabzCut` (Git próprio, branch `labzcut`, remoto `upstream` = jub0t/Concat).
- Instalador recebido de John: `C:\Users\JohnD\Downloads\Concat-0.2.9-windows-x86_64-setup.exe`, SHA-256 `bc3e994a592d46c9dce037bf0b41e329de7b3821c25bc27717a8e0d5d34d1a0a`, sem assinatura digital. Não foi executado nem descompilado: o código-fonte oficial da mesma versão foi usado no lugar.

## Estado que deve ser recuperado
| Camada | Local ou revisão | Data | Limites |
|---|---|---|---|
| Código | Git local, branch `labzcut` | 10/11/2026 | Sem remoto da OrbeLabz: o fork público `OrbeLabz/LabzCut` aguarda OK de John |
| Executável | `src/target/x86_64-pc-windows-msvc/app/labzcut.exe` (final) e `src/target/quick/labzcut.exe` (teste) | 10/11/2026 | Regenerável; o final leva ~37 min |
| Instalador de distribuição (limpo) | `E:\Brain\Ferramentas\labzcut-build\stage\LabzCut-0.2.9-windows-x86_64-setup.exe`, 80,1 MB, SHA-256 `9ff4ca422fdcf56812fbd20362f554548e306a8189d4a18d82f68be4bac849e7` | 10/11/2026 | Sem assinatura digital (o SmartScreen avisa). Kaspersky (41 objetos) e Defender: zero detecção. Sem caminhos ou dados de John dentro |
| Remoto | `github.com/OrbeLabz/LabzCut`, branch `labzcut` (padrão), público, Actions desligado; Release `labzcut-v0.2.9` com o instalador (hash conferido no download) | 10/11/2026 | Página de download: orbelabz.com/ferramentas/labzcut/ |
| Backup | `G:\Meu Drive\Projeto OrbeLabz\LabzCut.zip`, 95 MB, SHA-256 `6726d888…f2401c4`, sem `src/target*` | 10/11/2026 | Cópia na pasta do Drive conferida; envio à nuvem pelo Google Drive não verificado |
| Dados do usuário | `%APPDATA%\com.orbelabz.labzcut` e `%LOCALAPPDATA%\com.orbelabz.labzcut` | não verificado | Separados das pastas do Concat |

## Dependências de compilação (Windows)
Ficam em `E:\Brain\Ferramentas\labzcut-build`, baixadas por `baixar.sh` com SHA-256 conferido contra `scripts/ci/deps.lock`:
- LLVM 21.1.0 (libclang) instalado em `llvm\`.
- FFmpeg 8.1.3 LGPL shared (BtbN) em `ffmpeg\`.
- ONNX Runtime 1.28.0 (Microsoft) em `onnxruntime-win-x64-1.28.0\`.
- Rust 1.93.1 (fixado em `src/rust-toolchain.toml`), Visual Studio Build Tools 2022 (`E:\Apps PC\VSBuildTools`, com CMake).

## Reconstrução do zero
1. `git clone --branch v0.2.9 https://github.com/jub0t/Concat.git LabzCut` e reaplicar as mudanças do LabzCut (ou clonar o fork, quando existir).
2. `bash E:\Brain\Ferramentas\labzcut-build\baixar.sh`, extrair os zips e instalar o LLVM em `llvm\` (`LLVM-21.1.0-win64.exe /S /D=...\llvm`).
3. `E:\Brain\Ferramentas\labzcut-build\compilar.bat quick` (teste, ~12 min na primeira vez) ou `compilar.bat app` (versão final, usa `--target x86_64-pc-windows-msvc`; sem ele o build script do ffmpeg-sys quebra com violação de acesso).
4. `powershell -File E:\Brain\Ferramentas\labzcut-build\empacotar.ps1` monta a pasta em `stage\` e gera o instalador com o Inno Setup 6.7.4 (instalado em `innosetup\`).
5. **Versão de download sem dados do PC:** `compilar-limpo.bat` compila em `E:\lt` (junção para `src	arget-lt`) com `CARGO_HOME=E:\lc` (junção para `E:\Apps PC\Rust\cargo`) e `limpo.toml` (`--remap-path-prefix`). Depois `empacotar.ps1 -Exe E:\lt_64-pc-windows-msvcpp\labzcut.exe`, escanear com `avp.com SCAN` e `MpCmdRun -Scan -ScanType 3`. Não usar `subst` (unidade virtual): o Kaspersky barrou o script de build ali com alerta heurístico `VHO:Trojan.Win32.Sdum.gen`, falso positivo num arquivo que nunca entra no instalador.
6. Para rodar, `onnxruntime.dll` e as DLLs do FFmpeg precisam estar ao lado do `labzcut.exe` ou no PATH.

## Verificado em 10/11/2026
- Tela inicial em pt-BR, com nome LabzCut, cores e versão certas, nas versões de teste e final empacotada (`assets/labzcut/tela-03-versao-final.png`).
- O exe empacotado carrega todas as DLLs sem o PATH de compilação.

## Lacunas
- Editor testado: importar mídia, montar a linha do tempo e pôr título funcionam (prints em `E:\LabzCut-demo`). Instalador testado: instala por usuário em `%LOCALAPPDATA%\Programs\LabzCut` e abre.
- Exportação e IA (legendas, recorte) continuam sem teste meu.
- Sem cópia fora do PC. Sem teste de restauração.
- Ícone: teste 02 (`assets/labzcut/teste-02.png`); vira padrão só quando John aprovar.
- Android, iOS e macOS não foram adaptados nem testados.
