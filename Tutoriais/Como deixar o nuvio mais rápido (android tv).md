<a name="topo"></a>

<div align="center">

  <img src="https://github.com/user-attachments/assets/25a5f09e-9f1f-417d-9e72-006805a0abe7" alt="Nuvio" width="550" />

  <br />
</div>

<h1 align="center">Como deixar o nuvio mais rápido (Android tv)</h1>

### ❓ Por que ocorre essa lentidão?

Isso já foi comentado em várias outras publicações, mas, basicamente, acontece porque os aplicativos instalados pela Play Store utilizam os Baseline Profiles do Google para pré-compilar partes do código durante a instalação, enquanto APKs instalados por sideload dependem de uma compilação mais lenta realizada durante a execução. Essencialmente, a versão da Play Store recebe otimizações que acontecem automaticamente. Usando o ADB (uma opção destinada a desenvolvedores), você pode forçar sua TV a compilar previamente o Nuvio para código de máquina nativo, obtendo o desempenho da versão da Play Store sem perder o suporte a trailers.

## ✅ Pré-requisitos

Um PC com Windows 10 ou 11 conectado à mesma rede Wi-Fi da sua TV/Firestick. Nuvio já instalado na TV.

### 📥 Etapa 1: Instalar o ADB no PC

- Passo 1: Clique com o botão direito no menu Iniciar do Windows e selecione PowerShell ou Prompt de Comando. 
- Passo 2: Execute este comando para instalar as ferramentas oficiais do Android: `winget install Google.PlatformTools`
- Passo 3: Digite Y e pressione Enter caso seja solicitado que você aceite os termos. 
- Passo 4: Feche e abra novamente a janela do terminal. 
- Passo 5: Verifique se a instalação foi realizada corretamente: adb version

### 📺 Etapa 2: Ativar a depuração ADB na Android TV / Firestick

Para Android TV / Google TV: 

- Passo 1: Vá para Configurações > Sistema / Preferências do dispositivo > Sobre. 
- Passo 2: Role até Compilação do Android TV OS e pressione o botão do controle remoto 7 vezes, até aparecer a mensagem `"Agora você é um desenvolvedor".` 
- Passo 3: Volte um nível no menu, entre em Opções do desenvolvedor e ative Depuração pela rede (ou Depuração USB). 
- Passo 4: Vá para Configurações > Rede e Internet e anote o endereço IP da sua TV. `Por exemplo: 192.168.1.50.`

Para Amazon Fire TV Stick (modelos baseados em Android): 

- Passo 1: Vá para Configurações > Minha Fire TV > Sobre. 
- Passo 2: Clique no nome do seu Firestick 7 vezes para desbloquear as Opções do Desenvolvedor. 
- Passo 3: Volte para Minha Fire TV > Opções do Desenvolvedor e ative Depuração ADB. 
- Passo 4: Vá para Minha Fire TV > Sobre > Rede e anote o endereço IP.

### 🔗 Etapa 3: Conectar o PC à TV

No terminal do PC, execute o seguinte comando (substitua pelo endereço IP real da sua TV): `adb connect 192.168.1.50:5555`.

⚠️ Olhe para a tela da TV! Aparecerá uma janela solicitando autorização para a conexão. Selecione "Sempre permitir deste computador" e pressione OK.

### ⚡ Etapa 4: Executar o comando de compilação

Execute exatamente este comando para forçar a compilação nativa completa: `adb shell pm compile -m speed -f com.nuvio.tv`.

Aguarde aproximadamente 10 a 30 segundos. O terminal exibirá Success quando o processo terminar. Abra o Nuvio na TV: os atrasos na inicialização a frio, engasgos da interface e lentidão no carregamento dos pôsteres deverão desaparecer. Caso o nome do pacote esteja incorreto, execute: `adb shell pm list packages | findstr /i nuvio`. 

Depois, identifique nessa lista o nome correto do pacote do Nuvio.

## ❓ Perguntas frequentes

- Vou perder minhas configurações, login da conta ou suporte a trailers? Não. Esse procedimento apenas otimiza a maneira como o processador da TV executa o código do aplicativo. Nenhuma configuração, dado do aplicativo ou mecanismo de reprodução de mídia é alterado.

- Preciso fazer isso toda vez que abrir o Nuvio? Não. Você só precisa executar o procedimento uma vez após cada atualização. Atualizar o Nuvio substitui os arquivos do aplicativo, então será necessário repetir as Etapas 3 e 4 depois de instalar uma nova versão do APK.

- Isso utiliza espaço adicional de armazenamento? Sim. O procedimento adiciona aproximadamente 30 MB a 60 MB de código compilado nativamente ao armazenamento interno da TV, o que não deve ser um problema para a grande maioria dos dispositivos.

## 📱 Não tem PC? Faça pelo celular Android

Se você não tiver um computador, também pode executar esse comando utilizando um celular Android conectado à mesma rede Wi-Fi da TV. Baixe um aplicativo de ADB Shell. Infelizmente existem muitas opções, então escolha um depois de fazer sua própria pesquisa. Pessoalmente, eu recomendaria o Termux e, nele, executaria o comando: `pkg install android-tools`

Digite o endereço IP da sua TV (ou use `adb connect <IP do dispositivo>` no Termux), mantenha a porta como 5555 e toque em Connect/Conectar. Aceite a janela de autorização que aparecerá na tela da TV (Sempre permitir → OK). Na caixa do terminal do celular, execute o seguinte comando. Atenção: não inclua adb shell no início caso esteja utilizando aplicativos móveis específicos de ADB; no Termux, inclua adb shell.

Em aplicativos ADB Shell: `pm compile -m speed -f com.nuvio.tv`

No Termux: `adb shell pm compile -m speed -f com.nuvio.tv`

Aguarde aproximadamente 10 a 30 segundos, até aparecer a mensagem: Success
