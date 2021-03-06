python-ipagare
==============

Esse projeto tem como objetivo implementar as chamadas ao webservice do iPagare, permitindo uma integração totalmente transparente atravéz desse gateway de pagamento.

# Antes de começar

Antes de começar a utilizar os webservices é importante ler esse post:
https://ipagare.zendesk.com/entries/20318508-1-antes-de-comecar

Para começar a usar os serviços você precisa ter seu ``id de estabelecimento`` e seu ``codigo de segurança``. Essas informações são obtidas no painel de usuário do iPagare

# Serviços

Atualmente os serviços abaixo são suportados. Sinta-se a vontade para implementar os outros e contribuir com esse projeto.

## [Consultar opções de pagamento](https://ipagare.zendesk.com/entries/20339157-servico-consultar-opcoes-de-pagamento)

Esse serviço é usado para recuperar a formas de pagamento configuradas na sua conta do iPagare

```python
from ipagare.gateway import IPagareGateway
gateway = IPagareGateway(ID_ESTABELECIMENTO, CODIGO_SEGURANCA, sandbox=True)
print gateway.payment_options(total=10000)
[{
    'formas': [u'\xe0 vista', u'2x sem juros'],
    'instituicao': 'American Express',
    'convenio': 'WebPOS Webservice',
    'nome': 'American Express'
}]
```

## [Processar pagamentos pela Integração Webservice](https://ipagare.zendesk.com/entries/20338847-servico-processar-pagamentos-pela-integracao-webservice)

```python
from ipagare.gateway import IPagareGateway
gateway = IPagareGateway(ID_ESTABELECIMENTO, CODIGO_SEGURANCA, sandbox=True)
request = gateway.process_payment(total=12000,
    payment_option='28',
    payment_form_code='A02',
    card_number='4444333322221111',
    card_expires_month='10',
    card_expires_year='2015',
    card_security_code='123',
    request_code='1234')
assert request.code == '1234'
```

# Instalando

```bash
pip install python-ipagare
```