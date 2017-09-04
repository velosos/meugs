# meugs
Painel de acompanhamento de chamados em tempo real na ServiceNow

![alt text](https://github.com/velosos/globoguru/blob/master/guru/core/static/img/Captura%20de%20Tela%202017-09-04%20%C3%A0s%2015.00.57.png)


Para facilitar onde os especialistas da globo.com devem atuar, foi criado o MEUGS, um painel de acompanhamento dos chamados que precisam ser atuados e seus respectivos avanços. No exemplo da imagem acima, a tabela usada é a de *problem* (PRB)

O layout foi inspirado nesse tema em bootstrap: 
https://blackrockdigital.github.io/startbootstrap-sb-admin-2/pages/index.html

A criação dentro da ServiceNow foi um conteúdo dinâmico
Caminho: *Gerenciamento de Conteúdo > Blocos > Dinâmico*


Criando filtros para exibicao:


```
<g:evaluate var="jvar_prb_group" object="true">
	   
     var queryString = "assignment_groupINjavascript:gs.getUser().getMyGroups()^active=true^ORDERBYDESCnumber^EQ";
     var gr = new GlideRecord('problem');
	   gr.addEncodedQuery(queryString);
	   gr.query();
     gr;	     

</g:evaluate>

```



Criando condições de cores de acordo com o status, passando como condicional a class CSS:

```
<g:evaluate var="color" object="true" >		
	var color =""; 
		<j:if test="${jvar_prb_group.getValue('state')!= '5'}">	
		color ="panel panel-danger"
			
		</j:if> 	
   
		<j:if test="${jvar_prb_group.getValue('state')== '5'}">
        color ="panel panel-success"
   
		</j:if> 
    </g:evaluate>	

```

Declarando minha class na DIV, após o condicional: 

```
<div class="${color}"

```

Exemplo da exibicao dos campos relacionado ao chamado( status ):

  ```
	<p> <strong> Status: </strong> ${jvar_prb_group.getChoiceValue('state')} </p>
  ```
  
  
  
