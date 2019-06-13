# Projeto-01
########################################################################
#                         HELLO WORD								   #
#																	   #
#	 PROJETO DA 3° UNIDADE DO CURSO DE BSI/UFRN-CAICÓ - 2018.1		   #
#    MATERIA: ALGORITMOS E LÓGICA DE PROGRAMAÇÃO                       #
#    PROF. FLAVIUS DA LUZ E GORGONIO 								   #
#	 PROF. AMARILDO JEIELE FERREIRA DE LUCENA 						   #
#	 ALUNO MACIEL LUCIANO DOS SANTOS								   #
#    ALUNO INALDO MACENA SILVA DE LIMA								   #
#    ALUNO JOANDERSON NATANAEL MEDEIROS FERREIRA					   #
#    																   #
#    >> DESCRIÇÃO: O TRABALHO BASEADO NA LINGUAGEM PYTHON 3, SIMULAMOS #
#    ALGUNS PROCEDIMENTO E MECANIMOS COMUNS EM UMA PEQUENA EMPRESA.    #
#																	   #
#    FORAM IMPLEMENTADOS: CADASTRAMENTO DE USUARIO > LOGIN > MENU DE   #
#    OPÇÕES > CONTROLE DE ESTOQUE > ATENDIMENTO DE CAIXA.              #
# 																	   #
#    COMENTARIOS: EMPREGANDO CONHECIMENTOS ABORDADOS, BASEADOS EM      #
#    ESTUDOS E MATÉRIAS TRATADAS EM SALAS DE AULA, NO DECORIDO DO      #
#    1° SEMESTRE, BUSCAMOS EXPOR A MAIOR GAMA DE MECANIMOS, ESTROTURAS #
#    PARA COMPOR ESTE PROJETO.										   #
#                                                                      #
#                                                  DATA 01/JULHO/2018  #
########################################################################







print("""
                                        █ █ █▀▀ █▀▀█ █▄ █
                                        █ █ █▀▀ █ █  █ ▀
                                        ▀▀▀ ▀   ▀  ▀ ▀  """)

import os 																# BIBLIOTECA "SISTEMA" (P/ LIMPAR A TELA DO PROMPT)

usuario = {} 															#DICIONARIO PARA ARMAZENAR LOGIN/SENHA
estoq = {} 																#DICIONARIO ESTOQUE
balanco_de_caixa = []													#LISTA PARA BALANÇO DE CAIXA 
lista_de_compras = []													#LISTA P/ ACIONAR ITENS AO CARRINHO DE COMPRAS
soma_total = []															#LISTA AUXILIAR P/ SOMAR VALORES


def somar_elementos(soma_total):                                        #SOMA VALORES DO CAIXA 
  soma_t = 0
  for i in soma_total:
    soma_t += i
  return soma_t
  
#▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀ MENU INICIAL ▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀

def inicio():
	abc_inicio = "═"*13
	print ("  ╔═%s╗" %(abc_inicio))
	print ("  ║ Menu Inícial ║")
	print ("  ╚═%s╝" %(abc_inicio))

	global cad 															#GLOBAL --> DEFINE A VARIÁVEL P/ USO GLOBAL
	
	a = True
	while a:
		cad = input("""[1] Cadastrar novo usuário
[2] Login
Digite sua opção: """)
		a = False
		if cad != "1" and cad != "2":
			print ("  > Opção invalida!\n")
			a = True
		elif cad =="1":
			os.system("cls") #LIMPA TELA DO PROMPT
			cadastro()													#REDIRECIONA AO MENU CADASTRO
		elif cad == "2":
			os.system("cls")
			login()														#REDIRECIONA AO MENU LOGIN

#▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀ CADASTRAMENTO ▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀

