# Autodesk License Manager Installer

Script Delphi para instala��o e configura��o automatizada do License Manager da Autodesk, incluindo substitui��o din�mica do Hostname e Endere�o MAC.

Isto � uma tentativa de automatizar o processo de uso do Crack do Magnitude. L�gicamente vc ir� precisar dele para que tudo funcione.

## Descri��o

Este script automatiza o processo de instala��o do License Manager da Autodesk, substituindo o Hostname e o Endere�o MAC no arquivo de licen�a (`lic.dat`). Ideal para empresas ou usu�rios que precisam de uma configura��o r�pida e personalizada do sistema de licenciamento em rede da Autodesk.

### Recursos do Script

- Instala automaticamente o Autodesk License Manager e os arquivos necess�rios
- Configura o arquivo de licen�a (`lic.dat`) substituindo `<HOSTNAME>` e `<MAC>` pelo Hostname e MAC Address da m�quina
- Gera e registra o servi�o de licen�a no Windows
- Inicia automaticamente o servidor de licen�a ao final da configura��o

## Requisitos

- **Sistema Operacional**: Windows
- **Linguagem**: Delphi XE11 Alexandria
- **Permiss�es**: Permiss�es de administrador para instala��o e manipula��o de servi�os
- **Depend�ncias**:
  - Delphi para compilar o script
  - `lmgrd.exe` e `adskflex.exe` devem estar dispon�veis

## Utiliza��o/Compila��o

Compilar o C�digo:

Abra o arquivo main.dpr com Delphi XE11 Alexandria e compile o projeto.
Configurar o Arquivo lic.dat

Coloque o arquivo lic.dat na pasta C:\Autodesk\Network License Manager\.
O script substituir� <HOSTNAME> e <MAC> automaticamente pelos valores do sistema.

Executar o C�digo:

Execute o c�digo ou .exe j� compilado para iniciar o processo de instala��o e configura��o:
Instala o Autodesk License Manager
Configura o arquivo de licen�a
Registra e inicia o servi�o de licen�a no Windows

## Utiliza��o/Compila��o
Sinta-se � vontade para abrir issues e pull requests para melhorias. A participa��o da comunidade � bem-vinda para melhorar e expandir este c�digo.


## License

Este projeto utiliza a licen�a "WathEver" fa�a o que quiser e como quiser, a que sempre utilizo :D.

## Disclaimer

Meu disclaimer padr�o:

"Este projeto � fornecido "como est�", sem garantias de qualquer tipo. Use-o a seu pr�prio risco. N�o tenho responsabilidade por qualquer danos ou perdas que ocorram ao usar este projeto.

Bla bla bla bla"