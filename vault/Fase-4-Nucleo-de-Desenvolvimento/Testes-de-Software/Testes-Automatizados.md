# Testes Automatizados

> [!info] Metadados
> **Disciplina:** Testes de Software
> **Bloco:** 4.3 — Testes de Software (FASE 4 — Núcleo de Desenvolvimento)
> **Tópico:** 3. Testes Automatizados
> **Subtópicos:** JUnit (anotações, asserts, suítes de teste) · Mockito (mocks e stubs) · Selenium (testes de UI web — conceito) · Cobertura de código (métricas e ferramentas)
> **Pré-requisitos:** [[Fundamentos-de-Teste|Fundamentos de Teste]] (níveis, tipos, estratégias) · [[Testes-Ageis|Testes Ágeis]] (TDD, ciclo Red-Green-Refactor) · [[Java-e-Ecossistema-JVM|Java/JVM]] (linguagem, bibliotecas) · [[Frameworks-Java|Spring]] (conceito de DI, container)
> **Cargo:** Analista de TI — Perfil 3 (Desenvolvimento de Software) · DATAPREV 2026
> **Data:** 2026-08-31

---

## 1. Por que estudar testes automatizados?

No [[Testes-Ageis|tópico anterior]] vimos **TDD** e **BDD** como métodos — mas métodos precisam de **ferramentas**. O TDD diz "escreva um teste antes do código" — mas *como* se escreve um teste em Java? O BDD diz "especifique em linguagem natural" — mas *como* se conecta isso ao código? É aqui que entram os **testes automatizados**: a camada técnica que torna os testes **executáveis, reproduzíveis e rápidos**.

Para a DATAPREV, a automação de testes é especialmente relevante: sistemas legados de benefícios previdenciários têm **milhares de regras de negócio**, e manualmente testar todas as combinações seria impossível. Um suite automatizado de testes unitários pode rodar em **segundos** e garantir que nenhuma mudança quebrou as regras existentes — o chamado **teste de regressão** (que você viu no [[Fundamentos-de-Teste]]).

> [!question] Pergunta orientadora
> Imagine que você precisa alterar a fórmula de cálculo de um benefício. Como garantir que a alteração não quebrou o cálculo de outros benefícios? Rodar todos os testes anteriores manualmente levaria dias. Rodá-los **automaticamente** leva minutos. É essa a promessa dos testes automatizados.

---

## 2. JUnit — o framework de testes do Java

### 2.1 O que é JUnit?

O **JUnit** é a biblioteca padrão para **testes unitários em Java**. A versão atual é o **JUnit 5** (também chamado de JUnit Jupiter). Quando você viu [[Frameworks-Java|Spring]] e a anotação `@Autowired`, o JUnit é a ferramenta que permite testar classes Spring de forma isolada — criando contextos de teste, injetando mocks, e verificando comportamentos.

O JUnit se integra perfeitamente com o ciclo **Red-Green-Refactor** do [[Testes-Ageis|TDD]]: você escreve o teste com JUnit (Red), escreve o código (Green), e o JUnit confirma que tudo passa.

### 2.2 Anotações principais do JUnit 5

| Anotação | Função | Quando usar |
|---|---|---|
| **`@Test`** | Marca um método como **teste** | Em todo método que executa um teste |
| **`@BeforeEach`** | Executa **antes de cada** teste | Configuração que se repete (criar objetos, limpar estado) |
| **`@AfterEach`** | Executa **depois de cada** teste | Limpeza (fechar conexões, restaurar estado) |
| **`@BeforeAll`** | Executa **uma vez antes** de todos os testes da classe | Configuração custosa (criar banco de dados em memória) |
| **`@AfterAll`** | Executa **uma vez depois** de todos os testes | Limpeza global |
| **`@Disabled("motivo")`** | Desativa um teste temporariamente | Quando um teste não deve rodar (ex: aguardando correção) |
| **`@ParameterizedTest`** | Executa o mesmo teste com **diferentes entradas** | Quando quer testar múltiplos valores (tabela de entrada) |
| **`@DisplayName("texto")`** | Dá um nome **legível** ao teste | Para tornar os relatórios mais compreensíveis |

### 2.3 Exemplo completo: JUnit 5 em ação

