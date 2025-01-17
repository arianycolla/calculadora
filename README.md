# calculadora
import 'package:flutter/material.dart';

void main() {
  runApp(MeuApp());
}

class MeuApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Calculadora Flutter',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MinhaPaginaInicial(),
    );
  }
}

class MinhaPaginaInicial extends StatefulWidget {
  @override
  _MinhaPaginaInicialState createState() => _MinhaPaginaInicialState();
}

class _MinhaPaginaInicialState extends State<MinhaPaginaInicial> {
  String resultado = '0';
  String operacao = '';
  double num1 = 0;
  double num2 = 0;

  void calcular(String buttonText) {
    if (buttonText == 'C') {
      resultado = '0';
      operacao = '';
      num1 = 0;
      num2 = 0;
    } else if (buttonText == '+' || buttonText == '-' || buttonText == '*' || buttonText == '/') {
      num1 = double.parse(resultado);
      operacao = buttonText;
      resultado = '0';
    } else if (buttonText == '=') {
      num2 = double.parse(resultado);
      if (operacao == '+') {
        resultado = (num1 + num2).toString();
      } else if (operacao == '-') {
        resultado = (num1 - num2).toString();
      } else if (operacao == '*') {
        resultado = (num1 * num2).toString();
      } else if (operacao == '/') {
        resultado = (num1 / num2).toString();
      }
      operacao = '';
    } else {
      if (resultado == '0') {
        resultado = buttonText;
      } else {
        resultado += buttonText;
      }
    }

    setState(() {});
  }

  Widget construirBotao(String buttonText) {
    return Expanded(
      child: OutlinedButton(
        child: Text(buttonText, style: TextStyle(fontSize: 24)),
        onPressed: () => calcular(buttonText),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Calculadora Responsiva'),
      ),
      body: Column(
        children: [
          Container(
            alignment: Alignment.centerRight,
            padding: EdgeInsets.symmetric(vertical: 24, horizontal: 12),
            child: Text(resultado, style: TextStyle(fontSize: 48)),
          ),
          Expanded(
            child: Divider(),
          ),
          Column(
            children: [
              Row(
                children: ['7', '8', '9', '/'].map(construirBotao).toList(),
              ),
              Row(
                children: ['4', '5', '6', '*'].map(construirBotao).toList(),
              ),
              Row(
                children: ['1', '2', '3', '-'].map(construirBotao).toList(),
              ),
              Row(
                children: ['C', '0', '=', '+'].map(construirBotao).toList(),
              ),
            ],
          ),
        ],
      ),
    );
  }
}
