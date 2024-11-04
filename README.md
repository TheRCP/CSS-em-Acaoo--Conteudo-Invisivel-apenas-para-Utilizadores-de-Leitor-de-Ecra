## CSS em Acção: Conteúdo Invisível apenas para Utilizadores de Leitor de Ecrã.

### Introdução

A grande maioria das técnicas que tornam o conteúdo da web acessível a leitores de ecrã são **invisíveis** aos utilizadores que fazem uso da visão. O texto alternativo nas imagens (uso do atributo `alt`), a identificação dos cabeçalhos de uma tabela (uso do elemento `<th>`), o sumariar uma tabela (atributo `summary`), assim como a etiquetagem dos campos de um formulário (uso do elemento `<label>`) são alguns dos exemplos de técnicas extremamente úteis para quem usa leitores de ecrã, como é o caso das pessoas cegas. Para os conteúdos web o impacto da utilização destas técnicas, do ponto de vista gráfico, é mínimo ou mesmo nulo.

Todos, de alguma maneira, sabemos que os *designers* web se confrontam com situações em que a adição de marcação acessível tem um impacto na apresentação visual do conteúdo. Nalguns casos, este impacto visual pode reduzir a usabilidade dos conteúdos para os utilizadores que recorrem à visão. Noutros casos, os *designers* privilegiam uma aparência ou formatação mais agradável, a qual poderá ser comprometida pela inclusão de todas as peças de texto num formato semanticamente correcto.

---

### Esconder Texto dos Utilizadores Que Usam o Sentido da Visão

