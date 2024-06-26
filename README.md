<p></p>
<p align="center"><img src="https://i.imgur.com/HJnpvwQ.png" width="200" height="48"/> EFI</p>
<p align="center">
 <a href="https://www.apple.com/macos">
  <img src="https://img.shields.io/badge/Ventura-13.5-informational.svg">
 </a>
 <a href="https://www.apple.com/macos">
  <img src="https://img.shields.io/badge/Sonoma-14.0%20beta3-informational.svg">
 </a>
 <a href="https://github.com/acidanthera/OpenCorePkg">
  <img src="https://img.shields.io/badge/OpenCore-0.9.4-informational.svg">
 </a>
 <a href="https://github.com/haxgun/Ryzentosh/blob/main/LICENSE">
  <img src="https://img.shields.io/github/license/haxgun/Ryzentosh">
 </a>
</p>

<h2></h2>

> **Aviso**
>
> Use por sua conta e risco. Eu construí este EFI para mim e ele não garante 100% de funcionamento com o seu hardware.
>
> As seções MLB, ROM, número de série e SystemUUID são especificamente deixadas vazias. Use GenSMBIOS para gerar SMBios.
>
> Eu recomendo usar um iMac20.1, se você estiver usando um iGPU. Caso contrário, use [estes](https://dortania.github.io/OpenCore-Install-Guide/AMD/zen.html#platforminfo)

<h2 align="center">📺 Construir</h2>

| **Componente** | **Modelo**                                                     |
| ------------- |---------------------------------------------------------------|
| CPU         | AMD Ryzen 5 5600G @ 4.2GHz                                      |
| Motherboard | aorus elite B450M  - BIOS Version 7A38v9E                   |
| GPU         | ASUS AMD Radeon RX 550 DUAL OC*                                 |
| RAM         | ADATA XPG GAMMIX D20 2 x 8GB @ 3200 MHz                         |
| OS disk     | Team Group GX2 256GB                                            |
| Win disk    | NVMe Apacer AS2280P4 256GB                                      |
| Other disk  | WD Blue 1 TB                                                    |
| macOS       | Ventura 13.5 (22G74), Sonoma 14 beta 3 (23A5286i)               |
| OpenCore    | 0.9.4 Release                                                   |

> **Nota** \
> Em vez de dGPU, você pode usar iGPU no processador graças ao NootedRed, mas então você terá problemas com DRM, iServices e suspensão.

<h2 align="center">🔧 BIOS</h2>

<details>
    <summary><b>🔌 Configurações</b></summary>

| **Componente**                  | **Modelo**                                    |
|--------------------------------|----------------------------------------------|
| Inicialização rápida           | Desativada                                   |
| Modo SVM                       | Ativado                                      |
| Acima de 4G Decodificação      | Desativada                                   |
| BAR Redimensionável            | Desativada                                   |
| Controlador de Gráficos Integrados | Automático                              |
| IOMMU                          | Desativada                                   |
| Inicialização do Adaptador Gráfico | Gráficos Integrados (IGD)               |
| Tamanho do buffer de quadro UMA | Desativado*                                 |
| XHCI Hand-off                  | Ativado                                      |
| Modo de Inicialização          | CSM                                          |
| Secure Boot e TPM              | Desativados                                  |

> **Nota**
>
> *Se você usar iGPU, configure no mínimo 512 MB. Podem ocorrer artefatos em alguns PCs/notebooks se 512 MB de VRAM estiverem configurados. Para evitar isso, você precisa definir pelo menos 1 GB de VRAM.

</details>

**🏞️ Mais detalhes das minhas configurações podem ser encontrados [aqui](https://imgur.com/a/Q2ssS6q)**

**⚠️ Você pode ler mais sobre as configurações da BIOS no [guia](https://dortania.github.io/OpenCore-Install-Guide/AMD/zen.html#amd-bios-settings)**

<h2 align="center">🩼 Funcional</h2>

- [x] macOS graças ao [dortania](https://dortania.github.io/OpenCore-Install-Guide/)
- [x] CPU pelo [AMD-Vanilla](https://github.com/AMD-OSX/AMD_Vanilla)
- [x] Áudio pelo [AppleALC](https://github.com/acidanthera/AppleALC)
- [x] Ethernet pelo RealtekRTL8111
- [x] dGPU pelo [WhateverGreen](https://github.com/Acidanthera/WhateverGreen)
- [x] iGPU pelo [NootedRed](https://github.com/NootInc/NootedRed)
- [x] iServices & DRM
- [x] Suspensão
- [ ] Airdrop / Handoff (não há como verificar)

> **Nota**
>
> Se você usar iGPU: iServices não funcionará. Existem pequenos artefatos gráficos ao trabalhar com navegadores no motor Chromium. O desenvolvedor do NootedRed está ciente do problema. Um remendo está embutido no config, que reduz o número de artefatos gráficos.

<h2 align="center">🪚 Altere para você</h2>

Edite o patch de contagem de núcleos para corresponder ao seu CPU

Veja [AMD Vanilla OpenCore](https://github.com/AMD-OSX/AMD_Vanilla/tree/master) ou [OpenCore-Install-Guide](https://dortania.github.io/OpenCore-Install-Guide/extras/ventura.html#amd-patches)

<details>
    <summary>Mini-Guia</summary>
    Encontre os três `algrey - Force cpuid_cores_per_package`

    - `kernel -> Patch -> 0  -> Replace` para macOS 10.13.x, 10.14.x
    - `kernel -> Patch -> 1  -> Replace` para macOS 10.15.x, 11.x
    - `kernel -> Patch -> 2  -> Replace` para macOS 12.x, 13.0 a 13.2.1
    - `kernel -> Patch -> 3  -> Replace` para macOS 13.3

    ```
    B8000000 0000 => B8 <core count> 0000 0000
    BA000000 0000 => BA <core count> 0000 0000
    BA000000 0090 => BA <core count> 0000 0090
    BA000000 00 => BA <core count> 0000 00
    ```

    | CoreCount | Hexadecimal |
    | --------- | ----------- |
    | 6 Núcleos | 06          |
    | 8 Núcleos | 08          |
    | 12 Núcleos | 0C         |
    | 16 Núcleos | 10         |
    | 32 Núcleos | 20         |
    | 64 Núcleos | 40         |

    Por exemplo, o 5600G tem 6 núcleos

    ```
    B8 06 00000000
    BA 06 00000000
    BA 06 00000090
    BA 06 000000
    ```
</details>

<h2 align="center">🔧 Ferramentas</h2>

1. [Hackintool](https://github.com/benbaker76/Hackintool)
2. [OpenCore Configurator](https://mackie100projects.altervista.org/download-opencore-configurator/)
3. [CPU Name](https://github.com/corpnewt/CPU-Name)
4. [About This Hack](https://github.com/0xCUB3/About-This-Hack)

<h2 align="center">🧱 Scripts</h2>

> **Aviso**
>
> Todos os scripts devem ser usados com direitos elevados! Para fazer isso, use
> ```sudo bash <nome_script>.sh```
1. **hostname.sh** - altera o nome do seu computador ou hostname local no Mac
2. **clear-network-interfaces.sh** - ajuda a resolver problemas com ethernet en0

<h2 align="center">💡 Dicas</h2>

 1. Se você quiser mudar o nome do processador, use [este](https://github.com/corpnewt/CPU-Name)
 2. Se você tiver uma configuração de CPU e placa-mãe 1-em-1 como a minha, você pode usar este config. Se for diferente, aconselho a montá-lo você mesmo de acordo com [o guia](https://dortania.github.io/OpenCore-Install-Guide/). Dessa forma, você gastará menos tempo resolvendo problemas e tudo funcionará bem. 🫡

<h2 align="center">🏞️ Screenshot</h2>
<img src="https://i.imgur.com/qBf9Km2.png" alt="macOS Ventura">

<br/>

<img src="https://i.imgur.com/fpN7SS7.png" alt="macOS Ventura">

<br/>

<img src="https://i.imgur.com/y12giX0.png" alt
