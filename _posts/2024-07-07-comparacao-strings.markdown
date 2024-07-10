---
layout: post
title:  "Comparação de strings"
date:   2024-07-07 10:37:55 -0300
categories: csharp
---
🐌 Usar 𝗧𝗼𝗨𝗽𝗽𝗲𝗿() e 𝗧𝗼𝗟𝗼𝘄𝗲𝗿() para conversão de caso em C# pode afetar o desempenho devido à alocação de memória, cópia de cadeia de caracteres e possível coleta de lixo, especialmente em situações que envolvem cadeias de caracteres grandes ou conversões frequentes.

🚀 𝗦𝘁𝗿𝗶𝗻𝗴.𝗘𝗾𝘂𝗮𝗹𝘀 é mais rápido que ToUpper() ou ToLower() devido à comparação direta de caracteres, evitando a alocação de memória e reduzindo a sobrecarga para comparação de strings que não diferenciam maiúsculas de minúsculas.

🔥 Para realizar comparação de strings, é melhor usar os métodos de comparação integrados como 𝗦𝘁𝗿𝗶𝗻𝗴.𝗘𝗾𝘂𝗮𝗹𝘀 com opções StringComparison apropriadas, que lidam corretamente com a insensibilidade a maiúsculas e minúsculas e considerações culturais, mantendo melhor desempenho e precisão.

{% highlight csharp %}
    /// <summary>
    /// Desempenho na comparação de string´s
    /// </summary>
    [MemoryDiagnoser]
    public class DesempenhoComparacaoString
    {
        private string str1 = "ComP@rand0 StR1ng´s";
        private string str2 = "ComparandO String´S";

        [Benchmark(Baseline = true)]
        public bool Equals_OrdinalIgnoreCase() => string.Equals(str1, str2, StringComparison.OrdinalIgnoreCase);

        [Benchmark]
        public bool Compare_OrdinalIgnoreCase() => string.Compare(str1, str2, StringComparison.OrdinalIgnoreCase) == 0;

        [Benchmark]
        public bool ToLower() => str1.ToLower() == str2.ToLower();

        [Benchmark]
        public bool ToUpper() => str1.ToUpper() == str2.ToUpper();
    }
{% endhighlight %}
