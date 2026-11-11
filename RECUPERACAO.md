---
tipo: dossie-recuperacao
resumo: LabzCut, fork do editor de vídeo Concat v0.2.9 com nome, ícone e cores da OrbeLabz; compilado no PC, sem repositório remoto ainda.
data: 2026-11-10
projeto: LabzCut
status: ativo
origem: Pedido de John em 10/11/2026 ("desmonte todo esse aplicativo para recriar um clone dele chamado LabzCut com as cores da orbelabz"); regra de preservação aprovada em 29/10/2026.
---
# Recuperação: LabzCut

## Identificação e continuidade
- Nome: `LabzCut`. Objetivo: editor de vídeo local da OrbeLabz (alternativa ao CapCut), sem conta, sem marca d'água.
- Origem: fork do [Concat](https://github.com/jub0t/Concat), AGPL-3.0-or-later, tag `v0.2.9`, commit `784021e7`. Detalhes e licença: [LABZCUT.md](LABZCUT.md).
- Responsável: Claude, a pedido de John (10/11/2026).
- Pasta física: `E:\Brain\OrbeLabz\Projetos\Em desenvolvimento\LabzCut` (Git próprio, branch `labzcut`, remoto `upstream` = jub0t/Concat).
- Instalador recebido de John: `C:\Users\JohnD\Downloads\Concat-0.2.9-windows-x86_64-setup.exe`, SHA-256 `bc3e994a592d46c9dce037bf0b41e329de7b3821c25bc27717a8e0d5d34d1a0a`, sem assinatura digital. Não foi executado nem descompilado: o código-fonte oficial da mesma versão foi usado no lugar.

## Estado que deve ser recuperado
| Camada | Local ou revisão | Data | Limites |
|---|---|---|---|
| Código | Git local, branch `labzcut` | 10/11/2026 | Sem remoto da OrbeLabz: o fork público `OrbeLabz/LabzCut` aguarda OK de John |
| Executável | `src/target/<perfil>/labzcut.exe` | não verificado | Regenerável pela compilação abaixo |
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
3. `E:\Brain\Ferramentas\labzcut-build\compilar.bat quick` (teste) ou `compilar.bat app` (versão final).
4. Para rodar, `onnxruntime.dll` e as DLLs do FFmpeg precisam estar ao lado do `labzcut.exe` ou no PATH.

## Lacunas
- Sem cópia fora do PC. Sem teste de restauração.
- Ícone: teste 02 (`assets/labzcut/teste-02.png`); vira padrão só quando John aprovar.
- Android, iOS e macOS não foram adaptados nem testados.