```java
import org.junit.jupiter.api.*;
import static org.junit.jupiter.api.Assertions.*;

class CalculadoraBeneficioTest {

    private CalculadoraBeneficio calculadora;

    @BeforeEach
    void setUp() {
        // Executa ANTES de cada teste — cria instância limpa
        calculadora = new CalculadoraBeneficio();
    }

    @Test
    @DisplayName("Deve calcular valor do benefício corretamente")
    void calcularValor_CasoNormal_RetornaValorCorreto() {
        double resultado = calculadora.calcularValor(30, 1500.00);
        assertEquals(45000.00, resultado, 0.01); // tolerância de 0.01
    }

    @Test
    @DisplayName("Deve lançar exceção quando anos de contribuição for negativo")
    void calcularValor_AnosNegativos_LancaExcecao() {
        assertThrows(IllegalArgumentException.class,
            () -> calculadora.calcularValor(-1, 1500.00));
    }

    @Test
    @DisplayName("Deve retornar zero quando salário for zero")
    void calcularValor_SalarioZero_RetornaZero() {
        assertEquals(0.0, calculadora.calcularValor(30, 0.0), 0.01);
    }

    @AfterEach
    void tearDown() {
        calculadora = null; // limpeza após cada teste
    }
}
```

> [!important] `assertEquals` com tolerância
> Ao comparar valores `double`, sempre use a **tolerância** (terceiro parâmetro): `assertEquals(45000.00, resultado, 0.01)`. Isso evita falsos negativos causados por arredondamento de ponto flutuante. A banca cobra isso — se você compara `double` sem tolerância, o teste pode falhar mesmo com o código correto.

### 2.4 Asserts principais

| Assert | O que verifica |
|---|---|
| `assertEquals(esperado, real)` | Os dois valores são **iguais** |
| `assertNotEquals(esperado, real)` | Os dois valores são **diferentes** |
| `assertTrue(condição)` | A condição é **verdadeira** |
| `assertFalse(condição)` | A condição é **falsa** |
| `assertNull(objeto)` | O objeto é **null** |
| `assertNotNull(objeto)` | O objeto **não é null** |
| `assertThrows(TipoExceção.class, executable)` | Uma exceção do tipo especificado é **lançada** |
| `assertArrayEquals(esperado, real)` | Dois arrays são **iguais** |

> [!warning] PEGADINHA — anotação JUnit vs. assert
> A banca pode trocar os papéis: "A anotação `@Test` verifica se o método retorna o valor correto." **Falso.** `@Test` apenas **marca** o método como teste — quem verifica o valor são os **asserts** (`assertEquals`, `assertTrue`, etc.). São coisas completamente diferentes: `@Test` = "isso é um teste" · `assertEquals` = "isso está correto".

### 2.5 Suítes de teste

Uma **suíte de teste** agrupa vários testes para serem executados **em conjunto**. No JUnit 5:

```java
import org.junit.platform.suite.api.SelectClasses;
import org.junit.platform.suite.api.Suite;

@Suite
@SelectClasses({
    CalculadoraBeneficioTest.class,
    ValidadorAposentadoriaTest.class,
    ServicoBeneficioTest.class
})
class SuiteTestesBeneficio {
    // Esta classe é apenas um "agrupador" — não tem testes próprios
}
```

A suíte permite rodar **todos os testes de um módulo** com um único comando — essencial em pipelines de CI/CD ([[DevOps-e-Controle-de-Versao|DevOps]]).

---

## 3. Mockito — isolando dependências com mocks

### 3.1 O problema: como testar classes com dependências?

Imagine que você quer testar um `ServicoBeneficio` que depende de um `RepositorioBeneficio` (que acessa o banco de dados):

```java
@Service
public class ServicoBeneficio {
    @Autowired
    private RepositorioBeneficio repositorio;

    public Beneficiario buscarPorCpf(String cpf) {
        return repositorio.findByCpf(cpf);
    }
}
```

Para testar `buscarPorCpf`, você precisaria de um **banco de dados real** — o que tornaria o teste lento, frágil e dependente de infraestrutura. A solução: **substituir** o repositório por um objeto falso que retorna dados pré-definidos. É aí que entra o **Mockito**.

### 3.2 O que é um Mock?

Um **mock** é um **objeto falso** que se comporta como o objeto real, mas que você **controla** — você define o que ele deve retornar quando chamado. O Mockito cria esses mocks automaticamente.

