# LSP---retorna-escala-de-trabalho
Função que retorna escala de trabalho de acordo com o teto informado no parâmetro de entrada.

* Note que as estruturas objColaborador e objParametrosEntrada já devem estar devidamente preenchidos antes de executar a função.

## Função

```
Definir Funcao retornaEscalaDeTrabalho(Numero nTeto);

Funcao retornaEscalaDeTrabalho(Numero nTeto);
{
     nNumEmp = objColaborador[nTeto].nNumEmp;
     nTipCol = objColaborador[nTeto].nTipCol;
     nNumcad = objColaborador[nTeto].nNumCad; 
     Definir Data dDataRef; dDataRef = objParamentrosEntrada[1].dDataFimDoMes;
       
     Definir Cursor cEscala;
     cEscala.SQL "Select r006esc.nomesc From r038hes, r006esc  \
       where r038hes.codesc = r006esc.codesc and r038hes.numcad = :nNumCad and r038hes.TipCol = :nTipCol and r038hes.NumEmp = :nNumemp \ 
       And r038hes.datalt = (Select max(Tab2.DatAlt) From r038hes Tab2 Where Tab2.NumEmp = :nNumemp And Tab2.NumCad = :nNumCad And Tab2.TipCol = :nTipCol \
                             And (tab2.DatAlt <= :dDataRef))";        
     cEscala.AbrirCursor();
     Se (cEscala.Achou) {  
       objColaborador[nTeto].aEscala = cEscala.NomEsc; 
     }  
     cEscala.FecharCursor(); 
};
```


## Recomendações
Para usar a função na regra, deve-se declará-la no início da mesma.
É interessante que se reserve, por exemplo, a regra 001 apenas para implementar funções.

Em implementações de relatório, tenho o hábito de declarar as funções em `Funções Globais` no `Modelo Gerador`.

![image](https://github.com/heripedroso/LSP---converte-minutos-em-HH-MI/assets/22459829/fa6ef8f7-399d-4923-9c2e-a814f502bddc)
