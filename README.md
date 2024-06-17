# Hackintosh com macOS Big Sur

## Sumário
1. [Introdução](#introdução)
2. [Especificações do Hardware](#especificações-do-hardware)
3. [Pré-requisitos](#pré-requisitos)
4. [Criação do Instalador USB](#criação-do-instalador-usb)
5. [Configuração do OpenCore](#configuração-do-opencore)
6. [Instalação do macOS Big Sur](#instalação-do-macos-big-sur)
7. [Pós-Instalação](#pós-instalação)
8. [Problemas Conhecidos](#problemas-conhecidos)
9. [Conclusão](#conclusão)
10. [Recursos e Créditos](#recursos-e-créditos)

## Introdução
Este guia detalha como configurar um Hackintosh com macOS Big Sur em um sistema baseado em AMD Ryzen. O processo envolve criar um instalador USB, configurar o bootloader OpenCore e realizar ajustes pós-instalação.

![Hackintosh Setup](https://user-images.githubusercontent.com/your-username/hackintosh-setup.png)

## Especificações do Hardware

### Componentes Principais:
- **Processador (CPU)**: AMD Ryzen 5 5600G
  - 6 núcleos / 12 threads
  - Frequência base: 3.9 GHz
  - Frequência de boost: até 4.4 GHz
- **Placa-mãe**: B450M Aorus
  - Chipset: AMD B450
  - BIOS: Atualização recomendada para compatibilidade com Hackintosh
- **Memória RAM**: 16GB DDR4 3200MHz
- **Armazenamento**: SSD NVMe principal
- **Placa de vídeo (GPU)**: Radeon RX 550 XT
  - 4 GB GDDR5
- **Placa de rede**: Intel Dual Band Wireless-AC 7260
  - Wi-Fi e Bluetooth

![Hardware](https://user-images.githubusercontent.com/your-username/hardware.png)

## Pré-requisitos

- **Sistema Operacional**: Um computador com macOS ou acesso a uma máquina virtual macOS para criar o instalador.
- **Pendrive USB**: Com pelo menos 16GB de capacidade.
- **Ferramentas de Software**:
  - **OpenCore**: Bootloader para Hackintosh
  - **GibMacOS**: Ferramenta para baixar o instalador do macOS
  - **ProperTree**: Editor de configuração para arquivos `.plist`
  - **GenSMBIOS**: Gerador de SMBIOS para emular a identidade do Mac
  - **MountEFI**: Ferramenta para montar partições EFI

## Criação do Instalador USB

1. **Baixe o macOS Big Sur**:
   - Use o **GibMacOS** para baixar o instalador do macOS Big Sur.
   - Siga as instruções para criar o instalador em um pendrive USB.

2. **Formatar o USB**:
   - Utilize o **Disk Utility** para formatar o pendrive USB com o formato **Mac OS Extended (Journaled)** e esquema **GUID Partition Map**.

3. **Criar o Instalador**:
   - Execute o comando no Terminal para criar o instalador no pendrive USB:
     ```bash
     sudo /Applications/Install\ macOS\ Big\ Sur.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
     ```

## Configuração do OpenCore

1. **Baixe e Extraia o OpenCore**:
   - Baixe a versão mais recente do OpenCore e extraia os arquivos.

2. **Configuração da EFI**:
   - Monte a partição EFI do pendrive USB usando **MountEFI**.
   - Copie a pasta **EFI** do OpenCore para a partição EFI do USB.

3. **Configuração do OpenCore**:
   - Edite o arquivo `config.plist` usando o **ProperTree**.
   - Adicione suporte específico para processadores AMD.
   - Configure drivers e kexts necessários:
     - **VirtualSMC**: Emulação de sensores do sistema.
     - **Lilu**: Base para várias extensões de kernel.
     - **WhateverGreen**: Suporte gráfico.
     - **AppleALC**: Suporte de áudio.
     - **USBInjectAll**: Suporte para portas USB.
     - **IntelMausi**: Suporte para rede.
     - **AirportItlwm**: Kext para suporte à placa Wi-Fi Intel 7260.

4. **SMBIOS**:
   - Gere um SMBIOS com **GenSMBIOS** que seja compatível com o modelo **iMacPro1,1**.

![OpenCore Setup](https://user-images.githubusercontent.com/your-username/opencore-setup.png)

## Instalação do macOS Big Sur

1. **Inicialize a partir do USB**:
   - Insira o pendrive USB e reinicie o computador.
   - Acesse a BIOS e configure para inicializar a partir do USB.
   - Selecione o instalador do macOS no menu do OpenCore.

2. **Instalação**:
   - Siga as etapas do instalador para instalar o macOS Big Sur no SSD NVMe.

## Pós-Instalação

1. **Configuração de EFI no SSD**:
   - Monte a partição EFI do SSD.
   - Copie a pasta **EFI** do pendrive USB para a partição EFI do SSD.

2. **Kexts e Patches**:
   - Instale todos os kexts adicionais e aplique patches específicos para estabilidade e funcionalidade.

3. **Configuração do Sistema**:
   - Ajuste configurações como resolução da tela, som e conectividade de rede.
   - Verifique se todos os componentes estão funcionando corretamente.

## Problemas Conhecidos

- **Gráficos Integrados**: Os gráficos Vega integrados do Ryzen 5 5600G não são suportados pelo macOS, então é necessário usar a Radeon RX 550 XT como GPU principal.
- **Conectividade Wi-Fi/Bluetooth**: A placa de rede Intel 7260 pode precisar de kexts específicos para funcionar corretamente com Wi-Fi e Bluetooth.

## Conclusão
Este guia cobre os passos essenciais para configurar um Hackintosh usando o macOS Big Sur em um sistema AMD Ryzen com a placa-mãe B450M Aorus. Embora a configuração inicial possa ser complexa, seguir os passos e usar as ferramentas adequadas facilita bastante o processo.

## Recursos e Créditos
- **[OpenCore](https://dortania.github.io/OpenCore-Install-Guide/)**: Guia oficial de instalação do OpenCore.
- **[GibMacOS](https://github.com/corpnewt/gibMacOS)**: Ferramenta para baixar o instalador do macOS.
- **[ProperTree](https://github.com/corpnewt/ProperTree)**: Editor de configuração para arquivos `.plist`.
- **[GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)**: Ferramenta para gerar SMBIOS compatíveis.
- **[Hackintosh Forum](https://www.tonymacx86.com/)**: Comunidade com suporte e guias detalhados.

---

Se precisar de mais informações ou ajustes no README, é só avisar!
