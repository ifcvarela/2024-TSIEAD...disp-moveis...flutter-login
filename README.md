# 1. Preparação do Ambiente

## 1.1. Baixando o Ambiente Portable

1. Faça o download do arquivo ZIP fornecido, que contém o Flutter, Android SDK, OpenJDK, e VSCode, através do link:
[bit.ly/varela-downloads](https://bit.ly/varela-downloads).

- O nome do arquivo é flutter-win-x64.zip.
Extraia o conteúdo do arquivo ZIP para uma pasta no seu computador.

2. Navegue até a pasta extraída e execute o arquivo run.cmd para iniciar o VSCode já configurado.

> Nota: Certifique-se de que está executando o arquivo run.cmd com permissões adequadas, caso encontre algum problema ao inicializar os componentes.

# 2. Criando o Projeto

## 2.1. Criar o Projeto Flutter

No terminal do VSCode, execute: `flutter create example_client_login` 

E abra a pasta do projeto gerado: `cd example_client_login`

2.2. Instalando os Pacotes Necessários

Adicione os pacotes usados no projeto:

`flutter_svg`: para exibir imagens no formato SVG.

No terminal, execute:

```shell
flutter pub add flutter_svg
```

# 3. Estrutura do Projeto

## 3.1. Arquivos e Pastas

Crie os seguintes arquivos dentro do projeto:

main.dart (em lib/):

Este arquivo inicializa o aplicativo e define as rotas das telas.
login_page.dart (em lib/):

Representa a tela de login.
todo.dart (em lib/):

Representa a tela de To-Do List.
components/todo_listitem.dart (em lib/components/):

Um componente reutilizável que define o layout de um item da lista.

# 4. Código

## 4.1. main.dart

```dart 
import 'package:example_client_login/login_page.dart';
import 'package:example_client_login/todo.dart';
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Login Page',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
        useMaterial3: true,
      ),
      initialRoute: '/',
      routes: {
        '/': (context) => const LoginPage(),
        '/todo': (context) => const ToDo(),
      },
    );
  }
}
```

## 4.2. login_page.dart

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';

class LoginPage extends StatelessWidget {
  const LoginPage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      extendBodyBehindAppBar: true,
      appBar: AppBar(
        toolbarHeight: 100,
        title: Align(
          alignment: Alignment.center,
          child: SvgPicture.asset("assets/logo.svg"),
        ),
        elevation: 0,
        backgroundColor: Colors.transparent,
      ),
      body: Container(
        padding: const EdgeInsets.all(30),
        decoration: const BoxDecoration(
          gradient: LinearGradient(
            colors: [
              Colors.deepPurple,
              Colors.pinkAccent,
            ],
          ),
        ),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            const SizedBox(height: 30),
            const Column(
              children: [
                Text(
                  "Bem Vindo",
                  style: TextStyle(
                      color: Colors.white, fontWeight: FontWeight.bold),
                ),
                Text(
                  "Por favor, insira suas credenciais para acessar sua conta.",
                  style: TextStyle(color: Colors.white),
                ),
              ],
            ),
            const SizedBox(height: 30),
            const CupertinoTextField(
              padding: EdgeInsets.all(20),
              placeholder: "Digite seu login",
              placeholderStyle: TextStyle(color: Colors.white70, fontSize: 14),
              style: TextStyle(color: Colors.white, fontSize: 14),
              decoration: BoxDecoration(
                color: Colors.black12,
                borderRadius: BorderRadius.all(Radius.circular(7)),
              ),
            ),
            const SizedBox(height: 5),
            const CupertinoTextField(
              padding: EdgeInsets.all(20),
              placeholder: "Digite sua senha",
              placeholderStyle: TextStyle(color: Colors.white70, fontSize: 14),
              style: TextStyle(color: Colors.white, fontSize: 14),
              decoration: BoxDecoration(
                color: Colors.black12,
                borderRadius: BorderRadius.all(Radius.circular(7)),
              ),
            ),
            const SizedBox(height: 30),
            Row(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Flexible(
                  flex: 2,
                  child: CupertinoButton(
                    color: Colors.transparent,
                    child: const Text(
                      "Cadastrar-se",
                      style: TextStyle(
                        color: Colors.black87,
                        fontSize: 14,
                      ),
                    ),
                    onPressed: () {},
                  ),
                ),
                const SizedBox(width: 20),
                Flexible(
                  flex: 1,
                  child: CupertinoButton(
                    padding: const EdgeInsets.symmetric(horizontal: 30),
                    color: Colors.greenAccent,
                    child: const Text(
                      "Entrar",
                      style: TextStyle(
                        color: Colors.black87,
                        fontSize: 14,
                      ),
                    ),
                    onPressed: () {
                      Navigator.pushNamed(context, "/todo");
                    },
                  ),
                ),
              ],
            )
          ],
        ),
      ),
    );
  }
}
```

## 4.3. todo.dart

```dart
import 'package:example_client_login/components/todo_listitem.dart';
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

