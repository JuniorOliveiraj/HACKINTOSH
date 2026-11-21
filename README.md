# macOS Tahoe 26.7.3 no Ryzen 5 5600G

EFI para a Gigabyte B450 AORUS M com BIOS F63a, Ryzen 5 5600G e Radeon integrada Cezanne. A configuração usa OpenCore 1.0.9 e NootedRed. Esta branch é independente e dedicada a essa versão.

## Teste pelo pendrive

1. Copie a pasta `EFI` para o pendrive do instalador do macOS Tahoe.
2. Inicie o pendrive pelo menu UEFI da placa-mãe. Use Ethernet durante a instalação.
3. Após instalar, use o HeliPort para conectar o Wi-Fi Intel Wireless-AC 7260 com o kext itlwm.

O `config.plist` passou no `ocvalidate` 1.0.9. O boot, o áudio e o mapa de portas USB ainda precisam de teste no hardware.

O SMBIOS MacPro7,1 foi gerado para uso local. Remova os identificadores específicos da máquina antes de publicar a EFI.
