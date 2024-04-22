# banking-system-dio - Desfaio de código DIO

### Código em python responsável pela criação de um apalicação para banco que faz opreações básicas de saque, depósito e abertura de extrato DESAFIO 1

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

### Código em python responsável pela criação de um aplicação para banco que faz operações básicas de saque, depósito e abertura de extrato, criação de usuárrio e vinculação de usuários e contas criadas DESAFIO 2

        def menu ():
        menu = """
        Determine a operação que gostaria de realizar
        ---------------------------------------------
        [s] = \tSaque
        [d] = \tDepósito
        [e] = \tExtrato
        [cu] = \tCriar usuário
        [lu] = \tListar usuários
        [cc] = \tCriar conta
        [f] = \tFinalizar
        ---------------------------------------------
        """
        return input(menu)
    
    def sacar(*,saldo, valor, extrato, numero_saques, limites_saques):
    
        saldo_insuficiente = valor > saldo
        excedeu_limite = valor > 500
        excedeu_saques = numero_saques >= limites_saques
    
        if saldo_insuficiente:
            print("Operação não realizada! Saldo insuficiente")
        elif excedeu_limite:
            print("Valor de saque determinado é maior que o limite por saque de 500 reais")
        elif excedeu_saques:
            print("Quantidade de saques diários atingido, máximo de 3")
        elif valor > 0:
            saldo -= valor
            numero_saques += 1
            extrato += f"Saque:\tR$ {valor:.2f}\n"
        else: 
            print("Valor inválido, valor preenchido é menor que 0")
    
        return saldo, extrato
    
    def depositar(saldo, valor, extrato,/):
        if valor > 0:
            saldo += valor
            extrato += f"Depósito: R$ {valor:.2f}\n"
        else:
             print("Valor inválido, valor para depósito menor ou igual a 0")
        return saldo, extrato
    
    def mostrar_extrato(saldo,/,*, extrato):
        print("\n================ EXTRATO ================")
        print("Não foram realizadas movimentações." if not extrato else extrato)
        print("==========================================")
        print(f"\nSaldo: R$ {saldo:.2f}")
    
    def criar_usuario(usuarios):
        cpf = input("Determine o seu CPF: \n->")
        usuario = filtrar_usuario(cpf,usuarios)
    
        if usuario:
            print("Já existe esse usuário cadastrado no sistema")
            return
        else:
            nome = input("Determine o nome do usuário\n ->")
            data_nascimento = input("Determine a data de nascimento, seguindo o padrão dd-mm-aaaa\n ->")
            endereco = input("Determine o endereço, seguindo o padrão RUA-N°-BAIRRO-CIDADE/UF\n ->")
            usuarios.append({
                "Nome":nome,
                "Data de nascimento":data_nascimento, 
                "CPF":cpf,
                "Endereço":endereco })
            print("Usuário cadastrado com sucesso")
    
    def filtrar_usuario(cpf, usuarios):
        usuarios_filtrados = [usuario for usuario in usuarios if usuario['CPF'] == cpf]
        return usuarios_filtrados[0] if usuarios_filtrados else None
    
    def listar_usuarios(contas):
        for conta in contas:
            linha = f"""
            Agência:{conta['agencia']}
            C/C: \t {conta['numero_conta']}
            Titular:{conta['usuario']['Nome']}"""
        print(linha)
    
    def criar_conta(agencia,numero_conta,usuarios):
        cpf = input("Informe o CPF do usuário:\n->")
        usuario = filtrar_usuario(cpf, usuarios)
    
        if usuario:
            print("Conta criada com sucesso!")
            return {"agencia": agencia, "numero_conta": numero_conta, "usuario": usuario}
    
        print("\nUsuário não encontrado, cadastre um CPF primeiro")
    
        def main():
    
        extrato = ""
        saldo = 0
        LIMITE_SAQUES_DIARIOS = 3
        numero_saques = 0
        contas = []
        usuarios = []
        numero_conta = 1
        AGENCIA = "0001"
    
        while True:
    
            opcao = menu()
            
            if opcao == "s": #Saque
    
                valor = float(input("Determine o valor que deseja sacar (Até 500 reais) \n-> "))
                saldo, extrato = sacar(
                    saldo = saldo, 
                    valor = valor, 
                    extrato= extrato,
                    numero_saques = numero_saques,
                    limites_saques = LIMITE_SAQUES_DIARIOS,)
                
            elif opcao == "d": #Depósito 
                valor = float(input("Determine o valor que deseja depositar \n-> "))
                saldo, extrato = depositar(saldo, valor, extrato)
                
            elif opcao == "e": #Demonstração de extrato
                mostrar_extrato(saldo,extrato=extrato)
    
            elif opcao == "cu": #Cadastro de usuários
                criar_usuario(usuarios)
    
            elif opcao == "lu": #Listar usuários
                listar_usuarios(contas)
    
            elif opcao == "cc": #Cadastro de contas
                
                conta = criar_conta(AGENCIA, numero_conta,usuarios)
    
                if conta:
                    numero_conta += 1
                    contas.append(conta)
            
            elif opcao == "f": #Finalizar operações 
                print("Agradecemos a utilização do nosso aplicativo")
                break
    
        main()