class ToDo extends StatelessWidget {
  const ToDo({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: const Color(0xFFD6D6D6),
      appBar: AppBar(
        title: const Text("TO DO"),
      ),
      body: Container(
        padding: const EdgeInsets.all(30),
        child: Column(
          children: [
            const SizedBox(height: 10),
            Row(
              children: [
                const Flexible(
                  child: CupertinoTextField(
                    placeholder: "O que você precisa fazer?",
                    padding: EdgeInsets.symmetric(vertical: 17, horizontal: 15),
                  ),
                ),
                const SizedBox(width: 15),
                CupertinoButton(
                  color: Colors.black,
                  borderRadius: BorderRadius.circular(100),
                  child: const Icon(Icons.add),
                  onPressed: () {},
                ),
              ],
            ),
            const SizedBox(height: 15),
            const Expanded(
              child: SingleChildScrollView(
                child: Column(
                  children: [
                    TodoListItem(text: "Texto do item da lista..."),
                  ],
                ),
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

## 4.4. components/todo_listitem.dart

```dart
import 'package:flutter/material.dart';

class TodoListItem extends StatelessWidget {
  final String text;

  const TodoListItem({super.key, required this.text});

  @override
  Widget build(BuildContext context) {
    return SizedBox(
      height: 60,
      child: Container(
        padding: const EdgeInsets.all(10),
        decoration: BoxDecoration(
          color: Colors.white,
          borderRadius: BorderRadius.circular(5),
        ),
        child: Row(
          children: [
            const Icon(Icons.check_circle_outline),
            const SizedBox(width: 10),
            Expanded(child: Text(text)),
            const SizedBox(width: 10),
            const Icon(Icons.edit_outlined),
            const SizedBox(width: 10),
            const Icon(Icons.delete_outline),
          ],
        ),
      ),
    );
  }
}
```

# 5. Atividade: Transformando os CupertinoTextField em Componentes Reutilizáveis

Nesta atividade, você será desafiado a refatorar o código da tela de login, transformando os campos de entrada (CupertinoTextField) em componentes reutilizáveis. O objetivo é criar um componente separado que possa ser usado sempre que você precisar de um campo de texto com o estilo e o comportamento do CupertinoTextField.

**Passos para realizar a atividade:**

- 1. **Identifique os CupertinoTextField na tela de login**
  - Na tela de login, existem dois campos de texto do tipo CupertinoTextField: um para o campo de "login" e outro para a "senha". Esses dois campos têm propriedades muito semelhantes, como o estilo e a decoração, e são usados de forma idêntica.

- 2. **Crie um novo arquivo de componente**
  - Crie um novo arquivo Dart na pasta lib/components (se a pasta não existir, crie-a). Nomeie esse arquivo de custom_text_field.dart.

- 3. **Transforme o CupertinoTextField em um componente reutilizável**
  - No arquivo custom_text_field.dart, crie uma classe que representa o CupertinoTextField de forma reutilizável. A ideia é que esse componente aceite parâmetros, como o placeholder, o decoration, e o onChanged para personalizar o comportamento conforme necessário.

Exemplo de como criar o componente:

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

class CustomTextField extends StatelessWidget {
  final String placeholder;
  final TextEditingController controller;
  final bool obscureText;

  const CustomTextField({
    Key? key,
    required this.placeholder,
    required this.controller,
    this.obscureText = false,
  }) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return CupertinoTextField(
      controller: controller,
      placeholder: placeholder,
      obscureText: obscureText,
      padding: const EdgeInsets.all(20),
      placeholderStyle: const TextStyle(color: Colors.white70, fontSize: 14),
      style: const TextStyle(color: Colors.white, fontSize: 14),
      decoration: BoxDecoration(
        color: Colors.black12,
        borderRadius: BorderRadius.all(Radius.circular(7)),
      ),
    );
  }
}
```

- 4. **Utilize o novo componente na tela de login**
  - No arquivo login_page.dart, substitua os CupertinoTextField originais pela nova classe CustomTextField que você criou. Lembre-se de passar os parâmetros necessários, como o placeholder e o controller, para o novo componente.

Exemplo de como usar o componente:

```dart
import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';
import 'package:example_client_login/components/custom_text_field.dart';

class LoginPage extends StatelessWidget {
  const LoginPage({super.key});

  final TextEditingController loginController = TextEditingController();
  final TextEditingController passwordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      extendBodyBehindAppBar: true,
      appBar: AppBar(
        toolbarHeight: 100,
        title: const Text("Login"),
        elevation: 0,
        backgroundColor: Colors.transparent,
      ),
      body: Container(
        padding: const EdgeInsets.all(30),
        decoration: const BoxDecoration(
          gradient: LinearGradient(
            colors: [
              Colors.deepPurple,
              Colors.pinkAccent,
            ],
          ),
        ),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            const SizedBox(height: 30),
            const Column(
              children: [
                Text(
                  "Bem Vindo",
                  style: TextStyle(color: Colors.white, fontWeight: FontWeight.bold),
                ),
                Text(
                  "Por favor, insira suas credenciais para acessar sua conta.",
                  style: TextStyle(color: Colors.white),
                ),
              ],
            ),
            const SizedBox(height: 30),
            CustomTextField(
              controller: loginController,
              placeholder: "Digite seu login",
            ),
            const SizedBox(height: 5),
            CustomTextField(
              controller: passwordController,
              placeholder: "Digite sua senha",
              obscureText: true,
            ),
            const SizedBox(height: 30),
            Row(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Flexible(
                  flex: 2,
                  child: CupertinoButton(
                    color: Colors.transparent,
                    child: const Text(
                      "Cadastrar-se",
                      style: TextStyle(color: Colors.black87, fontSize: 14, fontWeight: FontWeight.w400),
                    ),
                    onPressed: () {},
                  ),
                ),
                const SizedBox(width: 20),
                Flexible(
                  flex: 1,
                  child: CupertinoButton(
                    padding: const EdgeInsets.symmetric(horizontal: 30),
                    color: Colors.greenAccent,
                    child: const Text(
                      "Entrar",
                      style: TextStyle(color: Colors.black87, fontSize: 14, fontWeight: FontWeight.w600),
                    ),
                    onPressed: () {
                      Navigator.pushNamed(context, "/todo");
                    },
                  ),
                ),
              ],
            )
          ],
        ),
      ),
    );
  }
}
```

- 5. **Teste a aplicação**
  - Agora, ao rodar o aplicativo, você verá que os campos de texto estão mais organizados e o código da tela de login ficou mais limpo. O melhor de tudo é que, caso precise de um campo de texto em outra parte do aplicativo, basta reutilizar o CustomTextField.

Essa atividade tem como objetivo melhorar a organização do código, criando componentes reutilizáveis que podem ser facilmente adaptados e utilizados em outros lugares do seu projeto, além de praticar os conceitos de modularização e reutilização de componentes.


