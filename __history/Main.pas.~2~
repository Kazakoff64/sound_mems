unit Main;

interface

uses
  System.SysUtils, System.Types, System.UITypes, System.Classes, System.Variants,
  FMX.Types, FMX.Controls, FMX.Forms, FMX.Graphics, FMX.Dialogs,
  FMX.Controls.Presentation, FMX.StdCtrls, FMX.Objects, FMX.Memo.Types,
  FMX.ScrollBox, FMX.Memo, FMX.Layouts, FMX.ListBox, System.Rtti,
  FMX.Grid.Style, FMX.Grid;

type
  TForm1 = class(TForm)
    Button9: TButton;
    StyleBook1: TStyleBook;
    ComboBox1: TComboBox;
    Button1: TButton;
    TrackBar1: TTrackBar;
    Label1: TLabel;
    procedure Button9Click(Sender: TObject);
    procedure FormCreate(Sender: TObject);
    procedure Button1Click(Sender: TObject);
    procedure TrackBar1Tracking(Sender: TObject);
    procedure ComboBox1ClosePopup(Sender: TObject);
  private
    { Private declarations }
  public
    { Public declarations }
  end;

var
  Form1: TForm1;

  chan: DWORD;

implementation

{$R *.fmx}

uses StrUtils, Bass, BassEnc, BassEnc_FLAC, BassEnc_MP3, BassEnc_OGG, BassEnc_OPUS, BassFLAC, BassOPUS; {-framework AudioToolbox -framework CFNetwork}

function VersionToString(LibName: string; LibVersion: DWORD): string;
begin
  Result := LibName
    {$IF Defined(WIN32) or Defined(MACOS32) or Defined(LINUX32) or Defined(IOS32) or Defined(ANDROID32)}
    + ' 32-bit '
    {$ELSEIF Defined(WIN64) or Defined(MACOS64) or Defined(LINUX64) or Defined(IOS64) or Defined(ANDROID64)}
    + ' 64-bit '
    {$ENDIF}
    + (LibVersion shr 24).ToString
    + '.' + ((LibVersion shr 16) and $FF).ToString
    + '.' + ((LibVersion shr 8) and $FF).ToString
    + '.' + (LibVersion and $FF).ToString;
end;

function AvailabilityToString(LibName: string; LibAvailability: Boolean): string;
begin
  Result := LibName
    {$IF Defined(WIN32) or Defined(MACOS32) or Defined(LINUX32) or Defined(IOS32) or Defined(ANDROID32)}
    + ' 32-bit '
    {$ELSEIF Defined(WIN64) or Defined(MACOS64) or Defined(LINUX64) or Defined(IOS64) or Defined(ANDROID64)}
    + ' 64-bit '
    {$ENDIF}
    + IfThen(LibAvailability, 'OK', 'not available');
end;

function PluginVersionToString(LibName: string; LibDLL: PChar): string;
var
  Plugin: HPLUGIN;
  Info: PBASS_PLUGININFO;
  Version: DWORD;
begin
  Version:= 0;
  {$IFDEF IOS}
    Plugin := BASS_PluginLoad(LibDLL, 0);
  {$ELSE}
    Plugin := BASS_PluginLoad(LibDLL, BASS_UNICODE);
  {$ENDIF}
  if Plugin <> 0 then
  begin
    Info := BASS_PluginGetInfo(Plugin);
    if Assigned(Info) then
      Version := Info.version;
    BASS_PluginFree(Plugin);
  end;
  Result := LibName + IfThen(Version <> 0, VersionToString('', Version), ' not available');
end;

procedure TForm1.Button1Click(Sender: TObject);
begin

    //Item:= ComboBox1.ItemIndex + 1;
    //ShowMessage(Item.ToString);


end;

procedure TForm1.Button9Click(Sender: TObject);

 var
  i, Item: Integer;
  ADeviceInfo: BASS_DEVICEINFO;


begin

   chan := BASS_StreamCreateFile(False,PAnsiChar(AnsiString('/Users/kazakoff/Downloads/baraban_1995_hq.mp3')),0,0,0);

   IF chan<>0 then

    begin

      BASS_ChannelPlay(chan, FALSE);

    end;


end;

procedure TForm1.ComboBox1ClosePopup(Sender: TObject);

var

Item:integer;

begin

    Item:= ComboBox1.ItemIndex + 1;


     {$IFDEF MSWINDOWS}

      if not  BASS_Init(Item, 44100, 0, 0, nil) Then

    {$ENDIF}


    {$IFDEF MACOS}
      if not  BASS_Init(Item, 44100, 0, handle, nil) Then
    {$ENDIF}

        ShowMessage('Не могу инициализировать звук!');

     BASS_Start;



end;

procedure TForm1.FormCreate(Sender: TObject);
var

  i:Integer;
  ADeviceInfo: BASS_DEVICEINFO;
  chan: DWORD;

begin

    i := 1;
    while BASS_GetDeviceInfo(I, ADeviceInfo) do

    begin

      //ListBox1.Items.Add(ADeviceInfo.name);
      ComboBox1.Items.Add(ADeviceInfo.name);


      i := i + 1;

    end;

end;

procedure TForm1.TrackBar1Tracking(Sender: TObject);
begin

    BASS_ChannelSetAttribute(chan, BASS_ATTRIB_VOL, TrackBar1.Value/100);

end;

end.