def cadastro():
	abc_cadastro = "═"*14
	print ("             ╔═%s╗" %(abc_cadastro))
	print ("             ║ Cadastramento ║")
	print ("             ╚═%s╝" %(abc_cadastro))
	
	global loginCad
	
	loginCad = input("Digite um nome de USUÁRIO a ser cadastrado: ")
	passwordCad = input("Digite uma SENHA a ser cadastrada: ")
	usuario [loginCad] = (passwordCad)
	os.system("cls")
	login() 															#REDIRECIONA O USUÁRIO AO LOGIN APÓS O CADASTRAMENTO

#▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀ MENU DE LOGIN ▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀

def login():
	abc_login = "═"*6
	print ("       ╔═%s╗" %(abc_login))
	print ("       ║ Login ║")
	print ("       ╚═%s╝\n" %(abc_login))
	
	if cad == "1":
		print("""Cadastro realizado com sucesso!!
Olá, %s, seja bem-vindo(a)!""" % (loginCad))

	cont = 0
	cond = True	
	while cond == True:													#TELA DE LOGIN E SUAS CONDICIONAIS
		
		global login_usuario 
		global password
		
		login_usuario = input("\nDigite o nome do usuário: ")
		
		cond = False
		if login_usuario in usuario:
			password = input(" > Digite sua senha: ")
			if (usuario[login_usuario] == password) == False:
				print(" > Senha inválida!\n")
				cond = True
			elif (usuario[login_usuario] == password) == True:
				os.system("cls")
				opcoes()				
		else:
			print(" > Login inválido!\n")
			cont += 1
			if cont %3 == 0:                                            #SE O USUÁRIO ERRAR TRÊS VEZES O LOGIN, TERÁ A OPÇÃO DE RETORNAR O MENU 
				voltar = input("\n       Deseja voltar ao início (S/N?) ")
				if voltar == "s" or voltar == "S":
					os.system("cls")
					inicio()											#REDIRECIONA AO MENU INÍCIO
			cond = True

#▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀ MENU OPÇÕES ▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀

def opcoes():
	abc_opcoes = "═"*15
	print ("   ╔═%s╗" %(abc_opcoes))
	print ("   ║ Menu de Opções ║")
	print ("   ╚═%s╝" %(abc_opcoes))

	a = True
	while a:
		opcao = input("""[1]| Início
[2]| Caixa
[3]| Estoque
Digite sua opção? """)
		a = False
		if opcao != "1" and opcao != "2" and opcao != "3":				#CONDICIONAL P/ OPÇÃO INVALIDA
			print ("  > Opção invalida!\n")
			a = True
		elif opcao == "1":
			os.system("cls")   	#LIMPA TELA DO PROMPT
			inicio()													#REDIRECIONA AO MENU INÍCIO
		elif opcao == "2":
			os.system("cls")
			caixa()														#REDIRECIONA AO MENU CAIXA
		elif opcao == "3":
			os.system("cls")   	#LIMPA TELA DO PROMPT
			estoque()													#REDIRECIONA AO MENU ESTOQUE

#▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀ CONTROLE DE ESTOQUE ▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀

