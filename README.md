# ☕ CaffeineZone

Aplicação desktop em C# (Windows Forms) que modela a concentração de
cafeína no organismo ao longo do dia, com base em um modelo
farmacocinético de absorção e eliminação, recomendando horários e
tipos de bebida para manter uma janela segura de performance
cognitiva.

> Projeto desenvolvido como Trabalho de Conclusão de Curso — Engenharia
> de Software, UNINTER.

## 📌 Sobre o projeto

O usuário registra o horário e o tipo de bebida consumida. O sistema
calcula a curva de concentração de cafeína no sangue ao longo do
tempo, somando o efeito de múltiplas doses, e exibe:

- Gráfico da concentração estimada (mg) por hora do dia
- Zona segura visual (verde: 40–300 mg | vermelho: acima de 300 mg)
- Recomendação do próximo horário e tipo de bebida
- Alertas quando a concentração está baixa ou alta demais
- Histórico de consumo do dia

## 🧮 Modelo matemático

O cálculo segue um modelo de dois compartimentos (absorção e
eliminação), com decaimento exponencial:

- **Absorção:** `C_abs(t+1) = C_reservatorio(t) × e^(-1/7)`  
  (meia-vida de absorção: 7 minutos)
- **Eliminação:** `C_sangue(t+1) = C_sangue(t) × e^(-1/240)`  
  (meia-vida de eliminação: 240 minutos)
- **Biodisponibilidade:** F = 1,0
- **Volume de distribuição:** `Vd = 0,6 × peso corporal (kg)`

Múltiplas doses são somadas independentemente, e a curva final é a
sobreposição de todas as curvas individuais.

## 🏗️ Arquitetura

O projeto é organizado em três camadas independentes:

- `CaffeineZone.Core/` → modelos, catálogo de bebidas e algoritmo de cálculo (sem UI)
- `CaffeineZone.App/` → interface Windows Forms
- `CaffeineZone.Tests/` → testes unitários do Core (xUnit)

`App` e `Tests` dependem de `Core`; `Core` não depende de nenhum dos
dois. Essa separação permite testar o algoritmo isoladamente da
interface gráfica.


## 🛠️ Tecnologias

- C# / .NET
- Windows Forms
- xUnit (testes unitários)
- GitHub Actions (build automático)

## 🚀 Como rodar

```bash
git clone https://github.com/<seu-usuario>/caffeinezone.git
cd caffeinezone
dotnet build
dotnet run --project CaffeineZone.App
```

## ✅ Rodando os testes

```bash
dotnet test
```

## 📄 Licença

Projeto acadêmico — TCC de Engenharia de Software (UNINTER).
