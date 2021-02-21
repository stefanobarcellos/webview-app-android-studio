# Criando um Aplicativo Webview com o Android Studio

Explica-se aqui como criar um aplicativo de navegador para abrir uma página desejada. Você pode abrir uma página remota ou abrir um arquivo local que ficará guardado dentro do app. Vamos por a mão na massa?

## 1. Criando o projeto

- Abra o Android Studio.
- Crie um novo projeto.
- Selecione uma atividade vazia (empty activity).
- Defina um nome para o app, um nome para o pacote, pasta para salvar o projeto, Java como linguagem, API mínima como 16.
- Prossiga para abrir o seu projeto.

## 2. Editando o arquivo AndroidManifest.xml

- Com o seu projeto criado e aberto no Android Studio, abra o arquivo AndroidManifest.xml
- Caso seu app for abrir uma página remota, antes da Tag <application> adicione o seguinte:

    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>

## 3. Editando o arquivo MainActivity.java

- Primeiro importe:

    import android.webkit.WebSettings;
    import android.webkit.WebView;
    import android.webkit.WebViewClient;

- Adicione logo que iniciar sua classe, dentro dela:

    private WebView mWebView;

- Adicione abaixo do setContentView o seguinte código:

    mWebView = findViewById(R.id.activity_main_webview);
    WebSettings webSettings = mWebView.getSettings();
    webSettings.setJavaScriptEnabled(true); // permite o uso de javascript, deixar como true pode implicar em problemas de segurança
    mWebView.setWebViewClient(new WebViewClient());
    mWebView.loadUrl("https://meusite.com");

- Em loadUrl, substitua https://meusite.com pela página remota que deseja abrir.

## 4. Editando o arquivo activity_main.xml

- Remova todo o TextView que já vem no arquivo e coloque no lugar o seguinte código:

        <WebView
        android:id="@+id/activity_main_webview"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

- Pronto, você já pode rodar sua aplicação, ela está pronta!

## 5. Deixando seu app webview em fullscreen (opcional)

- No arquivo themes.xml do seu projeto, procure por:

    DarkActionBar

- Substitua por:

    NoActionBar

- No arquivo MainActivity.java, importe o seguinte:

    import android.view.WindowManager;

- Ainda no arquivo MainActivity.java, adicione acima do setContentView o seguinte código:

    getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN, WindowManager.LayoutParams.FLAG_FULLSCREEN);

- Pronto, agora sua aplicação rodará em fullscreen (tela cheia).

## 5. Carregando um arquivo local (caso deseje)

- Crie um arquivo chamado teste.html em:

    NomeDoApp\app\src\main\assets\teste.html

- Crie a pasta assets se for necessário.

- Adicione o seguinte código HTML no teste.html:

    <h3>Funciona!</h3>

- No arquivo MainActivity.java, altere a string do loadUrl para:

    mWebView.loadUrl("file:///android_asset/teste.html");

- Você pode criar mais páginas dentro da pasta assets e linkar uma com a outra por meio de HTML, sem problemas.

- Pronto, agora sua aplicação webview roda arquivos locais.

## Considerações finais

Espero que você tenha gostado do tutorial. Indico utilizar o https://jquerymobile.com/ na criação dos seus apps baseados em webview. Até a próxima.