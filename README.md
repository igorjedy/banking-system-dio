# banking-system-dio - Desfaio de código DIO

### Código em python responsável pela criação de um apalicação para banco que faz opreações básicas de saque, depósito e abertura de extrato

menu = """
Determine a operação que gostaria de realizar

[s] = Saque
[d] = Depósito
[e] = Extrato
[f] = Finalizar

"""

limite = 500
extrato = ""
saldo = 0
LIMITE_SAQUES_DIARIOS = 3
numero_saques = 0

while True:

    opcao = input(menu)
    
    if opcao == "s": #Saque

        valor = float(input("Determine o valor que deseja sacar (Até 500 reais) \n-> "))
        saldo_insuficiente = valor > saldo
        excedeu_limite = valor > 300
        excedeu_saques = numero_saques >= LIMITE_SAQUES_DIARIOS

        if saldo_insuficiente:
            print("Operação não realizada! Saldo insuficiente")
        elif excedeu_limite:
            print("Valor de saque determinado é maior que o limite por saque de 500 reais")
        elif excedeu_saques:
            print("Quantidade de saques diários atingido, máximo de 3")
        elif valor > 0:
            saldo -= valor
            numero_saques += 1
            extrato += f"Saque: R$ {valor:.2f}\n"
        else: 
            print("Valor inválido, valor preenchido é menor que 0")

    elif opcao == "d": #Depósito 
        deposito = float(input("Determine o valor que deseja depositar \n-> "))
        if deposito > 0:
            saldo += deposito
            extrato += f"Depósito: R$ {deposito:.2f}\n"
        else:
            print("Valor inválido, valor para depósito menor ou igual a 0")
        
    elif opcao == "e": #Demonstração de extrato
        print("\n================ EXTRATO ================")
        print("Não foram realizadas movimentações." if not extrato else extrato)
        print("==========================================")
        print(f"\nSaldo: R$ {saldo:.2f}")

    elif opcao == "f": #Finalizar operações

        print("Agradecemos a utilização do nosso aplicativo")
        break

    else:
        print("Operação inválida, selecione uma opção dentro do menu")
