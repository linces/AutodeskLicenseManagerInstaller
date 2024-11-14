# Autodesk License Manager Installer

Script Delphi para instalação e configuração automatizada do License Manager da Autodesk, incluindo substituição dinâmica do Hostname e Endereço MAC.

Isto é uma tentativa de automatizar o processo de uso do Crack do Magnitude. Lógicamente vc irá precisar dele para que tudo funcione.

## Descrição

Este script automatiza o processo de instalação do License Manager da Autodesk, substituindo o Hostname e o Endereço MAC no arquivo de licença (`lic.dat`). Ideal para empresas ou usuários que precisam de uma configuração rápida e personalizada do sistema de licenciamento em rede da Autodesk.

### Recursos do Script

- Instala automaticamente o Autodesk License Manager e os arquivos necessários
- Configura o arquivo de licença (`lic.dat`) substituindo `<HOSTNAME>` e `<MAC>` pelo Hostname e MAC Address da máquina
- Gera e registra o serviço de licença no Windows
- Inicia automaticamente o servidor de licença ao final da configuração

## Requisitos

- **Sistema Operacional**: Windows
- **Linguagem**: Delphi XE11 Alexandria
- **Permissões**: Permissões de administrador para instalação e manipulação de serviços
- **Dependências**:
  - Delphi para compilar o script
  - `lmgrd.exe` e `adskflex.exe` devem estar disponíveis

## Utilização/Compilação

Compilar o Código:

Abra o arquivo main.dpr com Delphi XE11 Alexandria e compile o projeto.
Configurar o Arquivo lic.dat

Coloque o arquivo lic.dat na pasta C:\Autodesk\Network License Manager\.
O script substituirá <HOSTNAME> e <MAC> automaticamente pelos valores do sistema.

Executar o Código:

Execute o código ou .exe já compilado para iniciar o processo de instalação e configuração:
Instala o Autodesk License Manager
Configura o arquivo de licença
Registra e inicia o serviço de licença no Windows

## Utilização/Compilação
Sinta-se à vontade para abrir issues e pull requests para melhorias. A participação da comunidade é bem-vinda para melhorar e expandir este código.


## License

Este projeto utiliza a licença "WathEver" faça o que quiser e como quiser, a que sempre utilizo :D.

## Disclaimer

Meu disclaimer padrão:

"Este projeto é fornecido "como está", sem garantias de qualquer tipo. Use-o a seu próprio risco. Não tenho responsabilidade por qualquer danos ou perdas que ocorram ao usar este projeto.

Bla bla bla bla"