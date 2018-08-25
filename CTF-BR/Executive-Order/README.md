# EXECUTIVE ORDER

> Conseguimos grampear alguns mandachuvas da Butcher Corp e descobrimos que sim, eles ainda usam linhas de telefonia fixa! Obtivemos esse áudio de uma ligação telefônica que parece ser importante. Você consegue decodificar os dados que eles estão transferindo?
> O primeiro que mandar a flag para contato at ctf-br.org será o vencedor.
>
> Nome: Executive Order

>
> Categoria: Forensics
>
> Link: http://ctf-br.org/files/HallOfFame/executiveorder.tar.gz


Iniciando a análise do arquivo:
```shell
$ file wiretap.flac
wiretap.flac: FLAC audio bitstream data, 16 bit, mono, 8 kHz, 447198 samples
```

Após análise do arquivo foi verificado que se trata da gravação de uma comunicação aparentemente através de um modem.Uma primeira verificação dos tons de discagem através do site http://dialabc.com/sound/detect/index.html, reveloou  o número 55 49 33218400. 
Utilizando o software audacity, foi separada a parte dos tons de discagem e tons de chamada da parte de transmissão dos dados. 

Em uma primeira abordagem, a tentativa foi de decodificar o audio utilizando o software minimodem, na tentativa de que fossem dados de uma comunicação entre dois modens. Essa abordagem não teve sucesso. 

Após essa tentativa, imaginando-se tratar de uma possível comunicação de fax, foi realizado uma pesquisa para encontrar possíveis ferramentas para decodificar uma transmição de fax.
Foi encontrado um utilitário chamado spandsp (https://www.soft-switch.org/downloads/spandsp/snapshots/spandsp-20180108.tar.gz), no qual está presente a ferramenta de testes fax_decode.

Após a compilação da ferramenta habilitando os utilitários de teste:

```shell
$ ./configure --enable-tests && make 
```
A decodificação da mensagem foi realizada com sucesso, gerando o arquivo de saida fax_decode.tif (https://github.com/schleuss/writeups/raw/master/CTF-BR/Executive-Order/fax_decode.tif)

```shell
$ ./fax_decode ~/wiretap.wav
```


**CTF-BR{ITU-T_30-pR0toCoL_seNds_b3aut1fuL_IMGs_ovEr_PSTN}**