> [!question] Mock, Stub ou Fake — qual a diferença?
> A banca adora cobrar essa distinção:

| Conceito | O que é | Exemplo |
|---|---|---|
| **Stub** | Objeto que retorna **dados pré-definidos** — não tem lógica | Um repositório falso que sempre retorna o mesmo beneficiário |
| **Mock** | Objeto que pode ser **verificado** — você confirma que métodos específicos foram chamados com argumentos específicos | Um repositório falso que verifica se `findByCpf("123")` foi chamado |
| **Fake** | Objeto com **implementação funcional simplificada** — funciona, mas de forma mais simples que o real | Um banco de dados em memória (H2) que simula Oracle |

> [!warning] PEGADINHA — mock vs. stub vs. fake
> Essa é uma das **pegadinhas mais comuns** da FGV. Resumo rápido: **stub** = dado pré-definido (não verifica nada); **mock** = objeto que você **verifica** se foi chamado corretamente; **fake** = implementação simplificada mas funcional. Na prática com Mockito, o que você cria é **mock** (com `@Mock`) — e o **stub** é o comportamento que você configura com `when(...).thenReturn(...)`.

### 3.3 Mockito em ação

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

import static org.junit.jupiter.api.Assertions.*;
import static org.mockito.Mockito.*;

@ExtendWith(MockitoExtension.class)  // ativa o Mockito no JUnit 5
class ServicoBeneficioTest {

    @Mock
    private RepositorioBeneficio repositorio;  // cria um mock do repositório

    @InjectMocks
    private ServicoBeneficio servico;          // injeta o mock no serviço

    @Test
    void buscarPorCpf_DeveRetornarBeneficiario() {
        // ARRANGE: configurar o mock (stub)
        Beneficiario esperado = new Beneficiario("João", "12345678900");
        when(repositorio.findByCpf("12345678900")).thenReturn(esperado);

        // ACT: chamar o método que está sendo testado
        Beneficiario resultado = servico.buscarPorCpf("12345678900");

        // ASSERT: verificar o resultado
        assertEquals("João", resultado.getNome());

        // VERIFY: confirmar que o mock foi chamado corretamente
        verify(repositorio, times(1)).findByCpf("12345678900");
    }

    @Test
    void buscarPorCpf_CpfNaoEncontrado_RetornaNull() {
        when(repositorio.findByCpf("00000000000")).thenReturn(null);

        Beneficiario resultado = servico.buscarPorCpf("00000000000");

        assertNull(resultado);
        verify(repositorio).findByCpf("00000000000");
    }
}
```

### 3.4 Anotações e métodos-chave do Mockito

| Anotação/Método | Função |
|---|---|
| **`@Mock`** | Cria um **objeto mock** (falso) |
| **`@InjectMocks`** | Cria a classe real e **injeta** os mocks nos campos `@Mock` |
| **`when(...).thenReturn(...)`** | Configura o **stub** — "quando chamado com X, retorne Y" |
| **`verify(mock).metodo()`** | Verifica se o mock foi **chamado** |
| **`verify(mock, times(n))`** | Verifica se foi chamado **n vezes** |
| **`verify(mock, never())`** | Verifica se **nunca** foi chamado |
| **`verifyNoMoreInteractions(mock)`** | Verifica que **nenhum outro método** foi chamado no mock |

> [!important] `@InjectMocks` vs. `@Autowired`
> `@Autowired` é do **Spring** (injeta dependências reais no contexto da aplicação). `@InjectMocks` é do **Mockito** (injeta mocks no contexto do teste). São anotações de **ferramentas diferentes** com o mesmo objetivo — mas contextos completamente distintos. A banca troca uma pela outra.

---

## 4. Selenium — testes de UI web

### 4.1 O que é Selenium?

O **Selenium** é uma ferramenta que **automatiza um navegador web** para testar a **interface do usuário** — ele abre um navegador (Chrome, Firefox), navega para uma URL, clica em botões, preenche campos e verifica resultados. É a ferramenta por excelência para testes **E2E (End-to-End)** e de **aceitação** de sistemas web.

> [!note] Selenium e a pirâmide de testes
> Na [[Testes-Ageis|pirâmide de testes]], o Selenium opera no **ponto** — os testes E2E/Aceitação. São poucos, lentos e frágeis (dependem do navegador, da rede, da UI). Por isso, não se deve abusar de Selenium: o ideal é ter **muitos testes unitários** (JUnit) e **poucos testes E2E** (Selenium).

### 4.2 WebDriver — o conceito central

O Selenium usa o **WebDriver** — uma API que se comunica com o navegador para simular interações do usuário. O fluxo básico é:

1. Criar uma instância do WebDriver (abrir o navegador);
2. Navegar para uma URL;
3. Localizar elementos da página (por ID, classe, XPath, CSS selector);
4. Interagir (clicar, digitar, submeter);
5. Verificar o resultado esperado;
6. Fechar o navegador.

```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

