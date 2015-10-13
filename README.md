# webhook-eduzz
O webhook permite que você receba notificações a cada alteração de status de uma compra. Sempre que uma compra tiver seu status atualizado ( Pago, Cancelado, Reembolsado, etc... ) nós iremos enviar uma chamada via POST para uma URL pré-configurada nas configurações do seu conteúdo com alguns parâmetros para que você possa realizar suas decisões comerciais.

## Lista de parâmetros

Parâmetro     | Descrição
------------- | -------------
trans_cod     | ID da Fatura na Eduzz ( Venda )
trans_value | Valor da compra
trans_paid    | Valor pago
trans_status  | Status do pagamento ( Ver tabela de status )
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