def estoque():
	abc_estoque = "═"*20
	print ("    ╔═%s╗" %(abc_estoque))
	print ("    ║ Controle de Estoque ║")
	print ("    ╚═%s╝" %(abc_estoque))
	
	cond = True
	while cond:
		menu_estoque = input("""[1] | Exibir Estoque              |
[2] | Consutar Produto no Estoque |
[3] | Cadastrar novo Produto      |
[4] | Alterar Produto no Estoque  |
[5] | Excluir produto no estoque  |
[6] | Voltar ao menu anterior     |

Digite sua opção: """)
		cond = False
		if menu_estoque != "1" and menu_estoque != "2" and menu_estoque != "3" and menu_estoque != "4" and menu_estoque != "5" and menu_estoque != "6":
			os.system("cls")
			print ("\n  > Opção invalida!\n")
			print ("    ╔═%s╗" %(abc_estoque))
			print ("    ║ Controle de Estoque ║")
			print ("    ╚═%s╝" %(abc_estoque))
			cond = True
			
		elif menu_estoque == "1":										#Exibir Estoque
			os.system("cls")
			print("\n",estoq, "\n")
			cond = True
			
		elif menu_estoque == "2":										#Cadastrar novo Produto
			
			cont_consulta = 0
			cond_consulta = True
			while cond_consulta:										#CONSULTA O ESTOQUE
				consulta = input("Digite o nome do produto para ver suas informações: ")
				if consulta in estoq:
					print ("\n", consulta, estoq[consulta], "\n")
					cond_consulta = False
					voltar_consulta = input("\n > Deseja voltar ao menu Estoque (S/N?) ")
					if voltar_consulta == "s" or voltar_consulta == "S":
						cond_consulta = False
						os.system("cls")
						estoque()										#RETORNA AO MENU ESTOQUE
					else:
						cond_consulta = True
				else:
					print(" > Não existem produtos com esse nome no estoque!!\n")
					cont_consulta += 1
					cond_consulta = True
					if cont_consulta %2 == 0:                           #SE O USUÁRIO ERRAR DUAS VEZES, TERÁ A OPÇÃO DE RETORNAR O MENU 
						voltar = input("\n      > Deseja voltar ao menu Estoque (S/N?) ")
						if voltar == "s" or voltar == "S":
							os.system("cls")
							estoque()									#RETORNA AO MENU ESTOQUE
						
		elif menu_estoque == "3":										#CADASTRA PRODUTOS NO ESTOQUE
			cond_estoq = True
			while cond_estoq:
				print("\n >> PADRONIZE OS CADASTROS USANDO SENPRE LETRAS MAIUSCÚLAS << ")
				produto = input("\nDigite o nome do pruduto a ser cadastrado:\n")
				if produto == "":										#O NOME DO PRODRUTO NÃO PODERÁ SER CADASTRADO COM "ENTER"
					print(" > Cadastramento Invalido")
					sair = input(" > Aperte ENTER para voltar: ")
					if sair == "":										#SE O USUÁRIO APERTAR "ENTER", RETORNARA AO MENU ESTOQUE
						os.system("cls")
						estoque()
				else:
					valor_produto = float(input("\nValor do produto R$: "))
					quantidade_produto = int(input("\nQuantas unidades? "))
					estoq [produto] = {"valor": valor_produto, "quantidade": quantidade_produto}
					retorno = input("""\n > Aperte a tecla ENTER para VOLTAR
 > Ou qualquer outra tecla para CADASTRAR novo produto no estoque: """)
				if retorno == "":
					cond_estoq = False
					os.system("cls")
					estoque()											#RETORNA AO MENU ESTOQUE
				else:
					cond_estoq = True
		elif menu_estoque == "4": 										#Altera Produtos no Estoque 
			os.system("cls")
			print ("    ╔═%s╗" %(abc_estoque))
			print ("    ║ Controle de Estoque ║")
			print ("    ╚═%s╝" %(abc_estoque))
		
			cond_alt_est = True
			cont_est = 0
			while cond_alt_est:											#SUBMENU > ALTERAÇÕES
				alteracao = (input("""[1] |Alterar Nome do Produto       
[2] |Alterar Valor do Produto      
[3] |Alterar Quantidade do Produto 
[4] |Exibir Estoque
[5] |Voltar

Digite sua opção: """))
				if alteracao != "1" and alteracao != "2" and alteracao != "3" and alteracao != "4" and alteracao != "5":
					print (" > Opção invalida")
					cond_alt_est = True
					
				elif alteracao == "1":
					cond_alt_nome_est = True
					while cond_alt_nome_est:
						alterar = input("\nDigite o nome do produto de deseja alterar: ")
						if alterar in estoq:
							guarda_valor = estoq [alterar]["valor"]
							guarda_qunatidade = estoq [alterar]["quantidade"]
							produto_alterar = input("\nDigite o novo nome do pruduto para concluir a alteração: ")
							estoq [produto_alterar] = {"valor": guarda_valor, "quantidade": guarda_qunatidade}
							del(estoq[alterar])
							print(" > ALTERAÇÃO REALIZADA COM SUCESSO!!")
							cond_alt_nome_est = False
						else:
							print(" > Não existem produtos com esse nome no estoque!!\n")
							cont_est += 1
							cond_alt_nome_est = False
							if cont_est %2 == 0:                        #SE O USUÁRIO ERRAR DUAS VEZES, TERÁ A OPÇÃO DE RETORNAR O MENU 
								voltar = input("\n      > Deseja voltar ao menu Estoque (S/N?) ")
								if voltar == "s" or voltar == "S":
									os.system("cls")
									estoque()							#RETORNA AO MENU ESTOQUE
									
				elif alteracao == "2":									#Alterar Valor do Produto
					alterar = input("Digite o nome do produto de deseja alterar: ")
					
					cont_valor = 0
					cond_valor = True
					while cond_valor:
						if alterar in estoq:
							alterar_valor = float(input("\n > Digite o Novo Valor: "))
							estoq[alterar]["valor"] = alterar_valor
							print("ALTERAÇÃO REALIZADA COM SUCESSO!!")
							cond_valor = False
						else:
							print(" > Não existem produtos com esse nome no estoque!!\n")
							cont_valor += 1
							cond_valor = False
							if cont_valor %2 == 0:                      #SE O USUÁRIO ERRAR DUAS VEZES, TERÁ A OPÇÃO DE RETORNAR O MENU 
								voltar = input("\n      > Deseja voltar ao menu Estoque (S/N?) ")
								if voltar == "s" or voltar == "S":
									os.system("cls")
									estoque()
									
				elif alteracao == "3":									#Alterar Quantidade do Produto					
					cont_alt = 0
					cond_alt = True
					while cond_alt:
						alterar = input("\nDigite o nome do produto de deseja alterar: ")
						if alterar in estoq:
							alterar_quant = int(input("\nDigite a Nova Quatidade: "))
							estoq[alterar]["quantidade"] = alterar_quant
							print(" > ALTERAÇÃO REALIZADA COM SUCESSO!!")
							cond_alt = False
						else:
							print("\n > Não existem produtos com esse nome no estoque!!\n")
							cont_alt += 1
							if cont_alt %2 == 0:                        #SE O USUÁRIO ERRAR DUAS VEZES, TERÁ A OPÇÃO DE RETORNAR O MENU 
								voltar = input("\n      > Deseja voltar ao menu Estoque (S/N?) ")
								if voltar == "s" or voltar == "S":
									os.system("cls")
									estoque()							#RETORNA AO MENU ESTOQUE
									
				elif alteracao == "4":									#EXIBE O ESTOQUE
					print("\n", estoq, "\n")
					cond_alt_est = True

				elif alteracao == "5":									#RETORNA AO MENU INICIAL DO ESTOQUE									
					os.system("cls")
					estoque()
					
		elif menu_estoque == "5":										#EXCLUI UM PRODUTO DO ESTOQUE
			cond_del = True
			cont_del = 0
			while cond_del:
				deletar = input("\nDigite o nome do produto de deseja EXCLUIR: ")
				if deletar in estoq:
					del(estoq[deletar])
					cond_del = False
					os.system("cls")
					print("\n > EXCLUÇÂO REALIZADA COM SUCESSO!!\n")
					estoque()
				else:
					print("\n > Não existem produtos com esse nome no estoque!!\n")
					cont_del += 1
					cond_alt = False
					if cont_del %2 == 0:                                #SE O USUÁRIO ERRAR DUAS VEZES, TERÁ A OPÇÃO DE RETORNAR O MENU 
						voltar_del = input("\n     > Deseja voltar ao menu Estoque (S/N?) ")
						if voltar_del == "s" or voltar_del == "S":
							os.system("cls")
							estoque()
							
		elif menu_estoque == "6":										#Voltar ao menu anterior (opções)
			os.system("cls") # LIMPA TELA DO PROMPT
			opcoes()

#▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀ CAIXA ▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀
def abc():
	abc_caixa = "═"*7
	print ("\n                         ╔═%s╗" %(abc_caixa))
	print ("                         ║ VENDAS ║")               		#CABEÇARIO P/ TELA DE VENDAS
	print ("                         ╚═%s╝" %(abc_caixa))
	print ("           Digite 'FIM' para finalizar a venda.\n")			#EXIBE UMA INSTRUÇÃO AO USUSÁRIO

def caixa():
	abc_caixa = "═"*14
	print ("   ╔═%s╗" %(abc_caixa))
	print ("   ║ MENU DE CAIXA ║")
	print ("   ╚═%s╝" %(abc_caixa))
	
	cond_caixa = True
	cont_caixa = 0
	while cond_caixa:
		cond_caixa = False
		menu_c = input("""[1]| Vendas
[2]| Balanço de Caixa
[3]| Voltar ao Menu Opções

Digite sua opção: """)

		if menu_c == "1":												# CARRINHO / VENDAS
			os.system("cls")
			abc()				
			cond_caixa2 = True
			cont_caixa2 = 0
			while cond_caixa2:
				venda = input("Digite o nome do produto para ser adicionado a lista de compras:\n")
				if venda in estoq:
					for x in lista_de_compras:
						print ("Itens adicionados: %s" %x)
					quantidade = int(input("Quantidade: "))
					soma = estoq[venda]["valor"]
					lista_de_compras.append(venda)						#ADICIONA O PRODUTO EM UMA LISTA
					soma_total.append(soma * quantidade)				#O VALOR É MULTIPLICADO PELO VALOR DO PRODUTO E ADC A LISTA 
					print ("\n > Valor do item: R$ %.2f" %soma)
					print (" > Somador: R$ %.2f \n" % somar_elementos(soma_total))
				elif venda == "fim" or venda == "FIM" or venda == "Fim":#CONCLUI A VENDA 
					cond_fim = True
					while cond_fim:
						for x in lista_de_compras:
							print ("Item %s" %x, "R$ %.2f" % estoq[x]["valor"])		#MOSTRA A LISTA DE COMPRAS / VALORES INDIVIDUAIS
						print (" > Total a pagar :R$ %.2f" % somar_elementos(soma_total))  #MOSTRA TOTAL A PAGAR
						balanco_de_caixa.append(somar_elementos(soma_total))
						del soma_total[:]								#ZERA AS LISTAS P/ UM NOVO CICLO
						del lista_de_compras[:]							#ZERA AS LISTAS P/ UM NOVO CICLO
						cond_caixa2 = False
						voltar_fim = input("\n > Aperte 'ENTER' para voltar ao menu Caixa. ")
						if voltar_fim == "":
							os.system("cls") # LIMPA TELA DO PROMPT
							caixa()
						else:
							cond_fim = True
					
				elif (venda not in estoq) and (venda != "fim" or venda != "FIM" or venda != "Fim"): #CONDICIONAL P/ PRODUTO NÃO ENCAONTRADO NO ESTOQUE
					print (" > PRODUTO NÃO ENCONTRADO NO ESTOQUE!!")
		elif menu_c =="2":												#Balanço de Caixa (MOSTRA OS VALORES SOMADOS AO DE TODAS AS VENDAS) 
			cond_balanco = True
			while cond_balanco:
				print(balanco_de_caixa)
				voltar_balanco = input("\n >> Aperte 'ENTER' para voltar ao Menu Caixa. ")
				if voltar_balanco == "":
					os.system("cls") # LIMPA TELA DO PROMPT
					caixa()
				else:
					cond_balanco = True
		elif menu_c == "3":
			cond_c = False
			os.system("cls") # LIMPA TELA DO PROMPT
			opcoes()
		elif menu_c != "1" and menu_c != "2" and menu_c != "3":			#CONDICIONAL P/ OPÇÃO INVALIDA
			print(" > Opsão Invalida!!")
			cond_caixa = True

#▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀▀

inicio()																#LINHA DE EXECUÇÃO