class PaginaLoginTest {

    void deveLogarComSucesso() {
        WebDriver driver = new ChromeDriver();  // abre o Chrome

        driver.get("https://sistema.dataprev.gov.br/login");  // navega

        // Localiza os campos e preenche
        WebElement campoUsuario = driver.findElement(By.id("usuario"));
        campoUsuario.sendKeys("admin");

        WebElement campoSenha = driver.findElement(By.id("senha"));
        campoSenha.sendKeys("senha123");

        // Clica no botão de login
        WebElement botaoLogin = driver.findElement(By.id("btn-login"));
        botaoLogin.click();

        // Verifica se redirecionou para a página inicial
        String titulo = driver.getTitle();
        assertEquals("Sistema de Benefícios", titulo);

        driver.close();  // fecha o navegador
    }
}
```

> [!question] Selenium testa o quê — código ou comportamento?
> Selenium testa o **comportamento observável na interface** — ele não conhece o código-fonte. É, por definição, uma estratégia de **caixa-preta**. Ele valida: "o usuário clica no botão de login e é redirecionado?" — não valida como o backend processou a requisição.

### 4.3 Selenium vs. testes unitários

| Critério | JUnit (unitário) | Selenium (E2E) |
|---|---|---|
| **Velocidade** | Milissegundos | Segundos/minutos |
| **Escopo** | Método/classe isolada | Fluxo completo (UI + backend + BD) |
| **Fragilidade** | Baixa (sem dependência externa) | Alta (depende de navegador, rede, UI) |
| **Custo de manutenção** | Baixo | Alto (muda a UI = quebra o teste) |
| **Quando usar** | Sempre (base da pirâmide) | Pouco (validação final de fluxos críticos) |

---

## 5. Cobertura de código — métricas e ferramentas

### 5.1 O que é cobertura de código?

**Cobertura de código** mede **quanto do seu código-fonte foi executado** durante a execução dos testes. Se você tem 100 linhas de código e seus testes executaram 80 delas, a cobertura é 80%. É uma métrica de **testes estruturais (caixa-branca)** que você viu no [[Fundamentos-de-Teste]].

### 5.2 Tipos de cobertura

| Métrica | O que mede | Granularidade |
|---|---|---|
| **Cobertura de linha (line coverage)** | Quantas **linhas** foram executadas | Mais simples, mais comum |
| **Cobertura de ramo (branch coverage)** | Quantos **caminhos condicionais** (if/else, switch) foram percorridos | Mais rigorosa — garante que tanto o "true" quanto o "false" do if foram testados |
| **Cobertura de instrução** | Quantas **instruções** da JVM foram executadas | Mais detalhada que linha |
| **Cobertura de método** | Quantos **métodos** foram chamados | Menos granular |

> [!question] 100% de cobertura significa código sem defeitos?
> **Não.** 100% de cobertura significa que toda linha foi *executada* — mas não que todos os **comportamentos** foram validados. Você pode executar uma linha que retorna um valor, mas não verificar se o valor está correto. **Cobertura mede execução, não validação.** É uma métrica útil, mas não é suficiente sozinha.

### 5.3 JaCoCo — a ferramenta de cobertura

O **JaCoCo (Java Code Coverage)** é a ferramenta de cobertura mais usada em projetos Java. Ele se integra com Maven e Gradle e gera relatórios HTML detalhados mostrando quais linhas, branches e métodos foram cobertos.

No **Maven**, basta adicionar o plugin:

```xml
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>0.8.11</version>
    <executions>
        <execution>
            <goals>
                <goal>prepare-agent</goal>
            </goals>
        </execution>
        <execution>
            <id>report</id>
            <phase>test</phase>
            <goals>
                <goal>report</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

