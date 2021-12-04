unit Unit1;

interface

uses
  Windows, Messages, SysUtils, Variants, Classes, Graphics, Controls, Forms,
  Dialogs, StdCtrls,
  DCPblockciphers, DCPdes, DCPMd5,  DCPcrypt2,DCPsha1;

type
  TForm1 = class(TForm)
    edtSenha: TEdit;
    edtchave: TEdit;
    btn1: TButton;
    edtcartao: TEdit;
    edtOut: TEdit;
    lbl1: TLabel;
    lbl2: TLabel;
    lbl3: TLabel;
    lbl4: TLabel;
    lbl5: TLabel;
    procedure btn1Click(Sender: TObject);
  private
    { Private declarations }
  public
    { Public declarations }
  end;

var
  Form1: TForm1;

implementation

{$R *.dfm}
function StrToHex(Dado: String): String;
var cTemp: String;
I: Integer;
begin
  cTemp := '';
  for i := 1 to Length(Dado) Do
    cTemp := cTemp + IntToHex(Ord(Dado[i]), 2);
  Result := cTemp;
end;
function HexToInt(s: string): Longword;
var
  b: Byte;
  c: Char;
begin
  Result := 0;
  s := UpperCase(s);
  for b := 1 to Length(s) do
    begin
      Result := Result * 16;
      c := s[b];
      case c of
        '0'..'9': Inc(Result, Ord(c) - Ord('0'));
        'A'..'F': Inc(Result, Ord(c) - Ord('A') + 10);
        else
          raise EConvertError.Create('No Hex-Number');
      end;
    end;
end;

function HexToAsc(Dado: String): String;
var cTemp: String;
I: Integer;
begin
  cTemp := '';
  for i := 1 to Length(Dado) Do
  Begin
    if Not Odd(i) Then
      Begin
        cTemp := cTemp + Chr(HexToInt(Copy(Dado, i - 1, 2)));
      End;
  End;
  Result := cTemp;
end;

procedure TForm1.btn1Click(Sender: TObject);
var
  TDes: TDCP_3des;
  Des: TDCP_des;
  //TSha: TDCP_sha1;
  IV: String;
  K: Integer;
  Chave: String;
  Senha: String;
  Cartao: String;
  SenhaCartao:string;
  Criptograma,PinBlock:string;
begin

  //Chave  := HexToAsc(Chave);
  //SenhaCartao  := HexToAsc('06'+edtSenha.Text+'FFFFFFFF');

  SenhaCartao  := HexToAsc(edtSenha.Text);

  //SenhaCartao  := '06'+edtSenha.Text+'FFFFFFFF';
  IV     := StringOfChar(#0, 8);


        //SenhaCartao := edtSenha.Text+'FFFFFFFF';  //'06894060FFFFFFFF';
        Cartao      := HexToAsc('0000' + Copy(edtcartao.Text, 4, 12));
        PinBlock    := EmptyStr;
        Criptograma := '                                ';// Replicate(' ', 16);

        For K := 1 To 16 Do
          begin
            PinBlock := PinBlock + chr(ord(SenhaCartao[K]) Xor ord(Cartao[K]));
            //I := ord(SenhaCartao[K]) Xor ord(Cartao[K]);
            //PinBlock := PinBlock + IntToHexa(I);
          end;

        //PinBlock := StrToHex(PinBlock);


        TDes := TDCP_3des.Create(nil);
        Chave  := HexToAsc(edtchave.Text);


        TDes.Init(Chave[1],128,@IV[1]);


        TDes.EncryptCBC(PinBlock[1],Criptograma[1],Length(PinBlock));

        //TDes.EncryptECB(PinBlock[1], Criptograma[1]);
        //Criptograma := TDes.EncryptString(PinBlock);

        TDes.Burn;
        TDes.Free;


        edtOut.Text :=Copy( StrToHex(Criptograma),1,16);
end;

end.

