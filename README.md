'''Created on Mon Nov 13 20:40:33 2023
@author: Gabriel Sugayama (RM 99265) Arthur Petrin (RM 98735)'''

# Nosso projeto visa a implementação de um sistema de gestão hospitalar,
# para o administrador poder adicionar paciente e seu estado de saúde, 
# atualizá-lo e deletado quando o tratamento surtir efeito


# Link para o vídeo explicando o código:
# https://youtu.be/g6n9G967zG8


import json
import os

# Caminho do arquivo JSON para armazenar os pacientes
DB_FILE_PATH = "pacientes_db.json"



# Função para carregar os pacientes do arquivo JSON
def carregarPacientes():
    pacientes = {}
    if not os.path.exists(DB_FILE_PATH):
        # Se o arquivo não existir, retorna um dicionário vazio
        return pacientes

    with open(DB_FILE_PATH, "r") as file:
        pacientes = json.load(file)
    return pacientes

#---------------------------------------------------------

# Função para salvar os pacientes no arquivo JSON
def salvarPacientes(pacientes):
    with open(DB_FILE_PATH, "w") as file:
        json.dump(pacientes, file, indent=2)

#---------------------------------------------------------

# Função para adicionar paciente a um dicionário
def pacienteAdd(dicioPaciente):
    nomePaciente = input("Digite aqui o nome: ")
    doencaPaciente = input("Digite o nome da doença do paciente: ")

    paciente = {"nome": nomePaciente, "doenca": doencaPaciente}
    dicioPaciente[nomePaciente] = paciente
    print("")
    print("Paciente adicionado com sucesso")
    print("")

#---------------------------------------------------------

# Função para atualizar a doenca do dicionário do paciente
def atualizarPaciente(dicioPaciente):
    nomePaciente = input("Digite aqui as informações atualizadas do paciente: ")

    if nomePaciente in dicioPaciente:
        print("")
        print("----------------------------------------")
        print("Informações atuais do paciente:")
        print(f"Nome do paciente: {dicioPaciente[nomePaciente]['nome']}")
        print(f"Doença do paciente: {dicioPaciente[nomePaciente]['doenca']}")
        print("----------------------------------------")
        print("")

        # Nova doença do paciente após o tratamento médico
        print("")
        novaDoenca = input("Digite a doenca atualizada: ")
        print("")

        # Atualizando a doenças no dicionário
        # Usando tratamento de erros, caso as doenças sejam iguais
        novaDoenca = (novaDoenca)
        if novaDoenca != dicioPaciente[nomePaciente]["doenca"]:
            dicioPaciente[nomePaciente]["doenca"] = novaDoenca
            print("")
            print("Dicionário atualizado")
            print("")
        else:
            print("")
            print("A Doença deve ser diferente da original")
            print("")
    else:
        print("Paciente não encontrado")

#---------------------------------------------------------

# Função para deletar paciente do dicionário
def deletarPaciente(dicioPaciente):
    nomePaciente = input("Digite o nome do paciente a ser deletado: ")

    if nomePaciente in dicioPaciente:
        del dicioPaciente[nomePaciente]
        print("")
        print("Paciente deletado")
        print("")
    else:
        print("")
        print("Paciente não encontrado")
        print("")

#---------------------------------------------------------

# Função para exibir o menu
def exibirMenu():
    print('''
          ----------------------------------------
          1 = Adicionar paciente
          2 = Atualizar paciente
          3 = Deletar paciente
          4 = Exibir lista de pacientes
          5 = Sair
          ----------------------------------------
          ''')

#---------------------------------------------------------

# Dicionário para armazenar pacientes
dicioPaciente = carregarPacientes()

#---------------------------------------------------------

# Loop principal do programa
if __name__ == "__main__":
    while True:
        exibirMenu()
        choice = input("Digite o número da opção desejada: ")

        if choice == '1':
            pacienteAdd(dicioPaciente)
        elif choice == '2':
            atualizarPaciente(dicioPaciente)
        elif choice == '3':
            deletarPaciente(dicioPaciente)
        elif choice == '4':
            print("")
            print("Lista de Pacientes:")
            print("")
            for paciente in dicioPaciente.values():
                print(f"Nome: {paciente['nome']} / Doença: {paciente['doenca']}")
        elif choice == '5':
            print("Saindo do sistema. Até mais!")
            salvarPacientes(dicioPaciente)  # Salvar pacientes antes de sair
            break
        else:
            print("")
            print("Opção inválida. Por favor, escolha uma opção válida.")
            print("")

