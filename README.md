# webhook-eduzz
O webhook permite que você receba notificações a cada alteração de status de uma compra. Sempre que uma compra tiver seu status atualizado ( Pago, Cancelado, Reembolsado, etc... ) nós iremos enviar uma chamada via POST para uma URL pré-configurada nas configurações do seu conteúdo com alguns parâmetros para que você possa realizar suas decisões comerciais.

Consideramos como **sucesso** todas as requisições que retornam o [status HTTP 200](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) 

## Lista de parâmetros

Parâmetro     | Descrição
------------- | -------------
trans_cod     | ID da Fatura na Eduzz ( Venda )
trans_value | Valor da compra
trans_paid    | Valor pago
trans_status  | Status do pagamento ( Ver tabela de status )
trans_paymentmethod | Forma de pagamento ( Ver tabela de forma de pagamento )
trans_createdate | Data de criação da fatura
trans_paiddate | Data de pagamento da fatura
product_cod   | ID do produto ( Conteúdo )
product_name | Nome do produto
cus_cod	| ID do Cliente na Eduzz
cus_taxnumber | Documento do Cliente
cus_name | Nome do Cliente
cus_email | E-mail do Cliente
cus_address | Endereço do Cliente
cus_address_number | Número do Endereço do cliente
cus_address_country | País do Cliente
cus_address_district | Bairro do Cliente
cus_address_comp | Complemento do Cliente
cus_address_city | Cidade do Cliente 
cus_address_state | Estado do Cliente
cus_address_zip_code | CEP do Cliente
aff_cod | ID do Afiliado na Eduzz
aff_name | Nome do Afiliado
aff_email | E-mail do Afiliado
aff_value | Valor da comissão do afiliado 


## Tabela de status da fatura

ID  | Status | Descrição
--- | ------ | -----------
3 | Paga | Compra foi paga, o cliente já esta apto a receber o produto 
4 | Cancelada | Fatura Cancelada pela Eduzz
6 | Aguardando Reembolso | Cliente solicitou reembolso, porem o mesmo ainda não foi efetuado
7 | Reembolsado | Cliente já foi reembolsado pela eduzz
8 | Em Análise | Cliente efetuou o pagamento, porém esta em análise pela instituição financeira
11 | Em Recuperacao | Fatura entrou para o processo de recuperação

## Tabela de formas de pagamento
ID	| Forma de pagamento
----	| -----
1 	| Boleto Bancário
9 	| Paypal
13 	| Visa
14	| Amex
15 	| Mastercard
16 	| Diners
17 	| Débito Banco do Brasil
18 	| Débito Bradesco
19 	| Débito Itaú
21 	| Hipercard
22 	| Débito Banrisul
23 	| Hiper
24 	| Elo
25 	| Paypal Internacional


## Exemplo php
```php
<?php

	//Exemplo webhook Eduzz

	foreach ($_POST as $key => $value)	
		$$key = $value;


	if( $api_key == 'SUACHAVEDEAPI' )
	{
		
		switch ($trans_status)
		{
			case '3' :
						#Pagou
						libera_acesso();
				break;
			case '6':   #Aguardando reembolso
			case '7':   #Reembolsado
						remove_acesso();
						break;
				#...
				#...
				#...
			default:
				echo "STATUS DESCONHECIDO";
				break;
		}
	}
	else
		echo "ACESSO INVALIDO";

	function libera_acesso()
	{
		echo "ACESSO LIBERADO";
	}

	function remove_acesso()
	{
		echo "ACESSO REMOVIDO";
	}

?>
```