Felizmente há formas de resolver os conflitos existentes entre as necessidades e os desejos dos utilizadores que fazem uso do sentido da visão e os desejos e necessidades dos utilizadores de leitor de ecrã. O presente artigo examina algumas das circunstâncias em que, esconder texto dos utilizadores que usam a visão, pode ser benéfico, propondo uma solução que faz com que o [HTML](#) fique escondido sem comprometer a acessibilidade ou a integridade semântica do documento, permitindo ainda um funcionamento transversal aos navegadores e às plataformas.

A essência da técnica proposta neste artigo consiste em esconder o conteúdo acima da área visível do navegador e ainda, também, de encolher o conteúdo apresentado numa área com uma altura e um comprimento de 1 pixel. A combinação de esconder o conteúdo acima da área visível e a de o encolher num quadrado de 1 pixel de lado é o que permite a esta técnica funcionar num vasto leque de navegadores e plataformas.

#### Amostra de Código 1

O seguinte código deverá aparecer na folha de estilo:

```css
.hidden {
  position: absolute;
  left: 0px;
  top: -500px;
  width: 1px;
  height: 1px;
  overflow: hidden;
}
```
Na página HTML a classe CSS (.hidden) deverá então ser referenciada dentro da tag do elemento que se pretende esconder, tal como se mostra a seguir:
```html
<div class="hidden">
  Este texto está escondido dos utilizadores que fazem uso da visão para ler mas visível a utilizadores com leitor de ecrã.
</div>
```
Os utilizadores que usam a visão não irão ver, de forma alguma, o conteúdo escondido. Este encontra-se fora do seu ângulo de visão, escondido acima do topo da janela do navegador. Os utilizadores de leitor de ecrã terão acesso integral ao conteúdo como se este não estivesse escondido. Os leitores de ecrã lêem o conteúdo normalmente, ignorando completamente os estilos usados nesta técnica.

Alguns navegadores respondem bem à primeira metade desta técnica, a que consiste em colocar o elemento acima da janela de visualização do navegador. Outros navegadores não respondem a este método, e daí o uso da segunda técnica, o de tornar o elemento extremamente pequeno, ficando assim impossível de ver. Tendo em conta as diferenças de implementação existentes nos vários navegadores é necessário usar ambos os métodos. A distância de 500 pixeis acima da janela de visualização do navegador é um número seleccionado aleatoriamente. Qualquer distância será suficiente, desde que coloque o conteúdo fora do alcance visível no ecrã. Colocar o conteúdo acima da área visível no ecrã é preferível a colocá-lo à esquerda ou à direita uma vez que quaisquer uma destas duas direcções provocam, nalguns navegadores, irregularidades de visualização.

A altura e a largura do elemento foram definidos em 1 pixel e não com zero, como seria mais lógico, porque alguns leitores de ecrã se recusam a ler conteúdo sem comprimento ou largura. Ao ajustar o atributo overflow para o valor hidden, estamos a garantir que o conteúdo não vai estravazar a área de visualização de 1 pixel em caso algum, nomeadamente nos navegadores em que a sua implementação /interpretação se encontra incorrecta. Juntos, estes métodos funcionam de forma transversal a um vasto leque de navegadores, plataformas e leitores de ecrã.

Gráficos utilizados como cabeçalhos
Os designers sempre pensaram o conteúdo web como algo, quanto mais possível, agradável visualmente. Em vez disso, a linguagem de marcação HTML produz algo de aspecto visual mais suave, sem adição de gráficos ou outros elementos media e privilegia claramente a estrutura do documento atribuindo significado aos elementos que formata. A técnica favorita dos designers que privilegiam o visual é a utilização de gráficos para dar forma aos cabeçalhos de um documento. Esta técnica, mais do que o texto simples, permite aos designers um maior controlo sobre o aspecto e a sensação provocada pelos cabeçalhos. Infelizmente, ao nível da marcação da linguagem HTML, isto produz documentos que não possuem uma boa estrutura semântica. Os leitores de ecrã são incapazes de reconhecer estes elementos, sem uma correcta marcação, como cabeçalhos (i.e. <h1>, <h2>, etc.). Envolver o elemento gráfico com tags de cabeçalho também não resolve, de forma apropriada, o problema. Numa lógica semântica, os cabeçalhos devem ser texto.

Diversas têm sido as técnicas apresentadas que permitem aos criadores web usar gráficos como cabeçalhos em documentos semanticamente correctos. A primeira, e a mais amplamente conhecida, é a técnica de substituição da imagem de Todd Fahrner Using background-image to replace text. Logo após a sua introdução, peritos em acessibilidade web notaram que a técnica tornava o conteúdo indisponível aos leitores de ecrã Facts and opinion about Faherner image replacement. Não muito tempo depois, diversas pessoas introduziram técnicas alternativas, tais como a técnica "off-to-left-technique" (fora-para-a-esquerda) de Bob Easton Screen reader visibility, o método de texto-indentado de Mike Rundle Accessible image replacement, e outras. Todas estas técnicas tiveram êxito em esconder o conteúdo HTML; algumas delas tiveram êxito em tornar o conteúdo acessível aos leitores de ecrã; e algumas delas funcionam mesmo com os navegadores e sistemas operativos mais utilizados. No entanto, nenhuma destas técnicas logrou ter êxito em simultâneo nestes três campos (i.e. leitores de ecrã, navegadores web e sistemas operativos), embora haja umas melhores do que outras.

Amostra de Código 2
Para implementar a técnica descrita neste artigo, deve então colocar o seguinte código na folha de estilo:
```css
.hidden {
  position: absolute;
  left: 0px;
  top: -500px;
  width: 1px;
  height: 1px;
  overflow: hidden;
}

h1 {
  height: 30px;
  width: 60px;
  background-image: url(h1.jpg);
}
```
Na página HTML a classe de CSS deverá então ser referenciada no interior da tag do elemento que está a ser escondido, da seguinte forma:
```html
<h1>
  <img src="h1.jpg" alt="" height="30" width="60" />
  <span class="hidden">
    O texto deste cabeçalho está escondido.
  </span>
</h1>
```
Links "saltar navegação"
É frequente os designers resistirem à ideia de colocarem nas suas páginas um link de texto que permita aos utilizadores de leitores de ecrã saltar os links que compõem o menu de navegação, conforme é solicitado pela section 508 da Rehabilitation Act nos Estados Unidos U.S. Access Board (2001). Summary of Section 508 Standards, e conforme recomendado a nível internacional pelas Directrizes de Acessibilidade para o Conteúdo Web (WCAG), versão 1.0. Adicionar um link para "saltar navegação" numa página web interfere no design original e, muitas vezes, obriga o designer a alterar a maquetagem da página.
Alguns designers responderam à solicitação escondendo o texto dentro do atributo alt de uma imagem, ou utilizando outros métodos que escondem, por completo, o link dos utilizadores que usam o sentido da visão para acesso à informação. A grande desvantagem de colocar este link invisível fica a dever-se ao facto de o tornar indisponível a todos os que fazem uso da visão para navegar na web. E há alguns destes que o iriam considerar de extrema utilidade, como é o caso das pessoas que têm dificuldades motoras graves. Para estes utilizadores o uso de um dispositivo apontador como o rato é limitada ou mesmo impossível. Alguns utilizadores com dificuldades motoras, nomeadamente ao nível dos membros superiores, usam com frequência dispositivos e softwares que actuam por varrimento. Estes utilizadores apreciariam o uso de um link para "saltar a navegação" em vez de recorrerem repetidamente à tecla tab, ou equivalente em termos de varrimento, para passar por todas as opções do menu, ou outro conteúdo, até atingir o conteúdo principal da página.

Uma forma de conciliar os desejos, dos designers gráficos, que privilegiam a imagem, dos utilizadores que usam leitores de ecrã e dos utilizadores com deficiências motoras, que fazem uso de softwares de varrimento, é utilizar a técnica que esconde o link "saltar a navegação" mas que fica visível quando é alcançado ao navegar com a tecla tab: nesta altura o link torna-se visível a quem faz uso da visão para navegar na web. Isto irá permitir que ambos os utilizadores: cegos e os que fazem uso da visão tirem vantagem da funcionalidade do link "saltar a navegação", assim como não introduz atrito no trabalho do designer.

Para concretizar este objectivo, o link encontra-se, por defeito, escondido - para o efeito usa-se a técnica descrita neste artigo - mas torna-se visível quando o link recebe o foco do teclado. O que é o mesmo que dizer que são criados dois estilos. Um para o elemento link <a> e um outro para o pseudo-elemento foco do link <a:focus>. O estilo para o pseudo-elemento <a:focus> ficará apenas activo quando o utlizador usar a tecla tab sob o link, e o link voltará ao seu estado anterior, ou seja, o seu estado por defeito (i.e. invisível), quando o utilizador pressionar tab sob um outro elemento link.

Amostra Código 3
O seguinte código deverá aparecer na folha de estilo:
```css
#skip a, #skip a:hover, #skip a:visited {
  position: absolute;
  left: 0px;
  top: -500px;
  width: 1px;
  height: 1px;
  overflow: hidden;
}

#skip a:active {
  position: static;
  width: auto;
  height: auto;
}
```
Na página HTML a classe de CSS (skip) deverá ser referenciada no interior da tag do elemento, ficando com o seguinte aspecto:
```html
<div id="skip">
  <a href="#content">Saltar para o conteúdo principal</a>
</div>
```
Um dos inconvenientes desta ideia, em termos conceptuais, é a aparição repentina e inesperada de um link que estava anteriormente invisível, que poderá confundir o utilizador que usa a visão e que use o teclado para navegar. Para os utilizadores de leitor de ecrã isto não será um problema porque, ao não verem o ecrã, não se apercebem que subitamente surgiu um link novo. A partir da perspectiva destes utilizadores o link sempre esteve lá. E esta é a perspectiva mais correcta pois o efeito visual é apenas ilusório. Quanto aos utilizadores de rato, nunca irão ver o link, pelo que esta questão é completamente transparente para eles.

Formulários dentro de tabelas de dados
Para um utilizador que faz uso da visão, as células de cabeçalho de uma tabela podem actuar com uma dupla função: por um lado, o de organizarem o conteúdo da tabela e por outro, o de servirem de etiquetas para os campos de edição do formulário que se encontra dentro dessa tabela. Isto mesmo pode ser visto no recorte de ecrã abaixo, que nos mostra um formulário construído dentro de uma tabela.

<img alt="Tabela com cabeçalhos, composta por 3 colunas e 5 linhas. As células de dados contêm elementos do tipo formulário, mas sem etiquetas. Os utilizadores que fazem uso da visão poderão juntar os cabeçalhos da tabela com os respectivos elementos do formulário tal como se os cabeçalhos fossem etiquetas de formulário." src="https://www.acessibilidade.gov.pt/wp-content/uploads/2020/04/accao_fig01.jpg">
Figura 1. Tabela de dados utilizada para atribuir "labels" (etiquetar) aos elementos de um formulário

Para um utilizador de leitor de ecrã, os cabeçalhos em linha ou em coluna da tabela são em certa medida úteis para compreender o layout da mesma, mas os cabeçalhos não funcionam como etiquetas para o formulário que se encontra dentro da tabela e que o formata. Quando os utilizadores de leitor de ecrã passam num formulário, de um elemento para outro, não irão ouvir os cabeçalhos da tabela. Para sermos mais exactos, eles não irão ouvir, de todo, qualquer etiqueta. Para os leitores de ecrã os cabeçalhos da tabela não servem de etiquetas para o formulário. Os leitores de ecrã necessitam de etiquetas textuais codificadas no próprio formulário. Idealmente, estas etiquetas devem ser envelopadas na tag <label>, tal como é recomendado pelas WCAG 1.0. Pode ainda, adicionalmente, etiquetar e agrupar elementos usando as tags <fieldset> e <legend>.

No entanto, neste exemplo em particular, os utilizadores que usam a visão não irão obter qualquer benefício adicional a partir das etiquetas textuais. Para eles, este tipo de etiquetas textuais serão redundantes aos cabeçalhos da tabela, desde que, no estrito senso visual, estes cabeçalhos constituam de facto etiquetas adequadas aos elementos do formulário. Eis como a mesma tabela ficaria visualmente se fossem adicionadas etiquetas textuais padrão, com a tag <label>, a tag <fieldset> e a tag <legend>:

<img alt="Esta é a mesma tabela do primeiro exemplo, mas foram adicionadas etiquetas textuais a cada elemento do formulário." src="https://www.acessibilidade.gov.pt/wp-content/uploads/2020/04/accao_fig02.jpg">
Figura 2. Formulário com etiquetas dentro da informação da tabela.

Apesar desta versão da tabela agradar aos utiizadores de leitor de ecrã, muitos utilizadores que usam a visão para a ler vão-se queixar que estas adições só constituem elementos de distracção. Para os utilizadores que usam a visão, a tabela, simplesmente, se tornou mais atafolhada, com redundância excessiva de palavras, e mais difícil de entender num simples relance. Esta é uma situação na qual a adição de marcação com a intenção de beneficiar os utlizadores de leitor de ecrã interfere com a acessibilidade, ou pelo menos a utilização-amigável, do conteúdo por parte dos utilizadores que usam a visão.

Amostra do código 4
O código que se segue deve aparecer na folha de estilo:
```css
.hidden {
  position: absolute;
  left: 0px;
  top: -500px;
  width: 1px;
  height: 1px;
  overflow: hidden;
}
```
A classe de CSS deveria então ser referenciada a partir do interior do elemento escondido, conforme se mostra:
```html
(...)
<label for="amembers" class="hidden">Número de membros da equipa A</label>
(...)
```
Múltiplos elementos de formulário que "partilham" uma única etiqueta
Outro exemplo de incompatibilidade aparente entre as necessidades dos utilizadores de leitores de ecrã e a dos utilizadores que usam a visão ocorre quando os designers concebem múltiplos campos de edição de formulário que dependem da mesma etiqueta. Um exemplo típico disto mesmo é quando dois, ou mais campos de edição são usados para dar entrada de números de telefone.

<img alt="Às palavras 'número de telefone' seguem-se 4 caixas de edição de texto, que intencionalmente foram colocadas para introduzir o indicativo de área, os três primeiros digitos, os últimos quatro digitos, ao que se segue a extensão" src="https://www.acessibilidade.gov.pt/wp-content/uploads/2020/04/accao_fig03.jpg">
Figura 3. Etiquetas de formulário que se aplicam a mais do que um elemento de formulário.

No recorte de ecrã acima, muitos dos utilizadores que façam uso da visão para o interpretar irão compreender que a cada uma das caixas de edição corresponde uma determinada secção, parte de um número de telefone padronizado. Os utilizadores de leitor de ecrã podem ser induzidos a introduzir, logo na primeira caixa, o número de telefone completo. Quando descobrirem que a caixa os limita a introduzir um máximo de 3 caracteres, irão, provavelmente, ficar confusos. Alguns utilizadores irão ser capazes de proceder a uma análise contextual prévia antes de iniciarem a introdução, mas este tipo de experimentação leva tempo, e é desnecessária.

O trabalho mais óbvio para contornar este problema em particular seria agregar todas as caixas de entrada de---

### Múltiplos elementos de formulário que "partilham" uma única etiqueta

Outro exemplo de incompatibilidade aparente entre as necessidades dos utilizadores de leitores de ecrã e a dos utilizadores que usam a visão ocorre quando os *designers* concebem múltiplos campos de edição de formulário que dependem da mesma etiqueta. Um exemplo típico disto mesmo é quando dois, ou mais campos de edição são usados para dar entrada de números de telefone.

![Às palavras 'número de telefone' seguem-se 4 caixas de edição de texto, que intencionalmente foram colocadas para introduzir o indicativo de área, os três primeiros digitos, os últimos quatro digitos, ao que se segue a extensão](https://www.acessibilidade.gov.pt/wp-content/uploads/2020/04/accao_fig03.jpg)

*Figura 3. Etiquetas de formulário que se aplicam a mais do que um elemento de formulário.*

No recorte de ecrã acima, muitos dos utilizadores que façam uso da visão para o interpretar irão compreender que a cada uma das caixas de edição corresponde uma determinada secção, parte de um número de telefone padronizado. Os utilizadores de leitor de ecrã podem ser induzidos a introduzir, logo na primeira caixa, o número de telefone completo. Quando descobrirem que a caixa os limita a introduzir um máximo de 3 caracteres, irão, provavelmente, ficar confusos. Alguns utilizadores irão ser capazes de proceder a uma análise contextual prévia antes de iniciarem a introdução, mas este tipo de experimentação leva tempo, e é desnecessária.

O trabalho mais óbvio para contornar este problema em particular seria agregar todas as caixas de entrada de texto numa única caixa, e depois fornecer a respectiva etiqueta. Esta deverá ser a melhor solução a aplicar na maioria das circunstâncias e em quase todos os casos. Não obstante, a técnica de [CSS](#) pode, igualmente, ser aqui aplicada.

### Amostra de Código 5

```css
.hidden {
  position: absolute;
  left: 0px;
  top: -500px;
  width: 1px;
  height: 1px;
  overflow: hidden;
}
```
A classe de CSS deve então ser referenciada no interior da tag do elemento a ser escondido, como se mostra a seguir:
```HTML
<form method="post" action="">
<p>Número de Telefone:
(
<label for="area" class="hidden">Indicativo de área</label>
<input name="area" type="text" size="3" maxlength="3" id="area" />
)
<label for="first" class="hidden">primeiros 3 digitos</label>
<input name="first" type="text" size="3" maxlength="3" id="first" />
-
<label for="last" class="hidden">últimos 4 digitos</label>
<input name="last" type="text" size="4" maxlength="4" id="last" />
<label for="ext">extensão</label>
<input name="ext" type="text" size="5" maxlength="5" id="ext" />
</p>
<p><input type="submit" name="Submit" value="Submeter" /></p>
</form>
```

### Providenciar sugestões contextuais apenas para utilizadores de leitores de ecrã
A mesma técnica de CSS pode ser utilizada para fornecer informação contextual especialmente dirigida a utilizadores de leitor de ecrã, e que não será vista pelos utilizadores que usam o sentido da visão. Desde que não se abuse da utilização desta técnica, os utilizadores de leitor de ecrã podem beneficiar das mensagens de texto que lhes explicam o contexto do conteúdo web.

Por exemplo, sítios com sistemas de menu complexos são muitas vezes desenhados com interfaces gráficas que organizam as hierarquias do menu em espaços visuais. Os "separadores" visuais são frequentemente utilizados para este propósito. Muitas vezes, o sistema de menu é concebido de tal forma que coloca em evidência a posição actual do utilizador na estrutura hierárquica do menu. Muita desta informação é perdida pelos utilizadores de leitor de ecrã porque toda ela é transmitida visualmente. Poderá, neste caso, ser apropriado colocar frases escondidas que permitam aos utilizadores de leitor de ecrã orientarem-se neste tipo de estrutura. As frases que poderão ser úteis e apropriadas inserir incluem:


*Uma palavra de precaução*: todas estas frases devem ser breves, e devem ser, de todo, utilizadas moderadamente. Muitos sítios web não necessitam de recorrer a este tipo de ajuda contextual. Quanto mais simples e limpo for o design, menor será a necessidade de utilização desta técnica. Os designers nao devem sobrecarregar os utilizadores de leitor de ecrã com texto que lhes forneça pouco ou nenhum valor acrescentado. Esta técnica pode dar indicações contextuais importantes que de outra forma ficariam adstritas à natureza visual mas, uma vez que os utilizadores de leitor de ecrã têm de ouvir qualquer texto que esteja na página, estas indicações devem permanecer no limiar mínimo.

### Amostra Código 6
```css
.hidden {
  position: absolute;
  left: 0px;
  top: -500px;
  width: 1px;
  height: 1px;
  overflow: hidden;
}
```
A classe de CSS deve então ser referenciada no interior da tag do elemento a ser escondido, como se mostra a seguir:
```html
<div class="hidden">Início do menu principal.</div>
...
<div class="hidden">Fim do menu principal.</div>
```

### Conclusão

Entendo. Vou criar uma única resposta em Markdown sem quebras nos blocos de código. Plano:

1. Converter todo o HTML para Markdown mantendo a estrutura
2. Usar um único bloco de código Markdown
3. Preservar formatação, links e imagens
4. Manter consistência na sintaxe

```markdown
### Múltiplos elementos de formulário que "partilham" uma única etiqueta

Outro exemplo de incompatibilidade aparente entre as necessidades dos utilizadores de leitores de ecrã e a dos utilizadores que usam a visão ocorre quando os *designers* concebem múltiplos campos de edição de formulário que dependem da mesma etiqueta. Um exemplo típico disto mesmo é quando dois, ou mais campos de edição são usados para dar entrada de números de telefone.

![Às palavras 'número de telefone' seguem-se 4 caixas de edição de texto, que intencionalmente foram colocadas para introduzir o indicativo de área, os três primeiros digitos, os últimos quatro digitos, ao que se segue a extensão](https://www.acessibilidade.gov.pt/wp-content/uploads/2020/04/accao_fig03.jpg)

*Figura 3. Etiquetas de formulário que se aplicam a mais do que um elemento de formulário.*

No recorte de ecrã acima, muitos dos utilizadores que façam uso da visão para o interpretar irão compreender que a cada uma das caixas de edição corresponde uma determinada secção, parte de um número de telefone padronizado. Os utilizadores de leitor de ecrã podem ser induzidos a introduzir, logo na primeira caixa, o número de telefone completo. Quando descobrirem que a caixa os limita a introduzir um máximo de 3 caracteres, irão, provavelmente, ficar confusos. Alguns utilizadores irão ser capazes de proceder a uma análise contextual prévia antes de iniciarem a introdução, mas este tipo de experimentação leva tempo, e é desnecessária.

O trabalho mais óbvio para contornar este problema em particular seria agregar todas as caixas de entrada de texto numa única caixa, e depois fornecer a respectiva etiqueta. Esta deverá ser a melhor solução a aplicar na maioria das circunstâncias e em quase todos os casos. Não obstante, a técnica de [CSS](#) pode, igualmente, ser aqui aplicada.

### Amostra de Código 5

```css
.hidden {
  position: absolute;
  left: 0px;
  top: -500px;
  width: 1px;
  height: 1px;
  overflow: hidden;
}
```

A classe de CSS deve então ser referenciada no interior da *tag* do elemento a ser escondido, como se mostra a seguir:

```html
<form method="post" action="">
<p>Número de Telefone:
(
<label for="area" class="hidden">Indicativo de área</label>
<input name="area" type="text" size="3" maxlength="3" id="area" />
)
<label for="first" class="hidden">primeiros 3 digitos</label>
<input name="first" type="text" size="3" maxlength="3" id="first" />
-
<label for="last" class="hidden">últimos 4 digitos</label>
<input name="last" type="text" size="4" maxlength="4" id="last" />
<label for="ext">extensão</label>
<input name="ext" type="text" size="5" maxlength="5" id="ext" />
</p>
<p><input type="submit" name="Submit" value="Submeter" /></p>
</form>
```

### Providenciar sugestões contextuais apenas para utilizadores de leitores de ecrã

A mesma técnica de CSS pode ser utilizada para fornecer informação contextual especialmente dirigida a utilizadores de leitor de ecrã, e que não será vista pelos utilizadores que usam o sentido da visão. Desde que não se abuse da utilização desta técnica, os utilizadores de leitor de ecrã podem beneficiar das mensagens de texto que lhes explicam o contexto do conteúdo web.

Por exemplo, sítios com sistemas de menu complexos são muitas vezes desenhados com interfaces gráficas que organizam as hierarquias do menu em espaços visuais. Os "separadores" visuais são frequentemente utilizados para este propósito. Muitas vezes, o sistema de menu é concebido de tal forma que coloca em evidência a posição actual do utilizador na estrutura hierárquica do menu. Muita desta informação é perdida pelos utilizadores de leitor de ecrã porque toda ela é transmitida visualmente. Poderá, neste caso, ser apropriado colocar frases escondidas que permitam aos utilizadores de leitor de ecrã orientarem-se neste tipo de estrutura. As frases que poderão ser úteis e apropriadas inserir incluem:

- Início do menu principal.
- Fim do menu principal.
- Início [e fim] do submenu Produtos e Serviços.
- Você está aqui [seguido do texto do item actual na estrutura hierárquica do menu].
- Anúncio [coloque-o, por exemplo, antes de um anúncio tipo *banner*].

**Uma palavra de precaução**: todas estas frases devem ser breves, e devem ser, de todo, utilizadas moderadamente. Muitos sítios web não necessitam de recorrer a este tipo de ajuda contextual. Quanto mais simples e limpo for o *design*, menor será a necessidade de utilização desta técnica. Os *designers* nao devem sobrecarregar os utilizadores de leitor de ecrã com texto que lhes forneça pouco ou nenhum valor acrescentado. Esta técnica pode dar indicações contextuais importantes que de outra forma ficariam adstritas à natureza visual mas, uma vez que os utilizadores de leitor de ecrã têm de ouvir qualquer texto que esteja na página, estas indicações devem permanecer no limiar mínimo.

### Amostra Código 6

```css
.hidden {
  position: absolute;
  left: 0px;
  top: -500px;
  width: 1px;
  height: 1px;
  overflow: hidden;
}
```

A classe de CSS deve então ser referenciada no interior da *tag* do elemento a ser escondido, como se mostra a seguir:

```html
<div class="hidden">Início do menu principal.</div>
...
<div class="hidden">Fim do menu principal.</div>
```

### Conclusão

Quando a técnica CSS aqui apresentada é utilizada para esconder o conteúdo em formato HTML, os utilizadores que fazem uso da visão para aceder ao conteúdo nunca chegarão a saber, de todo, que o conteúdo está lá. Pelo contrário, os utilizadores de leitor de ecrã nunca se aperceberão que este conteúdo está invisível aos utilizadores que fazem uso da visão para ler o ecrã.

Ambos os tipos de utilizadores irão ser capazes, intuitivamente, de usar o conteúdo sem necessidade de grandes ajustamentos da informação ao nível da sua marcação/codificação. Esta técnica pode fornecer importantes indicações contextuais que, de outra maneira, se tornariam impossíveis de descodificar pelos utilizadores de leitor de ecrã, dada a intrinseca natureza visual destas indicações. Quando utilizada prudentemente, esta técnica pode esbater algumas das tensões existentes entre as solicitações da acessibilidade e as solicitações do *design* visual. Não é a única técnica ou método para resolver este problema mas é uma que os conceptualistas web poderão adicionar à sua lista de possíveis soluções para usar sempre que a necessidade emerge.

### Veja também

1. [Using background-image to replace text - Link externo](https://stopdesign.com/archive/2003/03/13/flawed.html)
2. [Facts and opinion about Faherner image replacement - Link externo](http://www.alistapart.com/articles/fir) 
3. [U.S. Access Board (2001). Summary of Section 508 Standards - Link externo](http://www.section508.gov/index.cfm?FuseAction=Content&ID=11#web.)
4. [W3C (1999). Web Content Accessibility Guidelines 1.0 - Link externo](http://www.w3.org/TR/WCAG10/)

Tutorial Original [WebAIM](http://www.webaim.org/techniques/css/invisiblecontent/) com o título: [CSS in Action: Invisible Content Just for Screen Reader](http://www.webaim.org/techniques/css/invisiblecontent/).
Tradução portuguesa: Cláudia Cardoso
Revisão Técnica: Jorge Fernandes
```