Ao rodar `mvn test`, o JaCoCo gera um relatório em `target/site/jacoco/index.html` com a cobertura detalhada.

### 5.4 O que é um "bom" percentual de cobertura?

| Percentual | Avaliação |
|---|---|
| **< 50%** | Crítico — muitas lacunas, risco alto |
| **50% – 70%** | Aceitável para projetos pequenos |
| **70% – 80%** | Bom para projetos corporativos |
| **80% – 90%** | Muito bom (META COMUM em times ágeis) |
| **> 90%** | Excelente (mas pode ser difícil de manter em projetos grandes) |
| **100%** | Difícil e nem sempre necessário — mas a banca cobra o conceito |

> [!tip] Regra prática para a prova
> Se a questão perguntar "qual é uma meta razoável de cobertura de código?", a resposta é **80%** — é o valor mais citado na literatura e o mais cobrado em concursos. Mas lembre: cobertura alta **não garante** ausência de defeitos — é apenas uma métrica, não um certificado.

---

## 6. Como a FGV cobra testes automatizados

- **JUnit** cai em questões práticas: "Qual anotação marca um método como teste?" (`@Test`), "Qual assert verifica igualdade?" (`assertEquals`).
- **Mockito** é o alvo mais rentável: a distinção mock vs. stub vs. fake é **muito cobrada**, e a banca descreve cenários onde você precisa identificar qual técnica se aplica.
- **Selenium** aparece em questões conceituais: "Qual ferramenta automatiza testes de UI web?" — e a distinção entre Selenium e JUnit (E2E vs. unitário).
- **Cobertura de código** cai em métricas: "O que é cobertura de ramo?" e "100% de cobertura significa código sem defeitos?" (não).

> [!warning] PEGADINHA — as cinco armadilhas mais rentáveis
> (1) **`@Test` não verifica nada** — marca o método; quem verifica é o `assert`. (2) **Mock ≠ stub** — mock verifica se foi chamado; stub retorna dado pré-definido. (3) **`@InjectMocks` ≠ `@Autowired`** — um é Mockito, o outro é Spring. (4) **Cobertura de linha ≠ validação** — executar ≠ testar corretamente. (5) **Selenium = caixa-preta** — testa comportamento na UI, não o código interno.

---

## 7. Resumo e pontos-chave

> [!tip] Checklist de revisão
> - [ ] **JUnit 5:** `@Test` (marca teste), `@BeforeEach` (antes de cada), `@AfterEach` (depois de cada), `@BeforeAll/@AfterAll` (uma vez), `@Disabled` (desativa), `@DisplayName` (nome legível)
> - [ ] **Asserts:** `assertEquals`, `assertTrue`, `assertFalse`, `assertNull`, `assertNotNull`, `assertThrows` — sempre com tolerância para `double`
> - [ ] **Mockito:** `@Mock` (cria mock), `@InjectMocks` (injeta mocks), `when().thenReturn()` (stub), `verify()` (verifica chamada)
> - [ ] **Mock vs Stub vs Fake:** mock = verificação · stub = dado pré-definido · fake = implementação simplificada funcional
> - [ ] **Selenium:** automatiza navegador (Chrome/Firefox) via **WebDriver**; caixa-preta; teste de UI/E2E; lento e frágil — usar com moderação
> - [ ] **Cobertura de código:** mede execução, não validação; tipos: linha, ramo, instrução, método; ferramenta: JaCoCo; meta comum: 80%
> - [ ] **100% cobertura ≠ código sem defeitos** — cobertura mede execução, não qualidade da validação

> [!question] Revise mentalmente
> Para testar a `ServicoBeneficio` que depende de `RepositorioBeneficio`, qual ferramenta você usar para isolar o repositório? *(Resposta: Mockito — cria um `@Mock` do repositório e injeta no serviço com `@InjectMocks`, configurando o comportamento com `when().thenReturn()`.)*

---

## 8. Próximos passos

Você agora domina as ferramentas de teste automatizado: JUnit para unitários, Mockito para isolar dependências e Selenium para E2E. No próximo tópico, vamos estudar como **gerenciar** todo esse processo: planos de teste, registro de defeitos, métricas e relatórios — a [[Gestao-do-Ciclo-de-Vida-de-Testes|Gestão do Ciclo de Vida de Testes]].
