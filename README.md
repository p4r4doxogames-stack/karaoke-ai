# Karaokê AI com celular como microfone

Este pacote tem duas versões do mesmo app. As duas têm letra sincronizada, histórico de músicas e um painel **"Celular como microfone"** que toca a voz do celular nas caixas da TV/PC. A diferença está só em **como os dois aparelhos se encontram**.

| | **Versão A** (PeerJS + QR) | **Versão B** (sem servidor) |
|---|---|---|
| Arquivo | `karaoke-ai-celular-A-peerjs-qr.html` | `karaoke-ai-celular-B-sem-servidor.html` |
| Como conecta | Celular escaneia um QR code | Você copia e cola dois códigos |
| Esforço por sessão | Baixo (2 toques) | Médio (vários copiar/colar) |
| Serviço externo de conexão | Sim (servidor público gratuito do PeerJS) | Não |
| Precisa de internet | Sim, nos dois aparelhos | Sim para o YouTube e a letra, mas a conexão entre os aparelhos não depende de servidor próprio |
| Recomendada para | Uso do dia a dia | Quando o servidor do PeerJS estiver fora do ar, ou se você não quer depender dele |

Nas duas versões, o áudio do celular vai **direto de um aparelho para o outro** (WebRTC, criptografado). Só a "apresentação" inicial muda.

---

## Antes de tudo: hospede o arquivo (vale para as duas versões)

O navegador do celular **só libera o microfone em páginas `https://`**. Por isso o arquivo precisa estar numa página de internet, e não apenas salvo no computador. Isso também evita erros do player do YouTube que acontecem em arquivos abertos localmente.

**Passo a passo com o Netlify Drop (gratuito):**

1. No computador, crie uma pasta nova (por exemplo, `karaoke`).
2. Copie para dentro dela **a versão que você vai usar** e **renomeie o arquivo para `index.html`**.
3. Acesse **app.netlify.com/drop** e arraste a **pasta** para a área indicada.
4. O Netlify gera um endereço parecido com `https://nome-aleatorio.netlify.app`. Pode ser que ele peça para criar uma conta gratuita para manter o site no ar; se pedir, crie.
5. Guarde esse endereço. Nos passos abaixo ele aparece como **SEU-ENDEREÇO**.

> Se quiser testar as duas versões, hospede cada uma em uma pasta/site separado.

Use **Chrome, Edge ou Safari** nos dois aparelhos. Abrir o link dentro de outro app (WhatsApp, Instagram, Telegram etc.) usa um navegador embutido que costuma bloquear o microfone. Se isso acontecer, toque em "Abrir no navegador".

---

## Versão A: PeerJS + QR code

### Preparação (uma vez por sessão)

**Na TV/PC**

1. Abra **SEU-ENDEREÇO** no navegador.
2. Role até o cartão **"Celular como microfone"** (fica logo abaixo do campo do link do YouTube).
3. Clique em **Criar sala**. Aparecem:
   - um **QR code**;
   - o endereço da sala, no formato `SEU-ENDEREÇO/#sala=123456`;
   - o status **"aguardando celular"**.

**No celular**

4. Abra a **câmera** e aponte para o QR code da tela. Toque no link que aparecer. (Alternativa: digite o endereço da sala manualmente.)
5. A página abre com o título **"Seu celular é o microfone"**. Toque em **Começar a cantar**.
6. O navegador pede permissão para usar o microfone. Toque em **Permitir**.
7. O celular mostra **"No ar! Cante perto do celular."** e a TV/PC muda para **"conectado"**, com a barrinha de nível se mexendo quando você fala.

### Cantando

8. Na TV/PC, cole o link de um vídeo do YouTube no campo do topo e clique em **Iniciar Karaokê**. A letra sincronizada aparece no palco.
9. Se a letra não for encontrada, preencha **Artista** e **Música** e clique em **Buscar**.
10. Ajuste o **Volume** do microfone no cartão da TV/PC. O botão **Mutar** silencia a voz nas caixas; o botão **Mutar microfone** no celular silencia na origem.

### Para encerrar ou recomeçar

- Feche a aba no celular para desconectar.
- Para uma nova sessão, **recarregue a página da TV/PC** e clique em **Criar sala** de novo (cada sala tem um código novo de 6 dígitos).

### Se algo der errado (Versão A)

| Sintoma | O que fazer |
|---|---|
| "Código da sala ausente" no celular | Você abriu o endereço sem o `#sala=...`. Escaneie o QR code de novo. |
| "Sem acesso ao microfone" | Abra o link no Chrome/Safari (não dentro de outro app) e permita o microfone. No iPhone, confira em Ajustes > Safari > Microfone. |
| Status "falhou, tente de novo" na TV/PC | Recarregue a TV/PC, clique em **Criar sala** e escaneie o novo QR. O servidor público do PeerJS pode estar instável; se persistir, use a Versão B. |
| Aparece um aviso vermelho sobre "arquivo local" | Você abriu o `.html` direto do computador. Abra pelo endereço hospedado. |
| Conectado, mas sem som | Confira o volume do cartão e o volume do sistema. Clique em qualquer lugar da página da TV/PC e tente falar de novo. |
| Não conecta com o celular no 4G | Use o **mesmo Wi-Fi** nos dois aparelhos. Sem servidor de retransmissão (TURN), algumas redes móveis bloqueiam a conexão direta. |

