# UMANO - Jitsi Meet Android SDK 1.0.2

Coordenadas Maven: `org.jitsi.react:jitsi-meet-sdk:1.0.2`.

Inclui deteção de dispositivos USB de áudio, libertação imediata das capturas
existentes ao fechar, proteção contra limpeza de pistas de uma chamada nova,
limpeza ao desmontar a interface e reposição do foco/rota de áudio no Android.

## Publicação

Juntar o conteúdo de `release/` à pasta `release/` do repositório
https://github.com/iolinesw/jitsi-maven-repository, mantendo os artefactos das
versões anteriores. Incluir os módulos React Native e os metadados/checksums,
além do AAR e POM do SDK. Esta preparação local não faz push para o GitHub.

## Integração Flutter

Depois de publicar, atualizar a dependência declarada pelo plugin Jitsi usado
pela UMANO, evitando manter outra versão do SDK declarada nesse plugin:

```groovy
implementation('org.jitsi.react:jitsi-meet-sdk:1.0.2') {
    transitive = true
}
```

Repositório Maven:

```groovy
maven {
    url 'https://raw.githubusercontent.com/iolinesw/jitsi-maven-repository/main/release'
}
```

Esta árvore usa Android mínimo API 26 (Android 8.0), React Native 0.85.2 e Hermes
0.16.0. O SDK inclui arm64-v8a, armeabi-v7a, x86 e x86_64.

Validar na UMANO a saída normal, fecho da página da chamada, falha de ligação e
desligar/voltar a ligar o microfone USB. Os testes locais não substituem estes
testes no equipamento.

## Repetir um build no Windows

Com JDK 17 em JAVA_HOME, Node 24+, dependências npm preparadas e Android SDK em
ANDROID_HOME, executar na raiz do projeto:

```powershell
./android/scripts/build-sdk.ps1 -Version 1.0.3
```

O script gera o SDK e as dependências numa única execução Gradle, sem criar
commits nem publicar no GitHub. Por predefinição escreve em
`android/.build-tools/maven-repository/release/` e recusa substituir uma versão
do SDK já existente nessa pasta.
