# UMANO - Jitsi Meet SDK Android 1.0.3

Corrige a libertação nativa de capturas e ligações WebRTC quando o runtime React
é destruído. O encerramento não depende de o JavaScript ainda conseguir executar
as chamadas dispose(). Callbacks e pedidos de captura atrasados são ignorados
depois da invalidação do módulo.

A nova API JitsiMeet.destroyReactNative(Runnable) chama a conclusão na thread de
UI depois de libertar os recursos WebRTC. A integração UMANO aguarda o evento de
fim da conferência, usa um limite de 5 segundos para a saída normal e mantém o
reconhecimento de voz bloqueado até receber essa confirmação de libertação.

## Publicar

Juntar release/ a release/ de https://github.com/tv4you2016/jitsi-maven-repository,
preservando as pastas de versões anteriores e incluindo todos os AAR/POM,
fontes, metadados e checksums. Coordenadas: org.jitsi.react:jitsi-meet-sdk:1.0.3.
O pacote foi gerado localmente; não faz publicação remota automaticamente.

## Compilar a UMANO antes da publicação

Foi acrescentada a propriedade Gradle opcional umanoJitsiMaven. O valor padrão
continua a ser o repositório GitHub. Para testar o pacote local no Windows:

```powershell
flutter build apk --debug --no-pub --target-platform android-arm64 --android-project-arg=umanoJitsiMaven=file:///C:/Users/IOLine/Documents/GitHub/jitsi-meet/android/.build-tools/maven-1.0.3/release/
```

Depois de publicar 1.0.3, o argumento deixa de ser necessário.

## Validar na box

1. Iniciar uma chamada e confirmar áudio no outro participante.
2. Terminar e verificar que a captura VOICE_COMMUNICATION da UMANO desaparece.
3. Iniciar outra chamada e voltar a confirmar áudio.
4. Repetir saindo pelo botão Voltar e terminando do outro participante.

Com Ajuda por voz contínua ligada, a captura VOICE_RECOGNITION fora da chamada
é esperada e pode manter o indicador de microfone aceso. Essa captura deve
ficar suspensa durante a chamada e retomar depois da libertação do Jitsi.

Os originais dos ficheiros alterados na UMANO foram guardados em
backups/microphone_lifecycle_20261028/. As alterações Flutter e nativas devem
ser mantidas em conjunto com o SDK 1.0.3.