---

## Versão B: sem servidor (copiar e colar)

Aqui não existe QR code nem sala. Os dois aparelhos trocam **dois códigos de texto**, e depois disso a conexão é direta. É mais trabalhoso, mas não depende do servidor do PeerJS.

### Preparação (uma vez por sessão)

**Passo 1. No celular, gere o código**

1. Abra **SEU-ENDEREÇO/#celular** em uma **nova aba** (digite o endereço completo, com `#celular` no final). Se a página já estava aberta e você só acrescentou `#celular`, **recarregue**; mudar só o final do endereço não recarrega a página.
2. Aparece **"Seu celular é o microfone"**. Toque em **Gerar código**.
3. Permita o microfone quando o navegador pedir.
4. Espere 1 a 3 segundos. Aparece uma caixa de texto com um código longo. Toque em **Copiar código**.

**Passo 2. Leve o código até a TV/PC**

5. Envie o código para você mesmo e abra no computador. Opções práticas: "Mensagens salvas" do WhatsApp/Telegram (abrindo o WhatsApp Web ou o Telegram Desktop no PC), e-mail para você mesmo, ou uma nota sincronizada.
6. Copie o código **inteiro**, sem cortar o começo nem o fim.

**Passo 3. Na TV/PC, gere a resposta**

7. Abra **SEU-ENDEREÇO** (sem `#celular`) e vá ao cartão **"Celular como microfone"**.
8. Cole o código na caixa **"Código do celular"** e clique em **Gerar resposta**.
9. Aparece uma segunda caixa com a resposta e o status **"aguardando conexão"**. Clique em **Copiar resposta**.

**Passo 4. Leve a resposta de volta ao celular**

10. Envie a resposta para o celular pelo mesmo caminho do passo 5 e copie.
11. No celular, cole na caixa **"Resposta"** e toque em **Conectar**.
12. Em poucos segundos o celular mostra **"No ar! Cante perto do celular."** e a TV/PC muda para **"conectado"**.

### Cantando

13. Na TV/PC, cole o link do YouTube e clique em **Iniciar Karaokê**.
14. Use o **Volume** e o **Mutar** do cartão, e o botão de mutar do celular, como na Versão A.

### Para encerrar ou recomeçar

- Os códigos valem **para uma única tentativa**. Para reconectar (ou se algo falhar), **recarregue as duas páginas** e refaça os passos 1 a 4.
- Fechar a aba do celular encerra a conexão.

### Se algo der errado (Versão B)

| Sintoma | O que fazer |
|---|---|
| A página do celular mostra o app completo, e não "Seu celular é o microfone" | Faltou o `#celular` no endereço, ou você não recarregou depois de adicioná-lo. |
| "Não conectou. Confira o código e tente de novo." | O código foi colado incompleto, ou foi gerado em outra tentativa. Recarregue as duas páginas e refaça do passo 1. |
| A TV/PC fica em "aguardando conexão" para sempre | Você esqueceu de tocar em **Conectar** no celular, ou a resposta colada no celular está incompleta. |
| "Sem acesso ao microfone" | Mesmo caso da Versão A: abra no Chrome/Safari e permita o microfone. |
| Não conecta | Coloque os dois aparelhos no **mesmo Wi-Fi** e tente de novo. |

---

## Dicas para as duas versões

- **Mantenha a tela do celular ligada** enquanto canta. Ao bloquear a tela, muitos celulares suspendem a página e o microfone para de enviar áudio.
- **Microfonia:** se o celular ficar perto das caixas da TV/PC, a voz pode "voltar" e apitar. Cante longe das caixas, reduza o volume do cartão ou use o botão de mutar quando não estiver cantando. O celular já pede cancelamento de eco ao navegador.
- **Pequeno atraso:** a voz chega às caixas com um atraso curto (tipicamente de algumas dezenas a poucas centenas de milissegundos, dependendo do Wi-Fi). É normal em microfone sem fio por rede.
- **Botão "Ativar Microfone" do palco:** é um recurso antigo do app e serve só para ver o medidor de nível do microfone do próprio aparelho. Ele **não** envia som para as caixas. O áudio do celular vem do cartão "Celular como microfone".
- **Letra fora de tempo ou errada:** o app pega a primeira letra sincronizada que encontra e ela pode ser de outra versão da música (ao vivo, por exemplo). Tente o campo manual de **Artista** e **Música**.
- **Histórico:** as músicas ficam salvas só no navegador daquele aparelho.

## Onde ficam os arquivos

- `karaoke-ai-celular-A-peerjs-qr.html`: Versão A
- `karaoke-ai-celular-B-sem-servidor.html`: Versão B
- `README.md`: este guia
