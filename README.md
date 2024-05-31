# Documentação de Testes de Unidade com xUnit, NUnit e MSTest em .NET 5

## Visão Geral

Este documento apresenta a implementação de testes de unidade em .NET 5 utilizando os frameworks xUnit, NUnit e MSTest. Todos os exemplos focam na mesma funcionalidade: a conversão de temperaturas de Fahrenheit para Celsius, demonstrando diferentes abordagens de codificação e uso de recursos de cada framework.

### Estrutura dos Testes

Cada repositório implementa testes de unidade para um método que converte temperaturas, proporcionando uma base para comparar as abordagens de teste entre xUnit, NUnit e MSTest.

## xUnit

### Características

- **Uso de Atributos**: `Theory` e `InlineData` são usados para testes parametrizados.
- **Compatibilidade**: Suporta o recurso Live Unit Testing do Visual Studio 2019 com .NET 5.

### Exemplo de Código

```csharp
namespace Test.XUnit.Temperatura
{
    public class TestesConversorTemperatura
    {
        [Theory]
        [InlineData(32, 0)]
        [InlineData(47, 8.33)]
        [InlineData(86, 30)]
        [InlineData(90.5, 32.5)]
        [InlineData(120.18, 48.99)]
        [InlineData(212, 100)]
        public void TestarConversaoTemperatura(
            double fahrenheit, double celsius)
        {
            double valorCalculado =
                ConversorTemperatura.FahrenheitParaCelsius(fahrenheit);
            Assert.Equal(celsius, valorCalculado);
        }
    }
}

```
![xunit](https://github.com/CFFricks/aplicando-testes/assets/99102201/9a7eb09d-2534-47ee-80c7-b3499080d480)

## NUnit

### Características

 - **Uso de Atributos**: Emprega o atributo TestCase para realizar testes parametrizados.
### Exemplo de Código

```csharp
using NUnit.Framework;

namespace Temperatura.Testes
{
    public class TestesConversorTemperatura
    {
        [TestCase(32, 0)]
        [TestCase(47, 8.33)]
        [TestCase(86, 30)]
        [TestCase(90.5, 32.5)]
        [TestCase(120.18, 48.99)]
        [TestCase(212, 100)]
        public void TesteConversaoTemperatura(
            double tempFahrenheit, double tempCelsius)
        {
            double valorCalculado =
                ConversorTemperatura.FahrenheitParaCelsius(tempFahrenheit);
            Assert.AreEqual(tempCelsius, valorCalculado);
        }
    }
}
```
![nunit](https://github.com/CFFricks/aplicando-testes/assets/99102201/107143ea-ee52-4079-bc4d-a5eccc4203ab)

## MSTest
### Características
 - **Uso de Atributos**: Utiliza DataTestMethod e DataRow para testes parametrizados.
### Exemplo de Código

```csharp
using Microsoft.VisualStudio.TestTools.UnitTesting;

namespace Temperatura.Testes
{
    [TestClass]
    public class TestesConversorTemperatura
    {
        [DataRow(32, 0)]
        [DataRow(47, 8.33)]
        [DataRow(86, 30)]
        [DataRow(90.5, 32.5)]
        [DataRow(120.18, 48.99)]
        [DataRow(212, 100)]
        [DataTestMethod]
        public void TesteConversaoTemperatura(
            double tempFahrenheit, double tempCelsius)
        {
            double valorCalculado =
                ConversorTemperatura.FahrenheitParaCelsius(tempFahrenheit);
            Assert.AreEqual(tempCelsius, valorCalculado);
        }
    }
}
```
![MStest](https://github.com/CFFricks/aplicando-testes/assets/99102201/8b1e1f41-0816-4e5d-9c27-4c27f5f4afb6)


# Conceitos aprendidos:
### Isolamento de Testes

Aprendi a importância de testar componentes de forma isolada, sem dependência de outros componentes ou configurações externas. Isso ajuda a identificar problemas específicos em partes isoladas do código.

### Testes Parametrizados

O uso de atributos como `InlineData` em xUnit, `TestCase` em NUnit e `DataRow` em MSTest para criar testes parametrizados ensina como executar o mesmo teste com diferentes conjuntos de dados. Isso não só aumenta a cobertura do teste mas também torna o processo mais eficiente.

### Assertivas

Entendi como usar assertivas para validar as condições de teste. Cada framework tem sua forma de assertiva que permite verificar se o resultado esperado corresponde ao resultado real, o que é fundamental para garantir que o código se comporte conforme esperado.
