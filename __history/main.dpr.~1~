uses
  ShellAPI, Windows, SysUtils, Classes, Registry, WinSock;

function GetHostName: string;
var
  Buffer: array[0..255] of AnsiChar;
begin
  if gethostname(Buffer, SizeOf(Buffer)) = 0 then
    Result := string(Buffer)
  else
    raise Exception.Create('Erro ao obter o nome do host');
end;

function GetMACAddress: string;
var
  NCB: TNCB;
  Adapter: array[1..8] of AdapterStatus;
  i: Integer;
  MAC: string;
begin
  FillChar(NCB, SizeOf(NCB), 0);
  NCB.ncb_command := NCBRESET;

  if Netbios(@NCB) <> NRC_GOODRET then
    raise Exception.Create('Erro ao resetar o NetBIOS');

  FillChar(NCB, SizeOf(NCB), 0);
  NCB.ncb_command := NCBASTAT;
  NCB.ncb_lana_num := 0;

  StrPCopy(NCB.ncb_callname, '*');
  if Netbios(@NCB) <> NRC_GOODRET then
    raise Exception.Create('Erro ao obter o status do adaptador');

  Move(NCB.ncb_buffer, Adapter, SizeOf(Adapter));

  MAC := '';
  for i := 1 to 6 do
    MAC := MAC + IntToHex(Adapter[1].adapter_address[i], 2);
  Result := MAC;
end;

procedure InstallApplication(const AppPath: string);
begin
  ShellExecute(0, 'open', PChar(AppPath), nil, nil, SW_SHOWNORMAL);
end;

procedure InstallNLM(const NLMPath: string);
begin
  ShellExecute(0, 'open', PChar(NLMPath), nil, nil, SW_SHOWNORMAL);
end;

procedure StopProcesses;
begin
  ShellExecute(0, 'open', 'taskkill.exe', '/F /IM lmgrd.exe', nil, SW_HIDE);
  ShellExecute(0, 'open', 'taskkill.exe', '/F /IM adskflex.exe', nil, SW_HIDE);
end;

procedure ReplaceFile(const Source, Dest: string);
begin
  if not CopyFile(PChar(Source), PChar(Dest), False) then
    raise Exception.CreateFmt('Erro ao substituir arquivo: %s', [SysErrorMessage(GetLastError)]);
end;

procedure ConfigureLicFile(const LicFilePath, HostName, MACAddress: string);
var
  LicFile: TStringList;
begin
  LicFile := TStringList.Create;
  try
    LicFile.LoadFromFile(LicFilePath);
    LicFile.Text := StringReplace(LicFile.Text, '<HOSTNAME>', HostName, [rfReplaceAll]);
    LicFile.Text := StringReplace(LicFile.Text, '<MAC>', MACAddress, [rfReplaceAll]);
    LicFile.SaveToFile(LicFilePath);
  finally
    LicFile.Free;
  end;
end;

procedure CreateService;
var
  reg: TRegistry;
begin
  reg := TRegistry.Create;
  try
    reg.RootKey := HKEY_LOCAL_MACHINE;
    if reg.OpenKey('\SYSTEM\CurrentControlSet\Services\Autodesk', True) then
    begin
      reg.WriteString('DisplayName', 'Autodesk License Service');
      reg.WriteString('ImagePath', '"C:\Autodesk\Network License Manager\lmgrd.exe" -c "C:\Autodesk\Network License Manager\lic.dat" -z');
      reg.WriteString('Description', 'Serviço de licença da Autodesk');
      reg.WriteInteger('Start', 2);
      reg.CloseKey;
    end;
  finally
    reg.Free;
  end;
end;

procedure StartLicenseServer;
begin
  ShellExecute(0, 'open', 'C:\Autodesk\Network License Manager\lmgrd.exe', '-c "C:\Autodesk\Network License Manager\lic.dat" -z', nil, SW_HIDE);
end;

procedure InitializeLMTools(const LMToolsPath: string);
begin
  ShellExecute(0, 'open', PChar(LMToolsPath), nil, nil, SW_SHOWNORMAL);
end;

procedure StartAutodeskApp(const AppPath: string);
begin
  ShellExecute(0, 'open', PChar(AppPath), nil, nil, SW_SHOWNORMAL);
end;

procedure Main;
var
  HostName, MACAddress: string;
begin
  try
    const AppInstallerPath = 'C:\path_to_autodesk_installer.exe';
    const NLMInstallerPath = 'C:\path_to_crack\NLM.msi';
    const CrackedAdskflex = 'C:\path_to_crack\adskflex.exe';
    const DestAdskflex = 'C:\Autodesk\Network License Manager\adskflex.exe';
    const CrackedNetapi32 = 'C:\path_to_crack\netapi32.dll';
    const DestNetapi32 = 'C:\Program Files (x86)\Common Files\Autodesk Shared\AdskLicensing\Current\AdskLicensingAgent\netapi32.dll';
    const LicFilePath = 'C:\Autodesk\Network License Manager\lic.dat';
    const LMToolsPath = 'C:\Autodesk\Network License Manager\lmtools.exe';

    InstallApplication(AppInstallerPath);
    InstallNLM(NLMInstallerPath);
    StopProcesses;
    ReplaceFile(CrackedAdskflex, DestAdskflex);
    ReplaceFile(CrackedNetapi32, DestNetapi32);

    HostName := GetHostName;
    MACAddress := GetMACAddress;
    ConfigureLicFile(LicFilePath, HostName, MACAddress);

    CreateService;
    StartLicenseServer;
    InitializeLMTools(LMToolsPath);
    StartAutodeskApp(AppInstallerPath);

  except
    on E: Exception do
      Writeln('Ocorreu um erro: ', E.Message);
  end;
end;

begin
  Main;
end.
